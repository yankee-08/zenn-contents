---
title: "さくらのクラウドシェルを試してみた（会員登録済み）"
emoji: "🌸"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["sakuracloud","shell","cloud"]
published: true
---
昨日（2023/05/25）、さくらインターネットさんから、会員登録不要でブラウザから無料で利用できるシェル環境「さくらのクラウドシェル」の提供を開始したとの記事がリリースされました。

@[card](https://cloud-news.sakura.ad.jp/2023/05/25/cloud-shell/)

スペックなどについては、既に他の方が以下の記事で書いてくれていますので、自分の方ではせっかくなので会員登録した状態で試してみた結果を載せてみたいと思います。

@[card](https://qiita.com/umerin/items/2c37d8e2f304b758cf97#%E3%83%8D%E3%83%83%E3%83%88%E3%81%AB%E7%B9%8B%E3%81%8C%E3%82%89%E3%81%AA%E3%81%84%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%83%9E%E3%82%B7%E3%83%B3%E3%81%A8%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%84%E3%82%8A%E5%8F%96%E3%82%8A%E5%87%BA%E6%9D%A5%E3%81%AA%E3%81%84%E3%81%A8%E4%BD%95%E3%82%82%E5%87%BA%E6%9D%A5%E3%81%AA%E3%81%84%E3%81%AE%E3%81%A7%E3%81%AF)

# 試した環境

- OS：Windows 11 Home 22H2
- ブラウザ：Firefox 113.0.2

なお、対応ブラウザは、

> サポート対象のブラウザとバージョンは何ですか
> Google Chrome, Mozilla Firefox, Microsoft Edge, Apple Safari の最新バージョンでご利用いただけます。

と公式ページに記載があります。

# さくらのクラウドシェルの概要

![](https://storage.googleapis.com/zenn-user-upload/4e82aaf908a3-20230526.png)

公式ページに掲載されている下の画像に説明があります。

![](https://storage.googleapis.com/zenn-user-upload/408011f93a51-20230526.png)

ブラウザから使えるオンラインクラウドシェル環境で、予めPython等のプログラミング環境がインストールされており、簡単にプログラミングを試すことができます。
特に、**会員登録しなくても基本機能を使用可能**というのが、使いやすいのではと思います。

OSは`Ubuntu22.04`がベースになっており、シェルはデフォルトが`zsh`が有効になっています。
その他の仕様については[公式のリリース記事](https://cloud-news.sakura.ad.jp/2023/05/25/cloud-shell/)に記載の仕様表を確認ください。

![](https://storage.googleapis.com/zenn-user-upload/2ab8b2a511ff-20230526.png)

## 会員登録しない場合の制限

先ほどのページに記載がありましたが、基本的に会員登録の有無で差があるのは、**アクセス制限**の部分のみになります。

![](https://storage.googleapis.com/zenn-user-upload/0da76a3d6b5d-20230526.png)

会員登録しない場合は、全ての通信が遮断される形になります。
会員登録した場合は一部のポートのアウトバウンドが有効になるため、外部通信が可能になります。
なお、インバウンドではなく、アウトバウンドが有効化される形のため、クラウドシェル環境上から他のサーバへのアクセス（ssh、HTTP、HTTPSなど）といった使い方を想定していると思われます。

# 会員IDを使用して開始する手順

[トップページ](https://www.sakura.ad.jp/services/cloudshell/)から`無料で試す`をクリックして表示される以下の画面で、**会員IDで利用する**をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/e0ef5ba10725-20230526.png =400x)

さくらインターネット会員のログイン画面が表示されるため、会員IDとパスワードを入力します。

![](https://storage.googleapis.com/zenn-user-upload/88ddb35d552f-20230526.png =400x)

なお、会員IDを未登録の場合は、**新規会員登録**をクリックして、会員登録作業を行います。
登録手順は、さくらインターネットのサポート情報に詳細な説明がありますので、必要に応じて参考にしてください。

@[card](https://help.sakura.ad.jp/purpose_beginner/2545/)

会員IDを使用した、初めてのクラウドシェルの利用の場合、電話番号による二勝があります。

![](https://storage.googleapis.com/zenn-user-upload/8efc7252348f-20230526.png =400x)

会員登録時に入力した電話番号宛てに着信があり、電話に出ると数桁の認証コードを喋るので、そのコードを以下の画面に入力します。

![](https://storage.googleapis.com/zenn-user-upload/e89fb7811323-20230526.png =400x)

認証に成功すると、認証完了画面が表示されるので、次に進むボタンを押します。

![](https://storage.googleapis.com/zenn-user-upload/107dfeb10e89-20230527.png =400x)

# クラウドシェルの利用

ブラウザ上にクラウドシェルが立ち上がると、以下のような画面が表示されます。
会員IDを使って利用した場合、左上に**会員ID**が表示されます。
会員登録しないでシェルを立ち上げた場合、ここには**認証無し**と表示されます。

![](https://storage.googleapis.com/zenn-user-upload/4a584d552e46-20230527.png)

なお、シェル画面左下でフォントサイズや背景などを一部変更可能です。

![](https://storage.googleapis.com/zenn-user-upload/709233a256d0-20230527.png =400x)

会員登録済みの場合、アウトバウンドの通信が一部許可されているはずなので、いくつか試してみました。

## aptによるパッケージのインストール

`apt`によるインストールは問題なくできました。
以下は、`tree`パッケージをインストールして実行した例です（hoge,fugaはテキトーに作成）。

```shell
sakura@cloud-shell% sudo apt install -y tree
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  tree
0 upgraded, 1 newly installed, 0 to remove and 62 not upgraded.
Need to get 47.9 kB of archives.
After this operation, 116 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu jammy/universe amd64 tree amd64 2.0.2-1 [47.9 kB]
Fetched 47.9 kB in 1s (52.6 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package tree.
(Reading database ... 136425 files and directories currently installed.)
Preparing to unpack .../tree_2.0.2-1_amd64.deb ...
Unpacking tree (2.0.2-1) ...
Setting up tree (2.0.2-1) ...
Processing triggers for man-db (2.10.2-1) ...

sakura@cloud-shell% tree
.
├── README-cloud-shell.txt
└── hoge
    └── fuga

1 directory, 2 files
```

## リモートリポジトリからのgit clone

`git`はあらかじめインストールされているとのことでしたので、`git clone`ができるかも確認しましたが、こちらも問題なく動作しました。
逆に、認証なしの場合、リモートリポジトリからのcloneは難しいと思いますので、GitHubのリポジトリを使いたい場合などは会員登録が必要になると思います。
以下は、`git clone`で自分のGitHubリポジトリから`git clone`を行い、`tree`コマンドで構造を出力した例です。

```shell
sakura@cloud-shell% git clone https://github.com/yankee-08/M5-Unified-NTP-Clock.git 
Cloning into 'M5-Unified-NTP-Clock'...
remote: Enumerating objects: 27, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (20/20), done.
remote: Total 27 (delta 2), reused 19 (delta 1), pack-reused 0
Receiving objects: 100% (27/27), 3.32 MiB | 22.36 MiB/s, done.
Resolving deltas: 100% (2/2), done.
sakura@cloud-shell% ls
M5-Unified-NTP-Clock/  README-cloud-shell.txt  hoge/
sakura@cloud-shell% tree
.
├── M5-Unified-NTP-Clock
│   ├── LICENSE
│   ├── README.md
│   ├── image
│   │   └── img_001.JPG
│   ├── include
│   │   ├── README
│   │   ├── config.h
│   │   └── main.h
│   ├── lib
│   │   └── README
│   ├── platformio.ini
│   ├── src
│   │   └── main.cpp
│   └── test
│       └── README
├── README-cloud-shell.txt
└── hoge
    └── fuga

7 directories, 12 files```
```

現状、試せたのはこれ位ですが、今後何か試せればここに追記したいと思います。

# 思いつく活用方法

## パッとお試し

ラズパイやWindowsマシンでのWSL2など、最近ではLinuxの環境を簡単に用意しやすくなっていますが、ブラウザ上で簡単にLinux環境を試せるのは非常に魅力的だと思います。
また、VPSなどでも言えることですが、何か誤った操作をしてもすぐにリセットできるのはメリットでもあります（しかもそれが無料で試せるのは非常に助かる😎）。
なので、新しく試したいパッケージなどある場合に、まずはこの環境にインストールして好き勝手触ってみると言った使い方には適するのではないかと思います。

## 研修会（ハンズオン等）での利用

例えば、社内でLinuxのコマンドに関する研修会などを実施する場合にこのサービスを活用できるのではと思いました。
もちろんLinux環境の構築も含めて勉強することでより知識が深まると思いますが、特に環境構築の部分は躓きやすい（各自のPC環境がバラバラだと特に・・・）部分なので、そちらに時間がとられてメインのコマンドの部分の研修が満足にできなくなると言ったリスクは減らせるのではないかと思います。

## おわりに

まだリリースされたばかりでこれから使用ルールや機能改善などが行われていくとは思いますが、こういったサービスをリリースしてくれたさくらインターネットさんには非常に感謝したいです‼️

# 🔚
