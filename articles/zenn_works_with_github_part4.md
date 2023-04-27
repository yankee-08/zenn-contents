---
title: "Zennの記事をGitHub連携してVSCodeで作成させる手順④　Node.js(npm)、Zenn-CLIのインストール"
emoji: "📜"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["zenn","github","vscode","npm","bash"]
published: false
---
前回からの記事の続きになります。

@[card](https://zenn.dev/yankee/articles/zenn_works_with_github_part1)

@[card](https://zenn.dev/yankee/articles/zenn_works_with_github_part2)

@[card](https://zenn.dev/yankee/articles/zenn_works_with_github_part3)

# 概要

Zennでは、Qiitaにはない機能として、[GitHub連携による記事の投稿・管理](https://zenn.dev/zenn/articles/connect-to-github)が行えます。
今回は、GitHubアカウント、Zennアカウントの作成やVSCodeからの記事作成の手順について備忘録も兼ねて記事にしています。

# 開発環境

- OS：windows10 Home 22H2

# 記事の構成

以下の順で説明していきます。
本記事では**5. node.js(npm)のインストール**以降を説明します。

1. GitHubアカウントの作成・初期設定　（[手順①](https://zenn.dev/yankee/articles/zenn_works_with_github_part1)で説明）
2. Zennアカウントの作成・初期設定　（[手順②](https://zenn.dev/yankee/articles/zenn_works_with_github_part2)で説明）
3. GitHubとZennの連携　（[手順②](https://zenn.dev/yankee/articles/zenn_works_with_github_part2)で説明）
4. Gitのインストール・初期設定　（[手順③](https://zenn.dev/yankee/articles/zenn_works_with_github_part3)で説明）
5. **Node.js(npm)のインストール**　⏪本記事で説明
6. **Zenn CLIのインストール**　⏪本記事で説明

# Node.js(npm)のインストール

## インストーラのダウンロード

今回、Node.jsのインストールには、以下のサイトを参考にして、**NVM for Windows**からインストールす形としました。

@[card](https://learn.microsoft.com/ja-jp/windows/dev-environment/javascript/nodejs-on-windows)

**NVM for Windows**はGitHubの専用ページからダウンロードできます。

@[card](https://github.com/coreybutler/nvm-windows#installation--upgrades)

:::details Node.jsを直接インストールする場合
Node.jsのサイトから直接ダウンロード・インストールすることも可能です。
その場合は以下のサイトからダウンロードしてください。

@[card](https://nodejs.org/ja)

:::

ページ内の`README.md`内にある**Install nvm-windows**の項目から、最新バージョンのインストール画面に進みます。
ファイル一覧の中から、`nvm-setup.zip`をダウンロード・解凍して実行します。

![](https://storage.googleapis.com/zenn-user-upload/5a34d17683ad-20230425.png)

## インストール作業

インストーラを実行し、ライセンス条項への同意、インストール先の指定、シンボリックリンクの設定を順に行っていきます。
特に、理由がなければデフォルトの設定で問題ないと思います。

![](https://storage.googleapis.com/zenn-user-upload/ea582f8ade76-20230425.png =400x)

![](https://storage.googleapis.com/zenn-user-upload/dc99e17cfc25-20230425.png =400x)

![](https://storage.googleapis.com/zenn-user-upload/bb70f372e510-20230425.png =400x)

最後にインストール完了画面が表示されてインストール完了です。

![](https://storage.googleapis.com/zenn-user-upload/81cfb5cce151-20230425.png =400x)

このあと、Git Bash上で`nvm`コマンドが実行できるようになります。
インストールが完了していることを確認する場合、version取得コマンドなどが通ればOKです。

```bash
nvm version 
1.1.11
```

:::message
自分の環境の場合、VSCode上でBashを実行していたためか、VSCodeを再起動しないと`nvm`コマンドが認識されませんでした。
:::

次に、インストール可能なnode.jsのバージョンを確認するため、以下のコマンドを実行します。

```bash
nvm list available
```

![](https://storage.googleapis.com/zenn-user-upload/b54f671a5e09-20230425.png =400x)

今回は、LTSバージョンの最新である`18.16.0`をインストールしています。

```bash
nvm install 18.16.0
```

![](https://storage.googleapis.com/zenn-user-upload/fda9e74e3057-20230425.png =400x)

インストール完了後、有効にするnode.jsのバージョンを選択し、npmコマンドが実行できれば問題ありません。

```bash
nvm use 18.16.0
```

![](https://storage.googleapis.com/zenn-user-upload/e44f0deee4f2-20230425.png)

```bash
npm -v
9.5.1
```

# Zenn CLIのインストール

最後に、コンテンツのプレビュー等に使用するため、**Zenn CLI**をインストールしていきます。
基本は、公式の手順通りです。

@[card](https://zenn.dev/zenn/articles/install-zenn-cli)

まず、**Git Bash上でZennのコンテンツを管理するディレクトリに移動**した後、以下コマンドを実行します。

```bash
npm init --yes
npm install zenn-cli
```

コマンド実行後、ディレクトリ上に`zenn-cli`のフォルダが作成されます。
その後、以下の`npx`コマンドを実行します。
コマンドが正しく動作すれば、下の画像のように出力されます。

:::message alert
`npx`コマンドの実行場所を誤るとGitで正しく認識されません。
自分はそこでハマりました・・・
`git clone`コマンド実行後に作成されたフォルダの直下でコマンドを実行してください。
:::

```bash
npx zenn init
```

![](https://storage.googleapis.com/zenn-user-upload/6c28dd75b637-20230425.png)

これで一通りの準備は完了です。
記事の作成の仕方は以下のZenn公式ページが参考になるかと思いますが、以下のコマンドを実行すると記事用のテンプレートファイルが作成されます（ファイル名は変更して問題ありません）。

@[card](https://zenn.dev/zenn/articles/zenn-cli-guide)

```bash
npx zenn new:article
```

![](https://storage.googleapis.com/zenn-user-upload/3ccc0204a46c-20230425.png)

![](https://storage.googleapis.com/zenn-user-upload/a6cc46c42133-20230425.png)

その後、以下のコマンドを実行すると、ローカルにサーバが立ち上がり、記事のプレビューが閲覧できるようになります。
※ポート番号を変えなければ、下のリンクをクリックすればいけるはずです（ポート番号が競合する場合は変更することも可能）。

```bash
npx zenn preview
```

@[card](http://localhost:8000)

プレビューサイトには、記事を作成する上でのTipsがまとまったサイトのリンクもあるので、まずはプレビューを起動しながら記事を作成していく方が効率的かと思います。

# おわりに

おもいのほか記事のボリュームが多く、4つの記事に分ける形となってしまいましたが、これでひとまず記事は終了となります。
自分が作成した記事以外にも公式記事含め、参考リンクとして載せております。
自分の記事も誰かが環境構築する際の参考になればと思います。

以上
