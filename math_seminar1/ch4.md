# LaTeXを用いた数式の記述

- [LaTeXを用いた数式の記述](#latexを用いた数式の記述)
  - [Markdownに数式を書く](#markdownに数式を書く)
  - [ローカルコンピュータでLaTeXを使う](#ローカルコンピュータでlatexを使う)
  - [Overleafで数式の入った文書を作成する](#overleafで数式の入った文書を作成する)

## Markdownに数式を書く

Markdownファイルには数式を挿入することができます。その方法については、[矢内先生の資料](https://yukiyanai.github.io/mathseminar1/latex.html)が詳しいです。

## ローカルコンピュータでLaTeXを使う

WindowsにLaTeXをインストールして使うのはかなり面倒です。Linuxの良いところは、面倒な設定をしなくてもすぐにLaTeXが使えることです。

適当なディレクトリを作って、vscodeで開き、ディレクトリ内にテキストファイルを作りましょう。ファイル名は`test.tex`とします。このような`.tex`拡張子をもつテキストファイルを**tex(テフ)ファイル**と呼びます。ファイルの中に次のように記述しましょう。

```latex
\documentclass{jarticle}
\begin{document}
オイラーの等式
$$
e^{i\pi} + 1 = 0
$$
\end{document}
```

ファイルを保存したら、ターミナルで当該のディレクトリに移動し、次のように入力してtexファイルを**コンパイル**します。通常LaTeXではコンパイルに`latex`というコマンドを使いますが、日本語ファイルをコンパイルする際は、かわりに`platex`というコマンドを用います。

```bash
platex test
```

もしくは

```bash
platex test.tex
```

でも構いません。実行すると、ディレクトリ内に`test.dvi`というファイルができます。環境にも依存しますが、`xdvik-ja`というパッケージがLinuxにインストールされていれば、次のようにしてdviファイルを表示できます。

```bash
xdvi test.dvi
```

しかし環境によっては、日本語が含まれているdviファイルを表示できない場合もあります。そのような場合は、次のようにしてdviファイルをpdfファイルに変換しましょう。

```bash
dvipdfmx test.dvi
```

これで`test.pdf`というpdfファイルが作成されます。pdfファイルは次のようにして閲覧できます。

```bash
gio open test.pdf
```

もしくは

```bash
evince test.pdf
```

でも良いです。

LaTeXでどのように複雑な数式を作るかは、次回詳しく学ぶことにしましょう。

## Overleafで数式の入った文書を作成する

overleafはインターネット上でLaTeX文書を作成、共有、コンパイルすることができる非常に便利なサービスです。overleafの設定等については[矢内先生の資料](https://yukiyanai.github.io/mathseminar1/overleaf.html)に詳しいです。無料アカウントでも、一人で文書を作成する分にはほとんど不自由ありませんので、早速アカウントを作成しましょう。

overleafはデフォルトの状態では日本語を処理することができません。日本語を処理する方法については、[こちら](https://zenn.dev/daisuke23/articles/overleaf-japanese)のサイトが参考になります。
