# チートシート

- [チートシート](#チートシート)
  - [matplotlib](#matplotlib)
    - [フォント一覧の取得](#フォント一覧の取得)
    - [設定ファイルの場所](#設定ファイルの場所)
    - [設定ファイルの書き方](#設定ファイルの書き方)

## matplotlib

### フォント一覧の取得

フォントマネージャの`get_fontconfig_conts`関数を実行することで、自分の環境で使用可能なフォント名の一覧のリスト`font_names`が得られます。色々なサイトで解説されているかと思いますが、例えば[こちら](http://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=python:matplotlib:%E3%83%95%E3%82%A9%E3%83%B3%E3%83%88%E3%81%AE%E8%A8%AD%E5%AE%9A)からいただいたコードは次のようになります。

```python
# %%
import matplotlib.font_manager as fm
flist = fm.get_fontconfig_fonts()
fnames = [fm.FontProperties(fname=name).get_name() for name in flist]
```

なお、筆者のUbuntu 18.04では、`NotoColorEmoji.ttf`フォントが`get_name`でエラーを出して上のコードがうまく行かなかったので、上記の`flist`からこのフォントだけを排除しなくてはなりませんでした。

[font_manager](https://matplotlib.org/stable/api/font_manager_api.html)はまだ不勉強なので、誰か原因が分かる人がいたら教えてください。

### 設定ファイルの場所

matplotlibの設定ファイルの場所は、

```python
# %%
matplotlib.matplotlib_fname()
```

で取得できます。`base`環境だと、管理者しか編集できないと思います。

### 設定ファイルの書き方

`font.family`が書かれた行を探して`#`を消してコメントインします。

```python
font.faimly = 'Meiryo'
```

といったように、日本語フォントに変えればよいです。

Linuxでは[こちらの説明](https://blank-oldstranger.com/2018/11/08/matplotlib-japanese/)などを参考に日本語フォントをインストールしてから、IPAexGothicなどにフォントを設定していただければよろしいです。
