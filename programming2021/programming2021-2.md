# 第2回 VS Code/仮想環境入門

## VS Codeの設定
VS Codeは、とっつきやすくて拡張性に優れた、初心者から玄人にまで人気のあるエディターです。快適に使うために、以下の手順に従って、初期設定を行ってください。

### プロキシの設定

### 各種エクステンションのインストール

エクステンション（拡張機能）をインストールするには、**Ctrl+Shift+X**を叩きます。現れた検索ウィンドウにエクステンション名を入力すれば、候補をリストアップしてくれますので、望みのものを選んでインストールボタンを押しましょう。

以下のエクステンションが必要ですので、インストールしましょう。

+ Japanese Language Pack for VS Code (VS Codeを日本語化)
+ Python (これがないと論外)
+ Awesome Emacs Keymap (Emacsキーバインディング)
+ Pylance (Intellisenseがうまく機能しない場合)
+ Path Intellisense (ファイル名パス補完)
+ R (Rが実行できるようになります)
+ R Tools (R用のIntellisense)
+ Rainbow CSV (CSVファイルが見やすくなります)
+ Edit CSV (CSVが編集できる)

以下は授業では使わないけど、大変便利です。
+ Remote - SSH (外部サーバー等にSSH接続できる)

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

- env_class : 通常授業のための仮想環境
- otree5 : otree(ver.5)のための仮想環境
- otree3 : otree(ver.3)のための仮想環境

まずはAnaconda promptを起動して、既存の仮想環境を確認しておきます。
```

```

