# 第7回　関数とモジュール

## 名前空間

第4回「変数とメモリ」において、変数がオブジェクトに貼り付けられたラベルであるという話をしました。オブジェクトはメモリ上のある領域に格納されていることはすでに説明しました。一方、ラベルである「変数名」の方は、あるディクショナリのキーとして保存されています。

Pythonプログラムが実行されると、Pythonは、ある特別な辞書を作成します。これは、実行中のプログラムにおける変数名をキーとし、その変数名が指すオブジェクトを値とする辞書です。この辞書のことを、**グローバル名前空間**と呼ぶことがあります。グローバル名前空間はビルトイン関数globals()の戻り値として得られます。

```python
>>> globals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>}
```

この出力を見ると、すでにPythonが幾つかの変数を定義ずみであることがわかります。たとえば__name__という変数は__main__という文字列として定義されています。

```python
>>> print(__name__)
__main__
```

注)__name__変数の意味は後で説明します。

さて、グローバル名前空間は、どのような変数が定義されているかをPythonに教えるために存在しています。ためしにxという変数を定義して、実際にそれがグローバル名前空間に追加されることを確認しましょう。

```python
>>> x = 1
>>> globals()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'x': 1}
```

逆に、グローバル名前空間辞書に新たなキー：値ペアを追加することで、変数が定義されるかどうか試してみましょう。

```python
>>> globals().update({'y':2})
>>> y
2
```

このように、変数を定義するということは、グローバル名前空間に新たなキー：値ペアを追加することを意味します。

たとえばprint(x)というコードを実行すると、Pythonは、globals()名前空間を検索して、キー'x'に対応する値である整数オブジェクト1を発見し、それを印字するということをしています。このように名前空間が存在するおかげで、Pythonは、変数名とオブジェクトを対応づけることができます。

## 関数とローカル名前空間

それぞれの関数は、固有の名前空間をもっています。これを、ローカル名前空間とよびます。ローカル名前空間は、locals()関数によって出力することができます。

```python
>>> def f():
...     print(locals())
... 
>>> f()
{}
```

上記の出力から分かるように、関数の中で何も定義しない場合、locals()の出力はからっぽです。関数の中で変数を定義すると、ローカル名前空間に要素が追加されます。

```python
>>> def f():
...     x = 234
...     print(locals())
... 
>>> f()
{'x': 234}
```

ローカル名前空間は**辞書ではない**ことに注意してください。locals()関数は、ローカル名前空間を辞書のフォーマットにして返すだけで、ローカル名前空間そのものを返すわけではありません。

ローカル名前空間は、関数が呼び出されている間だけしか存続せず、関数の外からはアクセスすることができません。

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

グローバル名前空間に登録された変数をグローバル変数、ローカル名前空間に登録された変数をローカル変数と呼びます。

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
>>> locals() is globals()
True
```

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
