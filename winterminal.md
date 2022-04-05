## Windows Terminalのメモ

Windows Terminalの設定方法をメモ

### vscodeのインストール

JSONファイル編集で自動的にプロパティや値を補完してくれるのでインストールしておくと便利。

chocoでインストール。

### cursorShape

defaultsの中に書く。  
カーソルの形状を指定できる。

### 背景画像

背景画像にしたい画像を任意のフォルダに保存し、下記のように設定をする。  
defaultsの中に書く。  
uniformToFillにすると背景画像をターミナルの大きさに自動調整してくれる。

```
"backgroundImage": "C:\\Users\\takas\\wallpaper1.jpg",
"backgroundImageOpacity": 0.5,
"backgroundImageStretchMode": "uniformToFill"
```

## 余白

余白を設定できる。  
padding: 8,8,8,8のような記述方法

## opacity

背景の透明度を設定できる。  
"opacity": 80,
"useAcrylic": false

アクリル設定をfalseにすると背景が透ける。

dell precision m6500ではアクリルになってなぜか透けなかった。GPUが古いか、解像度が低いため対応していないみたい。


