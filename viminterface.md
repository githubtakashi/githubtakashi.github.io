# vimやnvimで各言語のインターフェースを有効化する

python3, lua, perl, rubyなど、特にnvimではデフォルトでは無効化されているので有効化する。

## 無効か有効かの確認方法

```
:echo has('python3)
```

上記で0だと無効、1だと有効を意味している。

neovimだと:checkhealthコマンドで各言語の有効か無効かの情報が表示される。

## 言語を有効化する(linux:パッケージマネージャにapt使用)

[vimjpのドキュメント](https://vim-jp.org/docs/build_linux.html)を読んで、必要なパッケージをインストールする。


