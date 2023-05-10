# Hexoでブログを作ってgithub pagesで公開するためのノート

node.jsを利用した静的サイトジェネレーターのHexoでブログを作成し、github pages上でブログを公開するための手順の忘備録。

<br />

## Hexoの特徴

Hexoの特徴として下記があげられる。  
- HTML、CSS、JavaScriptによるブログの静的ページを生成できる静的サイトジェネレータ  
- ブログを構築するためのテンプレートやプラグインがオープンソースでいろんな人が公開しておりそれらを使うことができる  
- マークダウンで記事を書くことができ、人がマークダウンで作成した記事は公開の際に自動的にHTMLに変換して出力される

<br />

## Hexoは基本的なことを理解することが大切

Hexoの仕組みとして、Hexoがブログのインフラ。そしてHexoのために様々なブログテーマのテンプレートやプラグインなど、  
Hexoの機能を拡張できるものが様々な第3者によって公開されている。  

そのため、Hexoを利用するにあたっては、下記のアプローチが必要となる。  
- Hexoの基本的な使い方や操作方法を覚える。  
- 第3者がHexoのために公開しているブログテーマのテンプレートを導入する方法と、そのテンプレートを利用するための設定方法などについて覚える。

<br />

記事を見るとよく書かれているが、Hexoは簡単ということらしいが、個人的に感じた感じではむしろ逆で、ある程度基本的な仕組みを理解していないと、  
何をしているのかが分からなくなる。そのため、まずはHexoについての使い方をきちんと自分なりに整理しておくことが大切。

<br />

## Hexoを利用するために必要な要件

- OS  
OSは何にでも対応している。  

- パソコン  
パソコンのローカルの記憶装置にHexoに必要なファイル類を全て保存するので、ある程度の記憶容量があった方がいい。

<br />

## Hexoについての概要

Hexoで楽々ブログを作れる!!みたいな、簡単さを強調するようなフレーズをやたらち見かけるので、簡単なのかと思っていると、  
全然そんなことはなく、むしろ難しくてものにならないとさえ感じました。なので、まずは概要を分かる範囲で理解していこうと  
考えました。

Hexoは、パソコンのローカルの記憶装置に保存し作成したファイルをGitHub上にアップロードし、github pagesのホスティング機能を利用して、  
ブログとしてリリースする。

そのため、まずはローカルでブログを作成して、github pagesでホスティングするのに必要なファイル一式をgithub pagesのリポジトリにアップロードする。  
そしてgithub pagesの機能によってブログをビルドし、公開するという手順になる。


hexo自体がnpmでインストールするパッケージなので、hexoはnode.jsの実行環境で動作するアプリ。

