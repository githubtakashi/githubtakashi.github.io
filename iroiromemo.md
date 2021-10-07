# いろんなメモ書いていく

いろいろ書いていきます。

## vimのLSPがインストールできない

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



