# ちょっと細かいはなし

ここに書かれていることは、CPythonのテクニカルな詳細であって、全く理解する必要ありませんが、知っていればよりPythonの理解が深まります。

## リンク

- [CPythonソースツリー検索ツール](https://elixir.ortiz.sh/python/latest/source)

## CPythonのリストのメモリ利用

### リスト構造体

CPythonのリストは[listobject.h](https://elixir.ortiz.sh/python/v3.9.0/source/Include/cpython/listobject.h)と[listobject.c](https://elixir.ortiz.sh/python/v3.9.0/source/Objects/listobject.c)で実装されています。

以下のように、`listobject.h`を見ると、リストがCの構造体`PyListObject`として定義されているのが分かります。

```C
// listobject.hより
typedef struct {
    PyObject_VAR_HEAD
    /* Vector of pointers to list elements.  list[0] is ob_item[0], etc. */
    PyObject **ob_item;

    /* ob_item contains space for 'allocated' elements.  The number
     * currently in use is ob_size.
     * Invariants:
     *     0 <= ob_size <= allocated
     *     len(list) == ob_size
     *     ob_item == NULL implies ob_size == allocated == 0
     * list.sort() temporarily sets allocated to -1 to detect mutations.
     *
     * Items must normally not be NULL, except during construction when
     * the list is not yet visible outside the function that builds it.
     */
    Py_ssize_t allocated;
} PyListObject;
```

ごちゃごちゃ書いてありますが、ほとんどコメントです。とても分かりやすく、以下のように、「`ob_item`はリストの要素へのポインタのベクトルです」と書いてあります。

```C
    /* Vector of pointers to list elements.  list[0] is ob_item[0], etc. */
    PyObject **ob_item;
```

つまり、Pythonのリストの本体は、C言語の**ポインタ配列**です。64ビット処理系ではポインタは8バイトで、メモリのアドレスを格納します。ただしC言語のポインタはアドレスを格納するだけでなく、演算が定義されており、参照されるオブジェクトの型の情報も付帯されています。これはC言語の整数が値を格納するだけではなくて演算が定義されているのと同じです。

また、その次のコメントを見てみると、

```C
/* ob_item contains space for 'allocated' elements.  The number
     * currently in use is ob_size.
     * Invariants:
     *     0 <= ob_size <= allocated
     *     len(list) == ob_size
     *     ob_item == NULL implies ob_size == allocated == 0
     * list.sort() temporarily sets allocated to -1 to detect mutations.
     *
     * Items must normally not be NULL, except during construction when
     * the list is not yet visible outside the function that builds it.
     */
```

これも非常に明解で、`ob_size`は実際に使われている要素の数であって、割り当てられているメモリのサイズ`allocated`以下になる、と書かれています。`len`関数の出力は`ob_size`であるとも書かれています。

### 新規リスト作成

以下は`listobject.c`から取ったPyList_Newという新しいリストを作るCの関数です。

```C
// listobject.cより
PyObject *
PyList_New(Py_ssize_t size)
{
    if (size < 0) {
        PyErr_BadInternalCall();
        return NULL;
    }

    struct _Py_list_state *state = get_list_state();
    PyListObject *op;
#ifdef Py_DEBUG
    // PyList_New() must not be called after _PyList_Fini()
    assert(state->numfree != -1);
#endif
    if (state->numfree) {
        state->numfree--;
        op = state->free_list[state->numfree];
        _Py_NewReference((PyObject *)op);
    }
    else {
        op = PyObject_GC_New(PyListObject, &PyList_Type);
        if (op == NULL) {
            return NULL;
        }
    }
    if (size <= 0) {
        op->ob_item = NULL;
    }
    else {
        op->ob_item = (PyObject **) PyMem_Calloc(size, sizeof(PyObject *));
        if (op->ob_item == NULL) {
            Py_DECREF(op);
            return PyErr_NoMemory();
        }
    }
    Py_SET_SIZE(op, size);
    op->allocated = size;
    _PyObject_GC_TRACK(op);
    return (PyObject *) op;
}
```

こちらを見ると下から12行目くらいに

```C
op->ob_item = (PyObject **) PyMem_Calloc(size, sizeof(PyObject *));
```

と書いてありますが、ここで、Pythonオブジェクトのポインタに必要なサイズ(64bitなら8バイト)を`size`個分確保して、そのポインタ配列へのポインタを属性`ob_item`に代入しています。

オブジェクトの「サイズ」は下から5行目の

```C
 Py_SET_SIZE(op, size);
```

で設定されています。このサイズは割当メモリサイズではなく実際に格納されている要素の個数です。`Py_SET_SIZE`関数は[object.h](https://elixir.ortiz.sh/python/v3.9.0/source/Include/object.h#L142)で次のように定義されています。

```C
static inline void _Py_SET_SIZE(PyVarObject *ob, Py_ssize_t size) {
    ob->ob_size = size;
}
#define Py_SET_SIZE(ob, size) _Py_SET_SIZE(_PyVarObject_CAST(ob), size)
```

これを見ると分かるように単にオブジェクトの`ob_size`を`size`に設定しているだけです。さらに`ob_size`はというと、`PyVarObject`構造体のメンバで、同じく[object.h](https://elixir.ortiz.sh/python/v3.9.0/source/Include/object.h#L118)で定義されています。

```C
typedef struct {
    PyObject ob_base;
    Py_ssize_t ob_size; /* Number of items in variable part */
} PyVarObject;
```

### 割当メモリについて

さらに、`PyList_New`関数の下から4行目で

```C
op->allocated = size;
```

という操作によって、**allocate**された区画の数を`allocated`属性に格納しています。これは一般に`op->ob_size`と同じかより大きいですが、リストを新規作成した場合はこの２つが同じ値になっていることが分かります。言い換えると、リストの新規作成では、**余分なメモリ領域を確保しません**。講義資料本編の実験で、リストのメモリ占有量が要素の個数と線形の関係を持っていたのはそのためです。

問題は`__sizeof__`メソッドで返されるメモリサイズの方ですが、こちらは[listobject.c](https://elixir.ortiz.sh/python/v3.9.0/source/Objects/listobject.c#L2754)の`list__sizeof__impl`関数で定義されています。

```C
/*[clinic input]
list.__sizeof__
Return the size of the list in memory, in bytes.
[clinic start generated code]*/

static PyObject *
list___sizeof___impl(PyListObject *self)
/*[clinic end generated code: output=3417541f95f9a53e input=b8030a5d5ce8a187]*/
{
    Py_ssize_t res;

    res = _PyObject_SIZE(Py_TYPE(self)) + self->allocated * sizeof(void*);
    return PyLong_FromSsize_t(res);
}
```

`self->allocated * sizeof(void*)`は、割り当てられたメモリサイズですが、その他に、`_PyObject_SIZE(Py_TYPE(self)`)というのが足されています。これがリスト構造のサイズであり、オーバーヘッドに相当します。

`_PyObject_SIZE`はというと、[objimpl.h](https://elixir.ortiz.sh/python/v3.9.0/source/Include/cpython/objimpl.h#L9)で定義されています。

```C
#define _PyObject_SIZE(typeobj) ( (typeobj)->tp_basicsize )

/* _PyObject_VAR_SIZE returns the number of bytes (as size_t) allocated for a
   vrbl-size object with nitems items, exclusive of gc overhead (if any).  The
   value is rounded up to the closest multiple of sizeof(void *), in order to
   ensure that pointer fields at the end of the object are correctly aligned
   for the platform (this is of special importance for subclasses of, e.g.,
   str or int, so that pointers can be stored after the embedded data).
   Note that there's no memory wastage in doing this, as malloc has to
   return (at worst) pointer-aligned memory anyway.
*/
```

これは単に与えられたデータ型`typeobj`の基本サイズ(`tp_basicsize`)を返すだけのようです。

ここはまだ未完成なので、今後も書き足して行きます。
