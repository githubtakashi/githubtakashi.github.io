# haskellのメモ

haskellの勉強を始めるのでメモしていく。

## haskellの環境準備

thinkpad x220 windows10にhaskellの環境を準備する。

stackというパッケージ管理ツールをインストールして、stackでhaskellをインストールするという手順。

stackはchocoでインストールできるのでchocoでstackをインストール。

```
> choco install haskell-stack
```

<br />

下記コマンドでhaskellに必要な準備がされる。
haskellやghcというコンパイラのインストールなど。

```
> stack setup
```

<br />

haskellのバージョンおよびstackのバージョンをを確認するためのコマンド

```
> stack ghc -- -V
> stack --version
```

<br />



下記コマンドで対話型のインターフェースが起動され、

Prelude>　というプロンプトになる。

```
> stack exec ghci
```