詳しくは[公式のドキュメント類](https://hexo.io/docs/)を参照する。

<br />

## 準備としてパッケージをインストール|MacOSの場合

nvm(MacOS),node.js,npmをインストール

node.jsはiphoneに入れたアプリのiphoneに相当する、javascriptのアプリを入れる箱、実行環境のようなもの。  
nvmはnode.jsのバージョンを好きなものに切り替えることができるツールで、node.jsを包む箱のようなもの。  
npmはnode.jsで使用するパッケージをインストールしたり削除したりするパッケージ管理ツール(aptやbrewのような)で、node.jsに同梱されている。  

※nvmでnode.jsをインストールしなくても、brewで最新版のnode.jsをインストールし、brew upgradeでnode.jsを最新版にするというシンプルな. 
方法の方が簡単かも。brewでnode.jsをインストールするには、下記のコマンドを実行する。

```
brew install node
```

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

初期化によってブログに必要なファイルが生成される。

hexoのブログをローカルサーバーで確認

```
> cd blog
> npm install //必要なパッケージがインストールされる
> hexo server
```

表示されたアドレスをブラウザに入力するとhexoで作られたブログの画面が表示される。  
ローカルサーバーはCtrl + cで停止できる。

![hexoinit](https://user-images.githubusercontent.com/43819429/164973954-3b628254-ae0f-4a1b-b39d-50f9ba22ee71.png)

生成されたファイルの説明

![hexofiles](https://user-images.githubusercontent.com/43819429/164974134-ff7c0a34-5d12-41c1-a8e9-7bc5d1f8c63d.png)

node_modules：  
hexoで使われるnpmライブラリの置き場所

public：  
公開用のデータ一式がここに書き出される

scaffolds：  
記事や固定ページを作るときに必要なMarkdownテンプレート集。  
hexoで新しい記事をビルドするときに、このフォルダからマークダウンの.mdファイルを参照する。

source：  
記事や固定ページを構成するMarkdown,画像データを置く場所  
この場所の記事用のmdファイルをマークダウンで編集することで、ブログ記事として反映される。

themes：  
ブログのテーマが置かれる場所（デフォルトテーマ入が最初から入っている）

config.yml：  
ブログのタイトルやURLなどhexoで作られるブログの設定を書くためのファイル

.gitignore：  
gitの取り扱いの対象外にさせるファイルやディレクトリを書くファイル

db.json：  
キャッシュが書き込まれるファイル

package-lock.json：  
特定のバージョンのライブラリ構成を共有するためのファイル

package.json：  
Hexoを構成しているライブラリのリスト。EJS、stylus、markdownなどの機能がデフォルトで組み込まれている。  
EJSはJavascriptで使われるテンプレートエンジンと呼ばれる機能で、共通パーツのヘッダーやフッターなどを  
パーツ化することで、個別に管理できるもの。ワードプレスのテンプレートに使われるような機能。  
stylusは、CSSを便利に書けるようになっている機能。  
デフォルトで入っている機能は後で任意でアンインストールできるようになっている。

config.ymlの内容を修正して/source内にMarkdownで記事を作って、/publicに書き出されたファイル一式を  
Web上にアップロードするとブログが公開できる。

/node_modulesディレクトリにnpmコマンドで特定のnodeライブラリを追加することで任意の機能を追加できる。

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
  スラッシュなどあらかじめ設定されているアクセス方法でアクセスされたら自動でindex.htmlを探して表示する機能。おそらく。
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
  
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: https://github.com/kyachuo/katsuo-blog.git　# 自分のgithubのブログのリポジトリ
  branch: gh-pages
```

詳しくは[hexoのドキュメント](https://hexo.io/docs/configuration)に書いてあるけど、  
サブディレクトリの設定もできる。自分のconfig.ym fileでは項目を削除してしまっている。必要に応じて追加する。

サブディレクトリとは、ブログの中に少しメインとは異なるジャンルの子ブログを作るみたいなイメージ。  
もともとのブログのドメインパワーを引き継ぐことができる。

<br />

gitで簡単にdeployするためのパッケージをインストール

```
> npm install hexo-deployer-git --save
```

ブログをgithub pages上にデプロイ

```
> hexo deploy
```

<br />

### テーマのあてかた

hexoのサイトでいろんなテーマを載せている[ページ](https://hexo.io/themes/)があるので、そのページから好みのテーマを決める。  
テーマを決めたら、使いたいテーマのgithubのリポジトリのリンクをクリックしリポジトリのページで導入の仕方など参照する。

テーマのリポジトリを自分のローカルパソコンにインストールし、必要なパッケージ等を説明に沿って別途インストール等して、config.ymlファイル  
にテーマを設定することでテーマを適用することができる。

テーマのリポジトリを自分のローカルパソコン上にインストールする方法は何種類かある。

テーマのマニュアルを読むとテーマを適用する方法が載っているのでそれを参照してする。

最初はicarusというテーマを使ってみたが設定が難しく感じたので、particlexというテーマを適用してみた。

[particlexのgithub](https://github.com/theme-particlex/hexo-theme-particlex)に設定方法が記載されている。

どのテーマを使うかの判断として、githubを見て数年更新されていない場合は何かと面倒なことになったので、  
なるべく新しいテーマを使った方がスムーズに設定など進むので良いと感じた。

<br />

### particlexの設定メモ

particlex専用の設定のconfig.ymlファイルは、themes/particlexディレクトリ内にある。

#### 設定項目

- pollyfill. 
古いブラウザでもJavaScriptがきちんと動作させるためのプラグイン。これを設定することで、  
未対応のブラウザでもおかしくなることなくちゃんと動作してくれる。デフォルトで有効になっている。

- highlight.js. 
記事にソースコードを記載するときに見やすく色分けハイライト表示してくれる。デフォルトで有効になっている。

- Katex math rendering. 
数式を表示するための設定。HTMLとCSSだけで描画するので描画速度がsvgよりも速い。  
デフォルトで無効になっている。

- Image Preview. 
画像をクリックしたときに拡大、縮小する設定。デフォルトで有効になっている。

- Giscus. 
記事にコメント機能をつけるための設定. 
デフォルトでは無効
