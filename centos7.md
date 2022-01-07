# CentOS7をサーバーとして使うためのメモ

サーバーの勉強をするためにcentOS7を新規インストールしサーバーを構築していく。

PC: IBM System x3105(2006年式) Athlon64 3500+ 1core CPU Memory8GB HDD1TB

usbでのインストールはusbを認識しなかったので、DVDにISOイメージを焼いてインストールメディアを作成した。

<br />

## CentOS7のインストールメディア作成方法(DVD)

windowsのpcで作成するとスムーズにできる。  
centOSの公式サイトからisoイメージをダウンロード。今回はサイズの小さいminimalのisoを選択した。  
ダウンロードが完了したら、isoファイルを右クリックし"dvdに書き込む"旨の表示をクリックすると  
isoイメージがdvdに書き込まれる。

<br />

## CentOS7のインストール

pcにdvdをセットしpcを機動したらF12キーでcdドライブを選択しエンターをするとインストール画面が表示されるので  
installをエンターでGUIで視覚的にインストールできる。

<br />

## デスクトップ環境のインストール

minimalインストールはプロンプトのコンソール画面でデスクトップ環境がインストールされていないので、インストール。  
コンソール画面でとネット接続された状態でpcが立ち上がることをランレベル3という。ランレベル0はシャットダウン。  
pc起動時にデスクトップ環境が立ち上がることをランレベル5と呼ぶ。  

### sudo権限をユーザーに付与する

sudoがユーザーに設定されていないためsudoが使えないので、suでルートユーザーになり、visudoコマンドで使えるように設定する。

```
$ su -
# visudo
// visudo file
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL

katsuo  ALL=(ALL)       ALL //<username> ALL=(All) ALLを追加
```

### Gnome Desktopをインストール

yumでグループインストールという機能を使って一気にデスクトップ環境をインストールできる。

yum grouplistというコマンドで利用できるパッケージが確認できる。

```
$ sudo LANG=C yum grouplist

Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: ftp.iij.ad.jp
 * extras: ftp.iij.ad.jp
 * updates: ftp.iij.ad.jp
Installed Environment Groups:
   GNOME Desktop
Available Environment Groups:
   Minimal Install
   Compute Node
   Infrastructure Server
   File and Print Server
   Basic Web Server
   Virtualization Host
   Server with GUI
   KDE Plasma Workspaces
   GNOME Desktop
   Development and Creative Workstation
Available Groups:
   Compatibility Libraries
   Console Internet Tools
   Development Tools
   Graphical Administration Tools
   Legacy UNIX Compatibility
   Scientific Support
   Security Tools
   Smart Card Support
   System Administration Tools
   System Management
Done
```

この一覧の中にGNOME Desktopがあるので、これをインストールする。

```
$ sudo LANG=C yum groupinstall "GNOME Desktop"
```

installが完了したら"$ startx"でデスクトップ環境が立ち上がる。

<br />

### pc起動時からデスクトップ環境が立ち上がるようにする

ランレベル3からランレベル5に変更する。

現在のランレベルを確認

```
$ sudo systemctl get-default
multi-user.target
```

ランレベル3はmulti-user.target。

ランレベル5はgraphical.targetなので、この記述に変更する。

```
$ sudo systemctl set-default graphical.target
```

以上で再起動するとグラフィカルなログイン画面が立ち上がり、ログインするとデスクトップ環境となる。

