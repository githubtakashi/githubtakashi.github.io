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

microsoft storeからubuntuをインストールする。

