# ちょっと細かいはなし

## CPythonのリストのメモリ利用

CPythonのリストは[listobject.h](https://github.com/python/cpython/blob/main/Include/cpython/listobject.h)と[listobject.c](https://github.com/python/cpython/blob/main/Objects/listobject.c)で実装されています。

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

と書いてありますが、ここで、Pythonオブジェクトのポインタに必要なサイズ(64bitなら8バイト)を`size`個分確保して、そのポインタ配列へのポインタを`ob_item`に代入しています。

ここはまだ未完成なので、今後も書き足して行きます。
