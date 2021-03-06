# プログラミング(2022年度 3年生向け)

- [プログラミング(2022年度 3年生向け)](#プログラミング2022年度-3年生向け)
  - [授業の概要](#授業の概要)
  - [到達目標](#到達目標)
  - [授業の方法](#授業の方法)
  - [授業計画](#授業計画)
    - [第1回　プログラミング概論](#第1回プログラミング概論)
    - [第2回　VS Code/仮想環境入門](#第2回vs-code仮想環境入門)
    - [第3回　バージョン管理入門](#第3回バージョン管理入門)
    - [第4回　変数とメモリ](#第4回変数とメモリ)
    - [第5回　データ型と制御構文](#第5回データ型と制御構文)
    - [第6回　標準ライブラリ(1)―タプル、文字列、ファイル入出力](#第6回標準ライブラリ1タプル文字列ファイル入出力)
    - [第7回　標準ライブラリ(2)―辞書、集合](#第7回標準ライブラリ2辞書集合)
    - [第8回　関数とモジュール](#第8回関数とモジュール)
    - [第9回　NumPy/SciPy入門](#第9回numpyscipy入門)
    - [第10回　pandas入門](#第10回pandas入門)
    - [第11回　statsmodels入門](#第11回statsmodels入門)
    - [第12回　OOP入門](#第12回oop入門)
    - [第13回　otree入門](#第13回otree入門)
    - [第14回　ワンショットゲーム](#第14回ワンショットゲーム)
    - [第15回　繰り返しゲーム](#第15回繰り返しゲーム)
    - [第16回　期末試験](#第16回期末試験)
  - [教科書](#教科書)
    - [『独習Python』山田祥寛 著 (翔泳社, 2020年) ISBN 978-4-7981-6364-2](#独習python山田祥寛-著-翔泳社-2020年-isbn-978-4-7981-6364-2)
  - [その他](#その他)

## 授業の概要  

本講義の主要な狙いは、受講者のプログラミングに関する基礎力を向上させることである。ここでいう基礎力とは、簡単なプログラムを作るための**入門的スキル**という意味ではなく、むしろ一冊の入門書からは習得が非常に困難であるような、タイピング技術、エディターに関する深い知識、デバッガの使い方、バージョン管理、情報処理の基本的知識、文書作成技術、プログラミング言語の内部の仕組み・実装上の詳細など、すぐには役立たなくとも長期的に応用力を高める上でじわじわと効力を発揮するような**基盤となるスキル**の集合のことである。

本講義でプログラミングを学ぶために用いる主な言語はPythonである。Rを理解している受講者にとって、Pythonの理解は比較的容易であるが、同時にPythonには誰もがつまずく「落とし穴」が多い。この落とし穴は、Pythonとプログラムの仕組みがよく分かっていないと落ちてしまう落とし穴なので、**本講義ではこれを逆手にとって、この落とし穴を徹底的に研究する**ことでPythonやプログラムの仕組みを理解することを狙うというアプローチをとる。ぜひ、ゲームを作ったりツールを作ったりすることを楽しむことは趣味でやっていただくとして、本講義では、Pythonの不可解な挙動に対して「なんでやねん？」と疑問に思ってむしろその徹底解明を楽しんでほしい。Pythonは研究対象としては非常に興味深い。こうした「言語を研究する」態度もまた、付け焼き刃でないプログラミング力を養う上で有用であろう。

また本講義では、Rとの比較を通して、Pythonの特徴的な挙動に関する解説を行う。プログラミングスキルを向上させるためには、複数の言語の習得を通して、言語の設計における多様な理念に触れることが重要である。本講義であえて二つの言語を比較するのは、学習のスピードアップだけでなく、一つの言語の表面的な文法にとらわれない応用力を得ることが狙いである。

本講義のもう一つの狙いは、研究でのプログラミングの活用やAIに興味を持ち始めたばかりの学生に、汎用性に富んだPythonの世界を紹介することである。Pythonの最大の特徴は、機械学習、ウェブアプリケーション、スクレイピング、ゲーム開発、GIS（地理情報システム）など多様な分野で使われていることであり、データサイエンスに特化したRとは理念が大いに異なる。本講義では、データ分析と社会科学実験での活用を主に取り扱うが、可能な限り他の応用についても紹介する。

## 到達目標

本講義の受講者が達成すべき具体的目標は、以下の通りである。

1. 標準的なコードエディターであるVS Codeを使いこなす
2. Markdownファイルによる資料作成ができる
3. Git/GitHubを用いてアプリケーション開発ができる
4. 計算機とプログラムの原理を大まかに理解している
5. Pythonがメモリをどのように使用しているかを理解しており、その知識を用いてバグのないプログラムを作成できる
6. バグを発見し、取り除くことができる
7. Pythonを用いて基本的なデータの操作、可視化、統計解析ができる
8. OOP(オブジェクト指向プログラミング)のコンセプトを理解し、otreeを用いて簡単な実験プログラムを作成できるようになることである

注）今年度は上記の「7.統計解析」までを扱う予定です。実験プログラミングに興味が有る方は、単位を取得した後、個人的に教員にご相談ください。

## 授業の方法  

オンデマンド動画を中心として行う。対面授業も同時に開催するが、こちらは初回の講義と最終テストを除き参加任意である。学生は授業に参加して動画を視聴しても良いし、自宅で動画を視聴しても構わない。対面授業に参加する場合は**ヘッドホン**を持参すること。教員は対面授業において待機し、個別の質問に対応する。なお、資料の順序と動画の順序は一致していない。受講にあたっては、動画を基本としつつ、資料を補助的あるいは復習のために用いることを推奨する。動画には古い内容も混じっているが(この点に関しては、各動画の視聴にあたっての注意事項において気づいた点を上げておくので、動画視聴の前にチェックすること)、資料の方は常に更新しているので、双方に齟齬がある場合は資料の内容に従うこと。

## 授業計画  

### [第1回　プログラミング概論](./programming-1.md)

プログラムが動くとはどういうことか、プログラミング言語にはどのようなものがあるのか等、事前に押さえるべき必要最低限の事項を解説する。

### [第2回　VS Code/仮想環境入門](./programming-2.md)

本講義でプログラミングに用いるエディター(VS Code)の解説を行う。また、Pythonの特徴である仮想環境およびAnacondaの操作、環境設定について解説を行う。

### [第3回　バージョン管理入門](./programming-3.md)

アプリケーションやパッケージ作成の際に有用なGit/GitHubを用いたバージョン管理について解説する。

### [第4回　変数とメモリ](./programming-4.md)

変数に値を代入するということが意味するところについて、Rとの比較を通して詳細な解説を行う。その際に、ランダムアクセスメモリ(RAM)について多少のイメージを養うことが必要である。

### [第5回　データ型と制御構文](./programming-5.md)

Pythonの最も基本的なデータ構造であるリストの操作について解説する。また、Rとの比較を通して、条件分岐やループ処理などの制御構文について学ぶ。

### [第6回　標準ライブラリ(1)―タプル、文字列、ファイル入出力](./programming-6.md)

リスト以外の重要な組み込みデータ構造である文字列とタプル、そしてファイル入出力について解説する。

### [第7回　標準ライブラリ(2)―辞書、集合](./programming-7.md)

残った組み込みデータ構造である辞書と集合について解説する。

### [第8回　関数とモジュール](./programming-8.md)

現代的なプログラミングでは、既存のものを再利用するのが普通である。再利用のための代表的な道具である関数とモジュール、そしてそれらにまつわる諸概念について学ぶ。

### [第9回　NumPy/SciPy入門](./programming-9.md)

Pythonにおいて数値計算やデータ解析をするために最も重要なモジュールであるnumpyの挙動とそのメリットについて解説する。numpyを乱数シミュレーションや記述統計量の計算について学ぶ。numpyを使った科学技術計算ライブラリであるSciPyを用いて単回帰分析を実施する。

### [第10回　pandas入門](./programming-10.md)

データ操作のためのモジュールとして標準的なpandasを使ってCSVデータを読み書きし、基本的な記述統計を計算する方法について学ぶ。さらにpandasに搭載されているグラフ機能とmatplotlibモジュールを用いてデータを可視化する。

### 第11回　statsmodels入門

単回帰と重回帰を例にとり、標準的な統計モデルを納めたstatsmodelsモジュールを紹介する。また、機械学習モジュールのscikit-learnについても軽く触れる。

### 第12回　OOP入門

大規模プロジェクトや実験プログラミングに必要なオブジェクト指向プログラミング(OOP)について学ぶ。クラス、メソッド、継承、ポリモルフィズムなど鍵となる概念について解説する。

### 第13回　otree入門

Pythonで実験プログラムを作成するためのフレームワークであるotreeの解説を行う。簡単なサーベイのプログラムを作成する。

### 第14回　ワンショットゲーム

otreeを用いてワンショットゲームを作成する方法について学ぶ。

### 第15回　繰り返しゲーム

前回作成したワンショットゲームを発展させ、繰り返しゲームを作成する。また、実験の結果得られるデータの取り扱いについて解説する。最後に、これまで学んできた知識をどのように研究に活かせばよいか解説し、まとめとする。

### 第16回　期末試験

第1～15回までの内容について筆記試験を課し、理解度を評価する。

## 教科書

### [『独習Python』山田祥寛 著](https://www.amazon.co.jp/%E7%8B%AC%E7%BF%92Python-%E5%B1%B1%E7%94%B0-%E7%A5%A5%E5%AF%9B/dp/4798163643) (翔泳社, 2020年) ISBN 978-4-7981-6364-2

紙媒体の書籍は大きくて重いので、講義には持参しなくてよい。ただし、自宅に所有していることを前提に講義を進める。Kindle版もあるのでそちらも検討すること。

## その他

- [チートシート](./cheatsheet.md)
- [ちょっと細かい話](./geeks.md)(CPythonの詳細)
