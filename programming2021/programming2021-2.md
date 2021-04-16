# 第2回 VS Code/仮想環境入門

- [第2回 VS Code/仮想環境入門](#第2回-vs-code仮想環境入門)
  - [VS Code ショートカット](#vs-code-ショートカット)
  - [VS Codeの設定](#vs-codeの設定)
    - [プロキシの設定](#プロキシの設定)
    - [各種エクステンションのインストール](#各種エクステンションのインストール)
  - [VS Codeインターラクティブモード](#vs-codeインターラクティブモード)
    - [Zenモード](#zenモード)
  - [Anacondaの設定](#anacondaの設定)
    - [プロキシサーバーの設定](#プロキシサーバーの設定)
  - [Anaconda仮想環境](#anaconda仮想環境)
    - [なぜ仮想環境が必要か？](#なぜ仮想環境が必要か)
    - [仮想環境の状態チェック](#仮想環境の状態チェック)
    - [仮想環境の作成](#仮想環境の作成)
  - [VS CodeとAnacondaのインストール](#vs-codeとanacondaのインストール)
  - [VS Code以外のエディター](#vs-code以外のエディター)
    - [Emacs](#emacs)
    - [vi/vim](#vivim)

## VS Code ショートカット

VS Codeを使うに当たって、覚えたほうが良いショートカットが3つあります。

- **Ctrl+Shift+P**: コマンドパレットを開きます。VS Codeの諸々の操作は、このコマンドパレットに望みの操作に関連するキーワードを入力し、出てきた操作リストの中から望みの操作を選択するという形で行います。
- **Ctrl+Shift+X**: 拡張機能検索ウィンドウとインストール済み拡張機能の一覧を表示します。邪魔な拡張機能を無効にしたり、新しい拡張機能を探してインストールするのに使います。
- **Ctrl+,**: 設定項目検索ウィンドウを開きます。注)設定ファイルを直接編集するときは、コマンドパレットにsettings.jsonと入力してください。

その他、覚えると快適なショートカットに、

- **Ctrl+PgUp**, **Ctrl+PgDn**: タブを切り替えます。

などがあります。他にも無数のショートカットがありますので、探してみてください。

## VS Codeの設定

VS Codeは、とっつきやすくて拡張性に優れた、初心者から玄人にまで人気のあるエディターです。快適に使うために、以下の手順に従って、初期設定を行ってください。

### プロキシの設定

大学内のPCでエクステンション（拡張機能）をインストールするためには、プロキシの設定が必要です（お家のパソコンでは必要ありません）。プロキシの設定はGUIを使う方法と、設定ファイル(settings.json)に直接書き込む方法の二通りがあります。

**Ctrl+,**と叩くと、設定のための検索窓が立ち上がりますので、**proxy**と入力しましょう。すると、

```
Http: Proxy
使用するプロキシ設定。設定されていない場合は、'http_proxy' および >'https_proxy' の環境変数から継承されます。
[                                        ]
```

というproxy設定パネルが現れますので、

```
Http: Proxy
使用するプロキシ設定。設定されていない場合は、'http_proxy' および 'https_proxy' の環境変数から継承されます。
[http://proxy-server-addr:????            ]
```

のように大学のプロキシサーバーとポート番号を入力しましょう。ここで、proxy-server-addrはプロキシサーバーのアドレス、????はポート番号です(Moodleに記載してあります)。

入力できたら、設定ファイルに正しく書き込まれているか次のようにして確認しましょう。**Ctrl+Shift+P**と叩いて、コマンドパレットを開きます。**settings.json**と入力すると、幾つか候補が出てきますが、そのうち、

```
基本設定：設定(JSON)を開く
Preferences: Open Settings (JSON)
```

を選択します。すると、json形式でかかれた設定ファイル**settings.json**が開かれますので、次のように、プロキシが記載されていることを確認します。

```
{
    ...
    ...
    "http.proxy": "http://proxy-server-addr:????", 
    ...
    ...
}
```

...のところは何か色々書いてあると思いますが、プロキシの設定が見当たれば大丈夫です。

もしくは、上記のsettings.jsonを開いて、直接プロキシの行を書き込んでしまっても構いませんが、そのように直接書き込むメリットはあまり無いと思います。むしろ各種設定は、上記のsettings.jsonというjson形式のファイルに書き込まれていて、VS Codeで自由に追記・修正できるということを理解するのが重要でしょう。

### 各種エクステンションのインストール

エクステンション（拡張機能）をインストールするには、**Ctrl+Shift+X**を叩きます。現れた検索ウィンドウにエクステンション名を入力すれば、候補をリストアップしてくれますので、望みのものを選んでインストールボタンを押しましょう。

以下のエクステンションが必要ですので、インストールしましょう。

- Japanese Language Pack for VS Code (VS Codeを日本語化)
- Python (これがないと論外)
- Awesome Emacs Keymap (Emacsキーバインディング)
- Pylance (Intellisenseがうまく機能しない場合、試す価値あり)
- Path Intellisense (ファイル名パス補完)
- R (Rが実行できるようになります)
- R Tools (R用のIntellisense)
- Rainbow CSV (CSVファイルが見やすくなります)
- Edit CSV (CSVが編集できる)
- Markdown All in One (マークダウン便利ツール集)
- markdownlint (Markdownの構文チェッカー)
- Markdown PDF (MarkdownファイルをPDFやHTMLに変換)

マークダウン系のエクステンションは(文字通り)無数に存在しますので、必ずしも上記のもので無くて良いですし、より良いものがあるかもしれません。ぜひ自分に合うエクステンションを探してみてください。授業時間で欲しいエクステンションを全てインストールするのは大変だと思うので、まずはJapanese Language PackとPythonエクステンションをインストールしましょう（残りは各自インストールしておいてください）。

なお以下は授業では使いませんが、AWSなどの外部サーバーで開発を行う際に大変重宝します。リモートのファイルを直接VS Codeで編集できます。

+ Remote - SSH (外部サーバー等にSSH接続できる)

## VS Codeインターラクティブモード

それでは準備ができたので、VS Codeでプログラミングしてみましょう。Pythonのプログラミングを行うときは、インターラクティブモードという、VS Codeの内部でJupyterを起動する方法が便利です。

under construction

### Zenモード

コマンドパレットにzenと入力してZenモードを起動すると、エディター部分が全面表示になり、画面を有効に使えます。Escを押すとZenモードを終了します。

## Anacondaの設定

### プロキシサーバーの設定

Windowsスタートメニューから、Anaconda Promptを起動し、次のように入力すると、Anacondaの設定が表示されます。

```
(base) C:\Users\hoge>conda config --show
```

これだと全ての設定が表示されてしまって見にくいので、以下のようにしてproxyの設定だけ表示しましょう。

```
(base) C:\Users\hoge>conda config --show proxy_servers
proxy_servers: {}
```

上記のようにproxy_serversの項目が空欄になっていたら、プロキシが設定されていません。その場合は、以下のように順次入力してhttpとhttpsの両方にnocのプロキシサーバーを設定しましょう。

```
(base) C:\Users\hoge>conda config --set proxy_servers.http http://proxy-server-addr:????
(base) C:\Users\hoge>conda config --set proxy_servers.https http://proxy-server-addr:????
```

ここで、proxy-server.addrは正しいプロキシサーバーのアドレス(Moodleに記載)に、????は正しいポート番号に置き換えてください。

もう一度設定を表示して、プロキシが正しく設定されているか確認しましょう。

```
(base) C:\Users\hoge>conda config --show proxy_servers
proxy_servers:
  http: http://proxy-server-addr:????
  https: http://proxy-server-addr:????
```

上記の用に表示されれば正しく設定されています。

## Anaconda仮想環境

### なぜ仮想環境が必要か？

Anacondaを使うと、Pythonの仮想環境を作成することができます（Anacondaが無くてもvenvモジュールを使って作ることができます）。仮想環境とは、新しくPythonがインストールされていて、自由にパッケージのインストール・アンインストールを行うことができる自分専用の環境のことです。

Pythonでは、新しいパッケージやバージョンの異なるパッケージを試してみる場合に、仮想環境を作って試してみるのが定石です。特に、情報演習室のパソコンでは、学生も教員も管理者権限をもっていませんので、仮想環境を作らない限りパッケージを自由にインストールできません。また、Anaconda環境においても、condaではパッケージがインストールできずpipパッケージマネージャを使いたい場合があります。condaとpipを混ぜて使用するのは**危険行為**ですので、こういったことをするときは、必ず新しい仮想環境を作って行うようにしましょう。

このように、仮想環境の知識はPythonを使う上で必須ですので、今から仮想環境に慣れましょう。

### 仮想環境の状態チェック

Anacondaをインストールすると、baseという名前の仮想環境が作成され、baseに入っている状態でcondaコマンドを呼び出して新たに仮想環境を作っていくことになります。

まずは現在存在している仮想環境をcondaコマンドでチェックしておきましょう。

```
(base) C:\Users\hoge>conda env list
# conda environments:
#
base                  *  E:\ProgramData\Anaconda3
```

最初は仮想環境がbaseしか存在しないので、#のある行を除けば1行しか出力されません。アスタリスク(*)は、現在自分のいる仮想環境がbaseであることを示しており、そのあとのパスはbaseがインストールされているディレクトリを表しています。全く同じ出力は、次のようにしても得られます。

```
(base) C:\Users\hoge>conda info --envs
# conda environments:
#
base                  *  E:\ProgramData\Anaconda3
```

次に、baseにはどれだけのパッケージがインストールされているのか調べてみましょう。

```
(base) C:\Users\hoge>conda list
# packages in environment at E:\ProgramData\Anaconda3:
#
# Name                    Version                   Build  Channel
_anaconda_depends         2020.07                  py38_0
_ipyw_jlab_nb_ext_conf    0.1.0                    py38_0
alabaster                 0.7.12             pyhd3eb1b0_0
anaconda                  custom                   py38_1
anaconda-client           1.7.2                    py38_0

...（中略）...

xz                        5.2.5                h62dcd97_0
yaml                      0.2.5                he774522_0
yapf                      0.31.0             pyhd3eb1b0_0
zeromq                    4.3.3                ha925a31_3
zfp                       0.5.5                hd77b12b_6
zict                      2.0.0              pyhd3eb1b0_0
zipp                      3.4.1              pyhd3eb1b0_0
zlib                      1.2.11               h62dcd97_4
zope                      1.0                      py38_1
zope.event                4.5.0                    py38_0
zope.interface            5.3.0            py38h2bbff1b_0
zstd                      1.4.5                h04227a9_0
```

ものすごく長い出力が得られたと思いますが、これらが全て予めインストールされているパッケージです。

### 仮想環境の作成

本授業では、次の三つの仮想環境を作っておくことにします。

- env_class : 通常授業のための仮想環境
- otree5 : otree(ver.5)のための仮想環境
- otree3 : otree(ver.3)のための仮想環境

まずはAnaconda promptを起動して、既存の仮想環境を確認しておきます。

## VS CodeとAnacondaのインストール

VS CodeとAnacondaのインストール方法は、『独習Python』のセクション1.3に詳しく載っていますので、こちらを参照し、自分のパソコンや研究室のパソコンにこれらのツールをインストールしてください。課題が情報演習室でしかできないのはあまりにも不便であり、学習もはかどりません。

ただし、LinuxにはAnacondaをインストールすべきでないと筆者は考えています。Linuxではpipだけで十分にpythonのバージョン・パッケージ管理ができますし、Anacondaは経験上、X Windowシステムに致命的なダメージを及ぼす危険性があります（二度と復旧しなかった経験が2度ほどあります）。Linuxには、直接Python3をインストールし、パッケージ管理はpipモジュール(パッケージマネージャ)を用いて行うことをお勧めします。

Anacondaとの相性が良いのはWindowsですので、WindowsユーザーにはAnacondaをお勧めします。Macについては良く分かりません。

## VS Code以外のエディター

### Emacs

VS Code以外にもエディターはたくさんありますが、代表的なものはvi(vimともいう)とEmacsです。プログラミングするだけならば、VS CodeはEmacsと同程度に拡張性があり、Emacsよりも遥かに使いやすいので、VS Codeがインストールされている環境ではわざわざEmacsでコーディングする理由はないと思います。むしろ、Emacsのキーバインディングをしっかりとマスターすることが重要でしょう。その練習のためにEmacsを使ってみるのは有益だと思います。

### vi/vim

ぜひマスターしてほしいエディターはvi(vimともいう)です。こちらは、数多あるエディターの中でも最も軽快に動作するエディターであり、Linux/Unixに標準で搭載されています。標準で搭載されているので、どのマシンでもいきなり使えるという保証がありますし、何よりも動作が軽快なので、「ちょこっと」設定ファイル等を書き換えるのに大変重宝します。筆者は、Linuxの設定ファイルを編集したりするのにはviを、プログラミングにはVS CodeやEmacs、Pycharmといった重厚なエディターを使うというふうに使い分けています。Linuxをいじりだすとわかりますが、各種の設定ファイルをちょこちょこ書き換えるのにいちいちEmacsなどを立ち上げていられません。Gitでコミットする際のメッセージを編集するのにもviが軽快で便利です。viのマニュアルはネット上に溢れていますので、ぜひ試してみてください。
