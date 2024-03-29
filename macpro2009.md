## MacPro2009のメモ

MacPro2009を購入し今でもまだまだ使えそうなスペックで、改造などかなりできるみたいなので、何とか活用したいと考えているのでいろいろメモしていく。  
macproの基本的なこと、macosのインストール方法、インストールメディアの作成方法、HDDの増設など。  
macosについても基本的なことも知らないので都度メモをしていく。

### macOSのファイルシステムのフォーマット

macOSを空のHDDにインストールしたいけど、フォーマットが必要なのかわからない。  
→macOSでもインストール時にフォーマットできた。

macOSに対応したフォーマットは、APFS、macOS拡張があり、windowsとmac両方に互換性があるフォーマット形式としてMS-DOS、exFATがある。  
(MS-DOSフォーマットは32GB以下のwindowsボリュームに使用、32GB以上のボリュームの場合はexFATを使用する)

APFSとmacOS拡張フォーマットは、macOSのディスクユーティリティメニューを使うことで、APFS形式やmacOS拡張形式でフォーマットできる。

#### APFS 
Apple File Systemの略。  
macOS10.13以降のデフォルトのファイルシステム。暗号化、領域の共有、スナップショット、高速なディレクトリのサイズ調整などが特徴。  
APFSはSSDストレージに最適化されているけど、HDDを搭載した以前のシステム、直接接続された外部ストレージでも使用できる。  
macOS 10.13以降では起動可能ボリュームとデータボリュームの両方でAPFSに対応している。

#### macOS拡張  
macOS10.12以前のmacOSを使うときは、macOS拡張フォーマットを使用する。以降のバージョンでもmacOS拡張でも大丈夫みたい。

### macOSインストールメディアの作成

今回はMac Pro2013 MontreyでHigh Sierraのインストールusbを作成に成功した。  
手順は下記。

- USBのフォーマット macOSのパソコンに挿入し、ディスクユーティリティを起動し、macOS拡張を選択して消去をすることでフォーマットができる。  
- USBを挿しておき、[appleの公式サイト](https://support.apple.com/ja-jp/HT211683)でOSイメージをMacのパソコンにダウンロードし、サイトの下部に記載されているコマンドをターミナルにコピペし実行するとusbにmacOSのインストールメディアが作成される。  

コピペするインストールメディアの作成コマンドは下記のような感じ。コマンドの動作として、macOSのアプリケーションフォルダにダウンロードされたmacOSのインストーラーが入っており、そこからUSBに書き込みがされる。

```
$ sudo /Applications/...
```

macOSのダウンロードとコマンドによるusbへの書き込みによるインストールメディアの作成は、その作業をしているMacがダウンロードするmacOSに対応可なバージョンじゃないとダウンロードは無理矢理できても書き込むための上記のコマンドを実行してもコマンドが実行できないようになっているので注意(terminalでcommand not foundとなる)。例えば、VenturaのパソコンでHigh Sierraのダウンロードおよび書き込みコマンドの実行はできない。

### MacPro2009にUSBを挿しインストーラを起動

作成したHigh SierraのUSBをMac Proに挿して電源ボタンを押す。  
起動音がしたらcキーを押下し続けると、リンゴマークが表示される。起動直後だとキーボードに通電していないので、キーボードのcaps lockなどのインジケーターが光った後にcキーを押下すると良さそう。もしリンゴマークが起動しなかったら、電源をボタンでオフにし、キーボード以外のUSBを一度抜いておく。電源を再びオンにする直前にUSBを再度挿す。

電源を再びオンにして、またcキーを押し続けてリンゴマークが表示されるまで待つ。１分以上待った。
何度か繰り返してもリンゴマークが出なかったら、一度PRAMリセットをする。電源をオンにしたらすぐに、command + option + P + Rキーを押し続ける。再度起動音がしたらリセットは完了となるので、電源ボタンで電源をオフにする。そして再びcキーを押下でリングマークの表示を待つ。今回はこれでリンゴマークが表示され、インストーラが立ち上がった。


何度かこの試行を繰り返してもリンゴマークが出なかったら、またはbootable os not foundなどが表示されたら、一度PRAMリセットをする。電源をオンにしたらすぐに、command + option + P + Rキーを押し続ける。再度起動音がしたらリセットは完了となるので、電源ボタンで電源をオフにする。そして再びcキーを押下でリングマークの表示を待つ。今回はこれでリンゴマークが表示され、インストーラが立ち上がった。

- [キーコンビネーションについて参照](https://support.apple.com/ja-jp/HT201255)

- [NVRAMとPRAMとは](https://support.apple.com/ja-jp/HT204063)

### HDDのフォーマットをしインストール

インストーラが立ち上がったら、ディスクユーティリティメニューも表示されるので、先にHDDのフォーマットをする。  
macOS拡張ジャーナルを選択し、消去を押すことでフォーマットできる。High Sierraからは、macOS拡張よりも進化したフォーマット形式であるAPFSフォーマットに対応しているのでAPFSフォーマットを選択して消去でも良い。  

High SierraはAPFSに対応しているが、今回はmacOS拡張でフォーマットした。macOS拡張でフォーマットし、High Sierraを問題なくインストールできた。

上記のようにHDDをフォーマットしたら、インストールボタンを押してmacOS High Sierraのインストールをする。

以上でインストール作業は完了。

### elecomのWi-Fi usbをWi-Fiとして利用する方法

エレコムのUSB型Wi-Fi子機の名称：WDC-433U2M2

elecom USB型のWi-FiインターフェースのドライバがCDのものも公式サイトのものもmacOS10.10までにしか対応しおらず、古すぎてドライバをHigh Sierraにインストールできない。  
ドライバとしてバッファローのWi-Fiドライバをインストールすると互換性があるためか、Wi-Fiが使えるようになる。

- [バッファローのWi-Fiドライバのページ](https://www.buffalo.jp/support/download/detail/?dl_contents_id=4264)

「WDC-433U2M2 macos BUFFALO ドライバ」のように検索すると出てくる。







