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

## 文字化けを解消(powershell)

cppファイルの中に日本語があると、powershellで実行時に文字化けする。

原因は、windowsのシステムはshift-jisがデフォルトでセットされているため、uft-8の日本語が文字化けする。  
下記のコマンドで現在のセット値が確認できる。

```
> chcp
```

shift-jis に対応する値は 932で、uft-8に対応する値は 65001

chcpで確認した値が932の場合、65001に変更するには、下記のコマンドを実行する。

```
> chcp 65001
```

ただし、ターミナルを閉じるとまたリセットされて932に戻ってしまう。

永続化は、下記の手順。

C:\Users\katsuo\OneDrive\ドキュメント\WindowsPowerShell\Microsoft.PowerShell_profile.ps1  
のように、Microsoft.PowerShell_profile.ps1ファイルを開き、1行目に下記のコマンドを入力して保存する。  

```
Invoke-Expression -Command "chcp 65001"
```

windows termnalで使うpowershellのプロファイルを読み込んで上記のコマンドが実行されるので、utf-8への変更を  
毎回手でしなくてもよくなる。

ただ、mod + xメニューなどから直接powershellを開くと、こっちには反映はされていないので、shift-jisのまま。  
こっちもutf-8に変更するには、下記のようにする。

エクスプローラで下記のパスを開く。  
%userprofile%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Windows PowerShell  
直接開くpowershellを右クリックする。プロパティの"リンク先"に下記をペーストする。

```
%SystemRoot%\system32\WindowsPowerShell\v1.0\powershell.exe -NoExit -Command "chcp 65001"
```

以上で、windows terminal経由で開くpowershellも直接開くpwershellもutf-8に設定されることが永続化される。

## プロンプトのカスタム

[microsoftの記事でoh my poshという便利なプロンプト](https://docs.microsoft.com/ja-jp/windows/terminal/tutorials/custom-prompt-setup#customize-your-powershell-prompt-with-oh-my-posh)があって、記事を参照することで設定できる。



