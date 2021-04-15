# 第2回 VS Code/仮想環境入門

- [第2回 VS Code/仮想環境入門](#第2回-vs-code仮想環境入門)
  - [VS Code ショートカット](#vs-code-ショートカット)
  - [VS Codeの設定](#vs-codeの設定)
    - [プロキシの設定](#プロキシの設定)
    - [各種エクステンションのインストール](#各種エクステンションのインストール)
  - [その他 VS Codeの便利な使い方](#その他-vs-codeの便利な使い方)
    - [Zenモード](#zenモード)
  - [Anacondaの設定](#anacondaの設定)
    - [プロキシサーバーの設定](#プロキシサーバーの設定)
    - [仮想環境の作成](#仮想環境の作成)

## VS Code ショートカット

VS Codeを使うに当たって、覚えたほうが良いショートカットが3つあります。

+ **Ctrl+Shift+P**: コマンドパレットを開きます。VS Codeの諸々の操作は、このコマンドパレットに望みの操作に関連するキーワードを入力し、出てきた操作リストの中から望みの操作を選択するという形で行います。
+ **Ctrl+Shift+X**: 拡張機能検索ウィンドウとインストール済み拡張機能の一覧を表示します。邪魔な拡張機能を無効にしたり、新しい拡張機能を探してインストールするのに使います。
+ **Ctrl+,**: 設定項目検索ウィンドウを開きます。注)設定ファイルを直接編集するときは、コマンドパレットにsettings.jsonと入力してください。

その他、覚えると快適なショートカットに、

+ **Ctrl+PgUp**, **Ctrl+PgDn**: タブを切り替えます。

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

+ Japanese Language Pack for VS Code (VS Codeを日本語化)
+ Python (これがないと論外)
+ Awesome Emacs Keymap (Emacsキーバインディング)
+ Pylance (Intellisenseがうまく機能しない場合、試す価値あり)
+ Path Intellisense (ファイル名パス補完)
+ R (Rが実行できるようになります)
+ R Tools (R用のIntellisense)
+ Rainbow CSV (CSVファイルが見やすくなります)
+ Edit CSV (CSVが編集できる)
+ markdownlint (Markdownの構文チェッカー)

以下は授業では使いませんが、AWSなどの外部サーバーで開発を行う際に大変重宝します。リモートのファイルを直接VS Codeで編集できます。

+ Remote - SSH (外部サーバー等にSSH接続できる)

## その他 VS Codeの便利な使い方

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

### 仮想環境の作成

Pythonでは、用途に合わせて仮想環境を作るのが定石です。特に、情報演習室のパソコンでは、仮想環境を作らない限りパッケージを自由にインストールできません。よって、今から仮想環境に慣れましょう。仮想環境はPythonの標準機能ですが、Anacondaを使う場合は、以下の説明に従って、必ずcondaコマンドで仮想環境を作るようにしてください。

本授業では、次の三つの仮想環境を作っておくことにします。

+ env_class : 通常授業のための仮想環境
+ otree5 : otree(ver.5)のための仮想環境
+ otree3 : otree(ver.3)のための仮想環境

まずはAnaconda promptを起動して、既存の仮想環境を確認しておきます。
