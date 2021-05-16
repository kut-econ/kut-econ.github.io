# 第3回 バージョン管理入門

- [第3回 バージョン管理入門](#第3回-バージョン管理入門)
  - [GitHubアカウントの作成](#githubアカウントの作成)
  - [課題遂行に用いる主なGitコマンド](#課題遂行に用いる主なgitコマンド)
  - [git bashの起動](#git-bashの起動)

## GitHubアカウントの作成

GitHubを利用するには、まずGitHubのサイトでユーザー登録をしてアカウントを作成する必要があります。以下のような方は、必ず新たにアカウントを作成してください。

- GitHubアカウントを持っていない人
- GitHubアカウントを持っているが、大学以外のメールアドレスでカウントを作成した人

大学のメールアドレスで作成したGitHubアカウントをお持ちの方は、新たに作成する必要はありません。

インターネットブラウザで[GitHub](https://github.com/)のサイトに行き、画面右上の"Sign up"をクリックします。

"Create your account"という画面になりますので、以下の項目を入力します。

   1. ユーザー名
   2. Emailアドレス(**必ず大学のアドレスを入力**)
   3. パスワード(紛失しないよう厳重に管理すること)

ユーザーネームを付ける際には、以下のルールに従ってください。例えば学籍番号1234567の山田太郎さんの場合、ユーザーネームは

yamada-taro-1234567

のように、(ローマ字姓)-(ローマ字名)-(学籍番号)としてください。**必ず全て半角文字にしてください**。既存のアカウントを持っている人は事前にユーザー名を教えてください(ユーザー名の変更は必要ありません)。

![create_account_github](img/create_account_github.png)

ユーザー名等の入力を終えたら、"Verify your account"の項目でロボットでないことを証明し、"Creat account"をクリックします。

"Welcome to GitHub"というページになりますので、以下のように入力してください。

What kind of work do you do, mainly?はStudentを選択してください。

![welcome_github1](img/welcome_github1.png)

How much programming experience do you have?はA littleなどご自身のプログラミング経験のレベルにあったものを選択してください。

![welcome_github2](img/welcome_github2.png)

What do you plant to use GitHub for?については、Learn to code、Learn Git and GitHub、School work and student projectsなどを選択しておけば良いでしょう。(3つまで選択可)

![welcome_github3](img/welcome_github3.png)

I am interested inのところは、pythonと入力し、"Complete setup"をクリックします。

![welcome_github4](img/welcome_github4.png)

"Please verify your email address"という画面になったら無事アカウント作成に成功です。

![github_please_verify](img/github_please_verify.png)

アカウント作成の後、認証作業が必要になります。登録した大学のEmailにGitHubから"Please verify your email address"という件名のメールが来ているはずですので、内容を確認してください。"Verify email address"というボタンがあるはずなので、これをクリックします。

インターネットブラウザが起動し、"What do you want to do first?"というページになりますので、一番下の"Skip this for now"をクリックしてください。これでアカウント作成・認証とも完了です。いつでもGitHubが使える状態になりました。

![github_what_do_you](img/github_what_do_you.png)

今後GitHubにログインするときは、GitHubのページの右上の"Sign in"をクリックしてユーザー名とパスワードを入力してください。

## 課題遂行に用いる主なGitコマンド

GitとGitHubには様々な機能が備わっていますが、それらを全て1回の講義で説明するのは不可能です。そこで、まずは皆さんが今後の講義を受講するにあたって最低限必要になる機能に絞って解説をすることにします。

皆さんがこの授業でGitとGitHubを使用する主な目的と、それに対応するGitコマンドは以下の通りです。

|目的|使用するGitコマンド|
|--|--|
|課題のダウンロード|clone, fetch, status, pull|
|課題の遂行|add, commit, reset, statusなど|
|課題のアップロード|fetch, status, push|

以下、これらのコマンドを一つずつ説明しましょう。

## git bashの起動

