# いろんなメモ書いていく

いろいろ書いていきます。

## vimのLSPがインストールできない|golang

環境；thinkpad x220 windows10

現象; vimでgoのLSPのgoplsを:LspInstallServerでインストールしようとしても途中で止まってちゃんとインストールできない。

下記のようなメッセージが出る。

```
go get: installing executables with `go get` in module mode is deprecated.
Use `go install pkg@version` instead.
For more information, see https://golang.org.doc/go-get-install-deprecation
or run `go help get` or `go help install`.
```

<br />

![スクリーンショット 2021-10-07 230312](https://user-images.githubusercontent.com/43819429/136400441-882098ec-0895-4294-9393-52381f53e6f2.png)

<br />

go getは非推奨のコマンドなので代わりにgo installを使ってくれというメッセージ。
vim-lsp-settingsの:LspInstallServerコマンドで自動的にインストールされるので、
プラグインが実行するようにしているgo getコマンドをgo installコマンドに修正しないと
いけなそう。自動的にインストールしてくれ分便利だけどこういうとき一気に分からなくなる。

自分でやる方法もあるのかもしれないので調べてみる。qiitaに記事があった。
vim-lsp-settingsにもissueとして同じ現象のことが書かれていた。

goのコマンドなど全然わからないのでこの際基本から調べてみる。

goplsを自分でインストールすればとりあえずよさそうなのでよくわからないままに
下記コマンドを実行したらエラーが消えてlspも動いてくれているっぽいのでとりあえずは
ok。

```
go install golang.org/x/tools/gopls@latest
```

<br />

## a.exeでエントリポイントが見つかりませんが出て実行できない｜c++


![スクリーンショット 2021-10-12 185931](https://user-images.githubusercontent.com/43819429/136935271-c9b30551-af33-4f93-b52a-61ec926b90d0.png)


エントリポイントとは、...


cmdプロンプトを管理者で下記のコマンドを実行

```
> sfc / sannow
```

実行することで修復が必要なものは修復してくれる。


![スクリーンショット 2021-10-12 190928](https://user-images.githubusercontent.com/43819429/136936763-bcdea9b1-8f01-42b6-8fd4-19fa81b0160f.png)
