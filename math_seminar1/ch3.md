# 数理セミナーI (第3回)

## VS Codeを起動しよう

VS Codeは、テキストエディタ、すなわちテキストファイルを編集するためのアプリケーションの一種です。VS Codeによるファイル編集は、原則としてディレクトリを単位として行うため、VS Codeを起動する際は、「どのディレクトリをVS Codeで開くか」を指定する必要があります。

入力例:

```bash
# ディレクトリseminar1を作成
$ mkdir seminar1
# VS Codeでディレクトリseminar1を開く
$ code seminar1
```

なお、通常ターミナルからアプリケーションを起動すると、アプリケーションを終了するまでターミナルが使えない状況になってしまいます。これを避けたい場合は、アプリケーションを起動するコマンドの後に&記号を付けます。

```bash
# VS Codeをバックグラウンドジョブとして実行
$ code seminar1 &
```

## VS Codeのショートカット

[プログラミングの資料](../programming2024/programming-2.md#vs-code-ショートカット)を参照してください。

## プロキシの設定

[プログラミングの資料](../programming2024/programming-2.md#プロキシの設定vs-code)を参照してください。

## 各種エクステンションのインストール

プロキシの設定ができましたので、各種エクステンションがインストールできます。エクステンション（拡張機能）をインストールするには、Ctrl-Shift-Xを叩きます。現れた検索ウィンドウにエクステンション名を入力すれば、候補をリストアップしてくれますので、望みのものを選んでインストールボタンを押しましょう。

本セミナーでは、最低限以下のエクステンションを入れておくと便利です。

+ Japanese Language Pack for VS Code
+ Awesome Emacs Keymap
+ Path Intellisense
+ Markdown All in One
+ markdownlint
+ Markdown Converter
+ vscode-pdf

## コマンドラインエイリアスの設定

それでは、練習として、VS Codeでコマンドラインエイリアスの設定ファイルを作成してみましょう。

入力例:

```bash
# ホームディレクトリに移動
$ cd
# VS Codeでホームディレクトリを開く
$ code . &
```

VS Code上で、`.bashrc`というファイルをホームディレクトリに作成し、次のように記述してください。

```bash
alias rm="rm -i"
alias cp="cp -i"
alias mv="mv -i"
```

記述できたら、保存しましょう。保存できたら、ターミナルを一度終了し、新しく起動してください。起動後、エイリアスが有効になっていることを確かめてください。

## Emacsキーバインドの練習

Awesome Emacs Keymapエクステンションをインストールすると、Emacsキーバインドが使用可能になります。Emacsキーバインドとは、Emacsというテキストエディタで用いられているキーバインドであり、これをマスターすれば、マウスを使わずに文書編集が可能です。超時短になりますので、必ずマスターするようにしましょう。

Emacsキーバインドの詳細は[プログラミングの資料](../programming2024/programming-2.md#emacsキーバインディング)をご覧ください。

ためしに、`/proc/cpuinfo`などのファイルをディレクトリ`seminar1`にコピーしてVS Codeで`seminar1`を開いてください。コピーしてきたファイル`cpuinfo`を開いて、慣れるまでキーバインドの挙動を試してみましょう。

## Markdownことはじめ

キーバインドに慣れてきたら、Markdown文書を作成しましょう。VS Codeでディレクトリ`seminar1`を開き、VS Code上でディレクトリ`seminar1`内に`kadai2.md`ファイルを作成してください。

Markdownの記法については、次回詳しく扱いますので、今回は、見出しの作り方だけ覚えましょう。見出しは、下記のように、ハッシュ記号を使って作成します。

```markdown
# 文書タイトル

## 見出し1

### 見出し2

#### 見出し3
```

文書は、プレビュー画面を見ながら作成しましょう。

文書ができたら、PDFに出力してください。`Ctrl-P`を入力してコマンドパレットを開き、`Markdown`と入力すると、幾つか候補が現れますので、`Markdown PDF: Export(pdf)`を選択してください。これでPDFファイルが作成されますので、ターミナルでPDFファイルが出来ているか確認してください。

PDFは、`gio open`もしくは`evince`コマンドにより閲覧することができます。

入力例:

```bash
# kadai2.pdfを開く
$ gio open kadai2.pdf
```

```bash
# kadai2.pdfを開く
$ evince kadai2.pdf
```

Markdownの本格的な文法については、[プログラミングの資料](https://kut-econ.github.io/programming2024/programming-2.html#マークダウン入門)を参照してください。

## 課題の提出

文書をPDF形式に出力できたら、Webmailを使って提出してください。
