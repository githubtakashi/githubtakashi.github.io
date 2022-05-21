# WSL2を導入するためのメモ

WSL2に何気なく興味を持ったのでwsl2を導入する。  
マシン：dell precisionのデスクトップpc、windows11pro

<br />

wsl2をインストールする前のwindowsOS側の準備として下記をする。

## Linux用Windowsサブシステムを有効化

管理者権限でパワーシェルを開いて実行

```
> dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

<br />

## 仮想マシンの機能を有効化する

管理者権限でパワーシェルを開いて実行

```
> dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

<br />

## wsl2を規定のバージョンにする

wsl1じゃなくて新しいバージョンの2を使いたいので規定にする。

```
> wsl --set-default-version 2
```

<br />

## 任意のLinuxをインストール

ubuntuをインストールする場合

microsoft storeからubuntuをインストールする。または、シェルからインストールする。  
その場合は下記のコマンドで、シェルからインストールできるosが一覧で表示される。

```
wsl --install --online
wsl --install -d Ubuntu-20.04 // ubuntu20.04をインストールする場合のコマンド
```

上記のリストでは最新のubuntu22.04が出てきてなく、microsoft storeからしかインストールできない。
22.04のインストールが正常にできなかったので、20.04から22.04にアップグレードする手順を書いておく。

## ubuntu20.04から22.04にアップグレードする方法

現状のバージョン確認

```
cat /etc/os-release
```

現状のパッケージを最新にしておく

```
sudo apt update && sudo apt upgrade
```

ディストリビューションアップグレードの依存解決をする。  
アップグレード前に必要なパッケージがあればインストールされる。

```
sudo apt dist-upgrade && sudo apt install update-manager-core
```


lts設定をしておく

```
sudo nano /etc/update-manager/release-upgrades

//Prompt=ltsであることを確認しなってない場合は左記のようにltsを記載しておく。
```

22.04へのアップグレード実施

```
sudo do-release-upgrade -d
```

最後にrebootするところはwslのubuntuではできないので、winterminalからwsl --shutdownを実行し停止後再度ubuntuを開くことで  
アップグレードが完了する。

## ubuntuなど再起動する方法

再起動や停止は別途windows terminal側で下記コマンドを実行する必要がある。

```
wsl --shutdown
```

再起動の場合は、上記コマンドの後で再度ubuntuなど開けば再起動と同じとなる。
ubuntuなどの中でrebootなどコマンドを実行しても再起動はできない?!みたいなので、上記のようにする。

ubuntuなど画面を閉じるだけで停止されていたかと思っていたけど、実は動き続けているかもしれないので、  
終了させるときは毎回wsl --shutdownをしといたほうが良いかも。

## ubuntuなどosの起動

アイコンクリックするか、winterminal上で下記コマンドを実行。  
個人的にはwinterminalのUI上でそのまま起動できるほうが見た目もよいので、コマンドで実行していきます。

```
//ubuntuを起動する場合
wsl -d ubuntu-20.04
```

