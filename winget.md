# windows10のパッケージ管理にwingetを使う

chocolateyの代わりにwindows公式のパッケージマネージャのwingetを使用してみた。  
使用方法などメモ。

windows11だと標準でインストールされている。windows10では標準ではインストールされていない。  
windows10にwingetをインストールするためには、windows Insider Programに登録して、アプリケーションインストーラー  
というアプリをwindowsストアでインストールすると、同梱されているので、wingetが使えるようになる。

今回はThinkpad Yoga windows10 homeにインストール。

winget search <パッケージ名>

winget install <パッケージ名>

など、aptみたいに使える。

```
> winget
```
とだけ入力し実行すると、使い方が表示される。

[詳しい使用方法](https://docs.microsoft.com/ja-jp/windows/package-manager/winget/?msclkid=754254dcaa2711ec9d8de897d55e2bc9)は公式の情報を確認する。





