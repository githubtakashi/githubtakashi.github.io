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

