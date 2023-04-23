---
title: "Zennの記事をGitHub連携してVSCodeで作成させる手順①"
emoji: "📜"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["zenn","github","vscode"]
published: true
---
今まで、技術情報は[Qiita](https://qiita.com/yankee)に挙げていたのですが、今回GitHubのアカウントを作成するついでにZennのアカウントも作成してみました。
最初の記事として、Zennに記事をあげる環境構築について投稿してみます。

# 概要

Zennでは、Qiitaにはない機能として、[GitHub連携による記事の投稿・管理](https://zenn.dev/zenn/articles/connect-to-github)が行えます。
今回は、GitHubアカウント、Zennアカウントの作成やVSCodeからの記事作成の手順について備忘録も兼ねて記事にしています。

# 開発環境

- OS：windows10 Home 22H2

# 記事の構成

以下の順で説明していきます。
なお、思ってたより記事の分量が多かったため、本記事では**1. GitHubアカウントの作成・初期設定**までとし、それ以降は次の記事に引き継ぐ形としています。

1. **GitHubアカウントの作成・初期設定**
2. Zennアカウントの作成・初期設定
3. GitHubとZennの連携
4. Gitのインストール・初期設定
5. node.js(npm)のインストール
6. zenn-cliのインストール

# GitHubアカウントの作成・初期設定

GitHubとZennのアカウント作成順序はどちらが先で問題ありませんが、
今回はGitHubから作りました。

## アカウント作成

まず、GitHubのトップページから`Sign up`ボタンを押します。

https://github.com/

![](https://storage.googleapis.com/zenn-user-upload/a369679b48ff-20230423.png)

email入力画面に続き、password、username画面を順に入力します。
usernameが利用可能になるとContinueボタンが押せるようになります。

![](https://storage.googleapis.com/zenn-user-upload/91bbb28a368b-20230423.png =500x)
![](https://storage.googleapis.com/zenn-user-upload/ea04e167e1f5-20230423.png =500x)

登録したメールアドレスへのupdate情報などの通知を希望するか？といった選択肢がでるので、`y`or`n`の好きな方を選びます。

![](https://storage.googleapis.com/zenn-user-upload/9ccb1f7bccad-20230423.png =500x)

次に、人間の証明？がありますので、それが成功すると`Create account`のボタンが押せます。

![](https://storage.googleapis.com/zenn-user-upload/128b3b8a695e-20230423.png =400x)
![](https://storage.googleapis.com/zenn-user-upload/b43e3e91cfe7-20230423.png =400x)

最後に登録したメールアドレス宛てに認証コードが送られますので、それを入力すればアカウントの作成が完了します。

:::message alert
自分がアカウント作成したときは、認証コードを入れても認証確認中の状態が終わらず、アカウント作成が完了しませんでした。
結局、次の日に改めて認証コードの入力を行ったので、うまくいかない場合は少し時間を空けてみるといいかもしれません。
:::

![](https://storage.googleapis.com/zenn-user-upload/6f69f887725f-20230423.png =500x)

アカウント作成完了すると、以下のページに遷移します。

![](https://storage.googleapis.com/zenn-user-upload/984c2393f45a-20230423.png =500x)

## 初期設定

### 2要素認証対応

必須ではありませんが、セキュリティの観点からAuthenticatorアプリを使用した2要素認証の設定を行います。
必要ない方は飛ばして問題ありません。

基本的には、[公式の手順通り](https://docs.github.com/ja/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication)です。

まず、マイページの右上にあるアイコンボタンから`Settings`をクリックします。
その後、左側のメニュー内から`Password and authentication`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/e8d3bcc25e58-20230423.png =300x)

![](https://storage.googleapis.com/zenn-user-upload/0a40d6d2e137-20230423.png =300x)

2要素認証の設定画面で`Enable two-factor authentication`ボタンを押した後に、パスワードを入力します。

![](https://storage.googleapis.com/zenn-user-upload/05412580a39c-20230423.png =400x)

![](https://storage.googleapis.com/zenn-user-upload/276c2ceaa963-20230423.png =400x)

パスワード入力に成功すると、認証アプリでQRコードを読み込みます。
今回は、[Microsoft Authentictor](https://www.microsoft.com/ja-jp/security/mobile-authenticator-app)使用していますが、他にも、1PasswordやAuthyでもいけるようです（アプリ側の使用手順は割愛）。

![](https://storage.googleapis.com/zenn-user-upload/485f18605302-20230423.png =500x)

QRコードを読み込み、コードの入力に成功するとリカバリコードのダウンロード画面に遷移するため、ダウンロードして大切に保管します。

![](https://storage.googleapis.com/zenn-user-upload/787a1a4a9c3c-20230423.png =500x)

なお、他の2要素認証用の手段として、GitHub Mobileのダウンロードを推奨されるので、必要に応じてスマホにインストールください。

![](https://storage.googleapis.com/zenn-user-upload/39bfc95e9969-20230423.png =500x)

### メールアドレスの非公開設定

次に、GitHubアカウントのメールアドレスの非公開設定を行います。
以下のサイトを参考にしています。

https://qiita.com/emiki/items/4103150a5d7a7cfbff24

https://zenn.dev/ctrlkeykoyubi/articles/0ba47a8ec2bab5#emails

`Settings`をクリック後、左側のメニュー内から`Emails`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/0cb2d702c6d8-20230423.png =300x)

Email設定の下の方にある、以下の2つの項目にチェックを入れます（Keep my email...は最初からチェックが入っているはず）。

![](https://storage.googleapis.com/zenn-user-upload/3f7e1ef59c6e-20230423.png =300x)

![](https://storage.googleapis.com/zenn-user-upload/0adc2a27478e-20230423.png =400x)

こうすることで、GitHubにプッシュする際にGitHubに登録したメールアドレスではなく、GitHub側で自動生成されたアドレスが使用されるようになります。

なお、このGitHub側で自動生成されたアドレスは、後でローカルのGit側に紐付ける必要がありますが、それについてはこの後の記事で説明します。
