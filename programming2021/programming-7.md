# 第7回　関数とモジュール

## 名前空間

第4回「変数とメモリ」において、変数がオブジェクトに貼り付けられたラベルであるという話をしました。鋭い受講者の中には、「それでは変数名（ラベル）自体はどのような形でメモリ上に存在するのか」という疑問をもった方がおられるかもしれません。実は変数名はPythonのディクショナリのキーとして保存されています。キーは名前空間が保持するハッシュテーブルの中に保存されているC言語の文字列ですので、オブジェクトではありません。つまり、重要なことですが、**変数名はオブジェクトではありません**。

Pythonプログラムが実行されると、Pythonは、**名前空間**と呼ばれる特別な辞書を作成します。これは、実行中のプログラムにおける変数名をキーとし、その変数名が指すオブジェクトを値とする辞書です。名前空間はビルトイン関数locals()の戻り値として得られます。

```python
>>> locals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>}
```

この出力を見ると、すでにPythonが幾つかの変数を定義ずみであることがわかります。たとえば__name__という変数は__main__という文字列として定義されています。

```python
>>> print(__name__)
__main__
```

注)__name__変数の意味は後で説明します。

あとから使いやすいように、名前空間をmain_nsという変数に代入しておきましょう。

```python
>>> main_ns = locals()
>>> main_ns
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'main_ns': {...}}
```

main_nsの内容をよく見てみると、最後に'main_ns'というキーが追加されていることがわかります。これは、main_nsという変数が定義されたことを表しています。そしてその値はちょっと奇妙ですが、{...}というものになっています。この{...}は、main_ns(が指す辞書オブジェクト)自身を表しています。Pythonでは、辞書やリストが自分自身を要素として含むとき、{...}や[...]のように表記されることを覚えておきましょう。

さて、このmain_nsという変数に代入した辞書は、どのような変数が定義されているかをPythonに教えるために存在しています。ためしにxという変数を定義して、実際にそれがmain_nsに追加されることを確認しましょう。

```python
>>> x = 1
>>> main_ns
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'main_ns': {...}, 'x': 1}
```

逆に、main_nsに新たなキー：値ペアを追加することで、変数が定義されるかどうか試してみましょう。

```python
>>> main_ns.update({'y':2})
>>> y
2
```

このように、変数を定義するということは、名前空間に新たなキー：値ペアを追加することを意味します。言い換えると、x=1というコードは、locals()['x'] = 1の省略記法であると言って良いです。

たとえばprint(x)というコードを実行すると、Pythonは、名前空間を検索して、キー'x'に対応する値である整数オブジェクト1を発見し、それを印字するということをしています。このように名前空間が存在するおかげで、Pythonは、変数名とオブジェクトを対応づけることができます。辞書を理解することが、Pythonの変数名管理を理解することにつながっているのです。

## 関数とローカル名前空間

次に関数を作って、関数内の名前空間がどうなっているか調べましょう。

```python
>>> def f():
...     print(locals())
... 
>>> f()
{}
```

上記の出力から分かるように、関数の中ではlocals()の出力はからっぽです。これは、関数が独自の名前空間を持っていることを表しています。これを、ローカル名前空間と呼びます。関数内で変数に代入を行うと、ローカル名前空間に変数が登録されます。

```python
>>> def f():
...     x = 234
...     print(locals())
... 
>>> f()
{'x': 234}
```

ローカル名前空間は、関数が呼び出されている間だけしか存続せず、関数の外からアクセスすることができません。

```python
>>> def f():
...     x = 234
... 
>>> f()
>>> print(x)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'x' is not defined
>>> 
```

ローカル名前空間に対して、関数の外で定義される変数が登録される名前空間をグローバル名前空間と呼びます。グローバル名前空間に登録された変数をグローバル変数、ローカル名前空間に登録された変数をローカル変数と呼びます。

|定義される場所|登録される名前空間|変数の呼び名|
|---|---|---|
|関数の外|グローバル名前空間|グローバル変数|
|関数の中|ローカル名前空間|ローカル変数|

関数の中でグローバル名前空間を表示するには、globals()関数を呼び出します。

```python
>>> def f():
...     print(locals())
...     print(globals())
... 
>>> f()
{}
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'f': <function f at 0x7fadb2500bf8>}
```

関数の外では、locals()の出力はglobals()と同じであり、どちらもグローバル名前空間であることに注意してください。

```python
>>> globals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>}
>>> locals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>}
>>> locals() == globals()
True
```

under construction...

## モジュールの作成とインポート

**モジュール**という言葉には難しい意味合いはなく、「実行可能なPythonのファイル」とほとんど同じ意味です。とくに、別のPythonプログラムからインポートされる想定で作られたPythonファイルをモジュールと言うことが多いようです。それではまず、my_moduleという名前の空のモジュールを作ってみましょう。my_module.pyという名前のファイルを作って次の内容を保存しておきましょう。

```python
# my_moduleの中身
x = 123
```

次にこれを読み込みます。

```python
>>> import my_module
>>> print(my_module.x)
123
```

このように、モジュールを読み込むと、モジュール内で
