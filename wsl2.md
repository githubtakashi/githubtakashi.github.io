# WSL2を導入するためのメモ

WSL2に何気なく興味を持ったのでwsl2を導入する。  

wslの基本的なコマンドなどは[公式サイトの説明](https://learn.microsoft.com/ja-jp/windows/wsl/basic-commands)を参照する。

<br />

wsl2をインストールする前のwindowsOS側の準備として下記をする。

## Linux用Windowsサブシステムを有効化

管理者権限でパワーシェルを開いて実行

```
> dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

<br />

## hyper-vの有効化

```
DISM /Online /Enable-Feature /All /FeatureName:Microsoft-Hyper-V
```

<br />

## 仮想マシンの機能を有効化する

管理者権限でパワーシェルを開いて実行

```
> dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

<br />

## コマンド1個でインストールが済むようになった| 追記

コマンド１個でインストールができるようになった。楽すぎる。これ以降の内容は以前の手順。

```
wsl --install
```


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
wsl --list --online
wsl --install -d Ubuntu-20.04 // ubuntu20.04をインストールする場合のコマンド
```

## インストール直後のエラーの解決方法

ubuntuをインストールして最初はエラーが出る。その場合はカーネルが古いので、下記のコマンドでカーネルを最新にする。

```
wsl --update
```

wsl --list --onlineによるリストでは最新のubuntu22.04が出てきてなく、microsoft storeからしかインストールできない。
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

## ubuntuのアップグレード時に出るワーニングの対処

出たubuntu=ubuntu22.04LTS

sudo apt upgradeを実行すると、下記のメッセージがでる。出ても、アップグレードに失敗している訳ではないみたい。

```
Failed to retrieve available kernel versions.
Failed to check for processor microcode upgrades.
```

上記のメッセージが出ないように設定できる。下記のファイルを編集する。

```
sudo -e /etc/needrestart/needrestart.conf
```

編集は、下記の項目のコメントを解除して、値として0を設定する。  
$nrconf{kernelhints} = 0;  
$nrconf{ucodehints} = 0;  

他にも、下記のメッセージも出てくるが、別に無視しても大丈夫みたい。  
消すなら、下記コマンドでパッケージ自体を消すと出なくなるようにできる。

```
sudo apt purge needrestart
```

<br />

## wsl2でsystemdを使うための手順

wsl2のubuntuではsystemctlが動いてなく、PID1のinitプロセスが動いている。systemctlで動くサービスが動かない状態となっている。  
そのため、systemctlを動かす対策が必要。

実際、mysqlをインストールしてもエラーで動作しなかった。

PID1はinitプロセスと呼ばれている。initプロセスとはunix系OSでbootの最初に起動される一番最初のプロセス。

Linuxのプログラムはすべて、まずinitプロセスが動き、必要な他のプロセスを呼び出し実行されるので、initプロセスは親プロセスとも呼ばれる。

芋づる式にプロセスがプロセスを起動することで必要な処理ができるようになっているので、もとをたどるとinitプロセスになる。

- [initプロセスについて分かりやすかった記事](https://atmarkit.itmedia.co.jp/ait/articles/0204/02/news002.html)




