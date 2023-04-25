---
title: "Zennの記事をGitHub連携してVSCodeで作成させる手順③"
emoji: "📜"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["zenn","github","vscode"]
published: false
---
前回からの記事の続きになります。

@[card](https://zenn.dev/yankee/articles/zenn_works_with_github_part1)

@[card](https://zenn.dev/yankee/articles/zenn_works_with_github_part2)

# 概要

Zennでは、Qiitaにはない機能として、[GitHub連携による記事の投稿・管理](https://zenn.dev/zenn/articles/connect-to-github)が行えます。
今回は、GitHubアカウント、Zennアカウントの作成やVSCodeからの記事作成の手順について備忘録も兼ねて記事にしています。

# 開発環境

- OS：windows10 Home 22H2

# 記事の構成

以下の順で説明していきます。
本記事では**4. Gitのインストール・初期設定**について説明します。

1. GitHubアカウントの作成・初期設定　（[手順①](https://zenn.dev/yankee/articles/zenn_works_with_github_part1)で説明）
2. Zennアカウントの作成・初期設定　（[手順②](https://zenn.dev/yankee/articles/zenn_works_with_github_part2)で説明）
3. GitHubとZennの連携　（[手順②](https://zenn.dev/yankee/articles/zenn_works_with_github_part2)で説明）
4. **Gitのインストール・初期設定**　⏪本記事で説明
5. node.js(npm)のインストール
6. zenn-cliのインストール

# Gitのインストール・初期設定

この作業は過去にGitをインストールした方は不要です。
その場合は、この章は飛ばしてください。

## インストーラのダウンロード

Gitのサイトにアクセスし、`Downloads`ボタンまたは`Download for Windows`ボタンを押し、自分の環境に合ったソフトをダウンロードします。
Portable版もありますが、今回はインストーラ版をダウンロードしています。

@[card](https://git-scm.com/)

![](https://storage.googleapis.com/zenn-user-upload/64e20efb500f-20230424.png)

インストーラを実行すると、ライセンスへの同意とインストール先の指定画面が表示されますので、特に変更を希望しなければそのままどちらも**Next**をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/94dbdd0c55b1-20230424.png =500x)

![](https://storage.googleapis.com/zenn-user-upload/3a522f769029-20230424.png =500x)

## インストール時のオプション設定

この後、Gitインストール時のオプション設定になるんですが、項目がかなり多いです（しかも英語）。

オプションの選択にあたっては、こちらの記事が大変参考になりましたので、こちらの記事も併せて確認しつつ、自分に合った設定を選んでいくと良いと思います。

@[card](https://www.curict.com/item/60/60bfe0e.html)

参考に、私のオプション選択も画面キャプチャを貼っておきます（詳細は省略）。

- インストールオプション

![](https://storage.googleapis.com/zenn-user-upload/74ac382a2e21-20230424.png =500x)

- スタートメニュー登録

![](https://storage.googleapis.com/zenn-user-upload/c24a50d3ae32-20230424.png =500x)

- ⚠エディタ設定
  :::message
  今回はVSCodeでGitを使用するため、VSCodeを選択します
  :::

![](https://storage.googleapis.com/zenn-user-upload/c06a118acb72-20230424.png =500x)

- リポジトリのブランチ名

![](https://storage.googleapis.com/zenn-user-upload/f50a6e8977c6-20230424.png =500x)

- 環境変数

![](https://storage.googleapis.com/zenn-user-upload/3c355e01debc-20230424.png =500x)

- SSH設定

![](https://storage.googleapis.com/zenn-user-upload/8fc4a8baff84-20230424.png =500x)

- HTTPS設定

![](https://storage.googleapis.com/zenn-user-upload/ff28f76fc3b8-20230424.png =500x)

- 改行コード

![](https://storage.googleapis.com/zenn-user-upload/46c0885c0cc2-20230424.png =500x)

- ターミナル

![](https://storage.googleapis.com/zenn-user-upload/5936becf96f2-20230424.png =500x)

- `git pull`設定

![](https://storage.googleapis.com/zenn-user-upload/dbeca5ea0e44-20230424.png =500x)

- 認証設定

![](https://storage.googleapis.com/zenn-user-upload/5731e954f419-20230424.png =500x)

- その他オプション

![](https://storage.googleapis.com/zenn-user-upload/8d8a7e91d1bd-20230424.png =500x)

- 試験オプション

![](https://storage.googleapis.com/zenn-user-upload/330384283c28-20230424.png =500x)

ここまででオプションの選択は完了します。
`Install`ボタンをクリックすると、インストールが開始され、完了するとインストール完了画面が表示されます。

![](https://storage.googleapis.com/zenn-user-upload/ef1bf0c49e0c-20230424.png)

## 初期設定

### GitHubとの紐付け

[GitHubの初期設定時](https://zenn.dev/yankee/articles/zenn_works_with_github_part1#%E3%83%A1%E3%83%BC%E3%83%AB%E3%82%A2%E3%83%89%E3%83%AC%E3%82%B9%E3%81%AE%E9%9D%9E%E5%85%AC%E9%96%8B%E8%A8%AD%E5%AE%9A)に記載されていた、GitHub側で自動生成されたアドレスをローカルのGitに紐付ける作業を行います。

Git Bashを立ち上げ、以下のコマンドを順に実行します。
`username`はGitHub Docsの記載を見た限り、何を入力しても問題なさそうですが、今回はGitHubのユーザー名と合わせてます。

> Git は、アイデンティティによってコミットを関連付けるためにユーザ名を使います。
> Git ユーザ名は、GitHub ユーザ名と同じではありません。

@[card](https://docs.github.com/ja/get-started/getting-started-with-git/setting-your-username-in-git)

`address_issued_by_GitHub`については、GitHub側で自動生成されたアドレスを入力します。

```bash
git config --global user.name "username"
git config --global user.email "address_issued_by_GitHub"
```

コマンド入力後、続けて以下のコマンドを入力して、ユーザー名、メールアドレスが正しく反映されていることを確認します。
また、`core.editor`には、インストール時のエディタ設定で選択したエディタソフトが選択されていることを確認します。

```bash
git config --global -l
// 出力結果
core.editor==*******************
user.name==*******************
user.email=*******************
```

### VSCodeでのGit設定

先ほどはGit Bashからコマンドを実行していましたが、VSCodeのターミナルからもGitを起動できるので、今後はそちらを使います。

なお、本記事ではVSCodeのインストールは既に済んでいる前提ですので、未インストールの方は別途VSCodeをインストールください。
VSCodeを起動し、画面右上にある画面分割（パネル切り替え）ボタンをクリックします。

![](https://storage.googleapis.com/zenn-user-upload/ac074c41e4f6-20230424.png =500x)

すると、画面下にターミナル画面が出ますので、右側の**＋ボタン右にある下矢印ボタン**をクリックして、Git Bashをクリックします。

![](https://storage.googleapis.com/zenn-user-upload/91b1dc2a72c9-20230424.png =500x)

ターミナル画面が追加され、bashの方でGitコマンドが実行できます。
なお、デフォルトのターミナルをPower ShellからGit Bashに変更することも可能ですので、
必要に応じて設定を変更ください（設定方法は省略）。

![](https://storage.googleapis.com/zenn-user-upload/b4b69a56c1d9-20230424.png)

### GitHub上のリポジトリのローカルへのクローン

GitHub上で作成したZennコンテンツ用のリポジトリをローカルにクローンします。
GitHub上から、クローンしたいリポジトリのページに行き、HTTPSを選択し、コピーボタンをクリックします。

![](https://storage.googleapis.com/zenn-user-upload/be79d61f8cfa-20230424.png)

VSCode上のGit Bashで、ローカルリポジトリを作成するフォルダに移動し、以下のコマンドを実行します。

```bash
git clone https://github.com/************.git
```

その後、ローカルにGitHub上と同じ名前のフォルダが作成できていれば問題ありません。
