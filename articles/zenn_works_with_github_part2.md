---
title: "Zennの記事をGitHub連携してVSCodeで作成させる手順②"
emoji: "📜"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["zenn","github","vscode"]
published: false
---
前回からの記事の続きになります。

# 概要

Zennでは、Qiitaにはない機能として、[GitHub連携による記事の投稿・管理](https://zenn.dev/zenn/articles/connect-to-github)が行えます。
今回は、GitHubアカウント、Zennアカウントの作成やVSCodeからの記事作成の手順について備忘録も兼ねて記事にしています。

# 開発環境

- OS：windows10 Home 22H2

# 記事の構成

以下の順で説明していきます。
なお、思ってたより記事の分量が多かったため、本記事では**1. GitHubアカウントの作成・初期設定**までとし、それ以降は次の記事に引き継ぐ形としています。

1. GitHubアカウントの作成・初期設定　（[手順①](https://zenn.dev/yankee/articles/zenn_works_with_github_part1)で説明）
2. **Zennアカウントの作成・初期設定**　⏪本記事で説明
3. **GitHubとZennの連携**　⏪本記事で説明
4. Gitのインストール・初期設定
5. node.js(npm)のインストール
6. zenn-cliのインストール

# Zennアカウントの作成・初期設定

## アカウント作成

まず、Zennのトップページに入り、ページ下部にある`Join Zenn 今すぐはじめる`ボタンを押します。

@[card](https://zenn.dev/)

![](https://storage.googleapis.com/zenn-user-upload/cdf90ae173f6-20230424.png)

すると、`Login with Google`ボタンが出るため、このボタンを押して、Googleアカウントでログインします。

:::message
このタイミングで知りましたが、ZennはGoogleアカウントでしかログインできないようです。
もしGoogleアカウントを持っていない場合はGoogleアカウントを新規で作成してください。
:::

![](https://storage.googleapis.com/zenn-user-upload/b4f5d22baf88-20230424.png)

Googleアカウントでログイン後、ユーザー名／表示名を入力して、**次へ進む**ボタンを押します。
※ユーザー名は後から変更ができないので注意

![](https://storage.googleapis.com/zenn-user-upload/fcbffe62c800-20230424.png =500x)

必要に応じてプロフィール紹介を記入して、**Zennをはじめる**ボタンを押せばZennアカウントの作成が完了します。

![](https://storage.googleapis.com/zenn-user-upload/0f11889b9640-20230424.png =300x)

![](https://storage.googleapis.com/zenn-user-upload/8b2eb6b4b53d-20230424.png =250x)

## 初期設定

### アカウント設定

Zennトップページ上の右上にある自分のアイコンをクリックし、**アカウント設定**をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/ea44a75bc113-20230424.png =200x)

アカウント設定上の**メール通知**の項目は必要に応じてチェックを外します（初期設定は全部有効）。
**プロフィール設定**メニューでは、表示名の変更やGitHubユーザー名の設定が可能です。
なお、ここでGitHubユーザー名を入力しなくてもリポジトリ連携は行えました。

![](https://storage.googleapis.com/zenn-user-upload/0138e149a9bd-20230424.png)

# GitHubリポジトリ連携

次に、作成したGitHubアカウントのリポジトリとZennアカウントを連携していきます。

先ほどと同じく、Zennトップページ上の右上にある自分のアイコンをクリックし今回は**GitHubからのデプロイ**をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/ea44a75bc113-20230424.png =200x)

初めて、リポジトリを連携する場合は下の画面が表示されるので、**リポジトリを連携する**ボタンをクリックします。

![](https://storage.googleapis.com/zenn-user-upload/a10e113478e0-20230424.png)

リポジトリ連携範囲は`Only select repositories`を選択し、リポジトリ名には、
[GitHubの初期設定時](https://zenn.dev/yankee/articles/zenn_works_with_github_part1#zenn%E7%94%A8%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E4%BD%9C%E6%88%90)に入力したリポジトリ名を転記します。

`Install & Authorize`ボタンを押すと、GitHubのパスワード入力画面が表示されますので、設定したパスワードを入力します。

![](https://storage.googleapis.com/zenn-user-upload/7a0e03bb4e88-20230424.png =500x)

![](https://storage.googleapis.com/zenn-user-upload/f0e7bddabc1e-20230424.png)

ZennのGitHub画面上に、✅リポジトリと連携中　の画面が表示されれば連携完了です。

![](https://storage.googleapis.com/zenn-user-upload/6291d9797320-20230424.png)
