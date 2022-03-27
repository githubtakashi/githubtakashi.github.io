# Hexoでブログを作るためのメモ

静的サイトジェネレーターのHexoを利用してブログを作っていくためのメモを書いていく。

Hexoは静的サイトジェネレータ、外観テーマが整っている。マークダウンで書けることが特徴。

使うos：　　
MacOS(導入手順についての記事を見るとどれもMacOSの環境での手順だったため)

<br />

## 準備としてパッケージをインストール

nvm,node.js,npmをインストール

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



