# RetroPieを使うためのメモ

thinkpad t60 ubuntu20.04.lts core 2 duo にretropieをインストールした。

retropieはubuntu debian ラズパイ等にインストールできるゲームをするためのエミュレータ。

<br />

## install

インストールは下記の手順で行う。

```
> sudo apt update && sudo apt upgrade
> sudo apt install -y git dialog unzip xmlstarlet
> git clone --depth=1 https://github.com/RetroPie/RetroPie-Setup.git
> cd RetroPie-Setup
> sudo ./retropie_setup.sh
```

![001](https://user-images.githubusercontent.com/43819429/146856535-4f4cfabe-77c7-420c-a162-44721e60d604.png)


上記でretropieがビルドされインストールされたらTUIでのメニューが表示され各種設定ができる。  
メニューはretropieが準備したスクリプトで簡単に各種設定ができるようになっている。

retropie設定のTUIメニューは下記コマンドでいつでも立ち上げられる。

```
> cd RetroPie-Setup
> sudo ./retropie_setup.sh
```

retropieの起動は"emulationstation"というコマンドでretropieが起動できる。

インストールしただけなのでまだ起動しても何もできない。

~/Retropie/ディレクトリの中に各種ゲームのromデータを入れることがあとで必要になってくる。

<br />

## sambaの利用

sambaというパッケージでディレクトリ共有ができ、外部からromデータを入れることができるので便利。


"Configuration/Tools" の"samba - Configure Samba ROM Shares" を選択。"Install RetroPie Samba shares" を選択.

Sambaと共有ディレクトリの設定が行われる。


