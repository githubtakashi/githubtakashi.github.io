# Hexoでブログを作るためのメモ

静的サイトジェネレーターのHexoを利用してブログを作っていくためのメモを書いていく。

Hexoは静的サイトジェネレータ、外観テーマが整っている。マークダウンで書けることが特徴。

使うos：　　
MacOS(導入手順についての記事を見るとどれもMacOSの環境での手順だったため)  
windows11

詳しくは[公式のドキュメント類](https://hexo.io/docs/)を参照する。

<br />

## 準備としてパッケージをインストール|MacOSの場合

nvm(MacOS),node.js,npmをインストール

node.jsはiphoneに入れたアプリのiphoneに相当する、javascriptのアプリを入れる箱、実行環境のようなものとイメージ。  
nvmはnode.jsのバージョンを好きなものに切り替えることができるツールで、node.jsを包む箱のようなイメージ。  
npmはnode.jsで使うパッケージを管理するパッケージ管理ツールで、node.jsに同梱されている。  

最初にnvmをインストールし、nvmのコマンドでnode.jsをインストールする。
[nvmはgithubにあるパッケージ](https://github.com/nvm-sh/nvm)で、インストール方法もgithubを参照する。

下記コマンドでインストーラをダウンロードしインストールのためのシェルスクリプトが実行される。

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

ターミナルを一度閉じてまた開くとnvmのコマンドが使えるようになる。  

nvmコマンドのヘルプの表示：  

```
$ nvm --help
```

<br />

nvmのバージョンの表示：

```
$ nvm --version
```

<br />

nvmでインストールできるnode.jsを表示する：

```
$ nvm ls-remote
//インストール可能なnode.jsのバージョンがズラーっと表示される
```

<br />

nvmでインストールしたnode.jsのバージョンの表示：

```
$ nvm ls
```

<br />

任意のバージョンのnode.jsをインストール：

```
$ nvm install v16.14.2 //node.jsのバージョンv16.14.2をインストール
```

<br />

任意のバージョンのnode.jsをアンインストール：

```
$ nvm uninstall v16.14.2 //node.jsのバージョンv16.14.2をアンインストール
```

<br />

任意のバージョンのnode.jsを使う：

```
$ nvm use v16.14.2 //node.jsのバージョンv16.14.2を使用
```

<br />

npmを最新版にアップデート

```
$ npm update -g npm
```

以上でHexoで使用するパッケージのインストール作業は完了。

<br />

## 準備としてパッケージをインストール|windowsの場合

nvsをインストール(nvmとnvsがあるけどドキュメントではnvsを推奨しているため)。

chocoを使ってインストール。

```
> choco install nvs
> nvs //windows terminalをreopen後に実行
nvs : このシステムではスクリプトの実行が無効になっているため、ファイル C:\Users\katsuo\AppData\Local\nvs\nvs.ps1 を読み
込むことができません。詳細については、「about_Execution_Policies」(https://go.microsoft.com/fwlink/?LinkID=135170) を参
照してください。
```

上記のように、メッセージが出る場合がある。初期値ではスクリプトの実行が無効になっているので、その場合はスクリプトの実行を有効にする。

```
> Get-ExecutionPolicy //実行ポリシーを確認
Restricted //確認結果
```

実行したユーザーのPowerShell上においては署名が行われたシェルスクリプトは制限なく実行できるように変更(自作スクリプトも制限の対象外になる)。

```
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> Get-ExecutionPolicy
RemoteSigned
```

nvsでnodeのインストールをしたり特定のバージョンに切り替えたりする。  
[nvsのドキュメント](https://github.com/jasongin/nvs/)を参照する。


```
> nvs add latest //最新版のnode.jsをインストール
> nvs use node/17.8.0/x64 //現在のシェルにパスが通る
PATH += $env:LOCALAPPDATA\nvs\node\17.8.0\x64
> node link node/17.8.0/x64 //デフォルトでの使用設定
$env:LOCALAPPDATA\nvs\default -> $env:LOCALAPPDATA\nvs\node\17.8.0\x64
User profile PATH += $env:LOCALAPPDATA\nvs\default
```

npmでhexo-cliをインストール

```
> npm install -g hexo-cli
```

ブログ用のローカルディレクトリを作成する。

```
> mkdir C:\Users\user\blog
```

ブログ用のローカルディレクトリをhexoで初期化する。

```
> hexo init C:\Users\user\blog
```

初期化によってブログにひつようなファイルが生成される。

hexoのブログをローカルサーバーで確認

```
> cd blog
> hexo server
```

表示されたアドレスをブラウザに入力するとウェブブラウザの画面が’表示される。  
Ctrl + cで停止できる。

![hexoinit](https://user-images.githubusercontent.com/43819429/164973954-3b628254-ae0f-4a1b-b39d-50f9ba22ee71.png)

生成されたファイルの説明

![hexofiles](https://user-images.githubusercontent.com/43819429/164974134-ff7c0a34-5d12-41c1-a8e9-7bc5d1f8c63d.png)

node_modules：  
構成しているnpmライブラリの置き場所

public：  
公開用のデータ一式がここに書き出される

scaffolds：  
記事や固定ページを作るときに必要なMarkdownテンプレート集

source：  
記事や固定ページを構成するMarkdown,画像データを置く場所

themes：  
ブログのテーマが置かれる場所（デフォルトテーマ入が最初から入っている）

config.yml：  
ブログのタイトルやURLなどの設定を書くためのファイル

.gitignore：  
gitの取り扱いの対象外にさせるファイルやディレクトリを書くファイル

db.json：  
キャッシュが書き込まれるファイル

package-lock.json：  
特定のバージョンのライブラリ構成を共有するためのファイル

package.json：  
Hexoを構成しているライブラリのリスト

config.ymlの内容を修正して/source内にMarkdownで記事を作って、/publicに書き出されたファイル一式を  
Web上にアップロードするとブログが公開できる。

npmコマンドで/node_modulesにライブラリを追加することで機能の追加ができる。

/themes内でテーマを編集または追加または新規作成すると、ブログの見た目や出力方法を変えられる。

Hexoブログの設定はconfig.ymlに書き込んで変更する。



config.ymlファイルを編集(編集する箇所のみ抜粋)

```
# Site
title: katsuo blog
subtitle: ''
description: ''
keywords:
author: katsuo
language: en
timezone: ''

# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://kyachuo.github.io/katsuo-blog/ # 自分のgithub pagesのurl
permalink: :year/:month/:day/:title/
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
  
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: 'git'
  repo: https://github.com/kyachuo/katsuo-blog.git　# 自分のgithubのブログのリポジトリ
  branch: master
```

gitでdeployするためにパッケージをインストール

```
> npm install hexo-deployer-git --save
```

ブログをgithub pages上にデプロイ

```
> hexo deploy
```

