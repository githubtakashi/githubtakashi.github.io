## starshipについてのメモ

starshipについてのメモ。windows terminalでの設定など。

### starshipのインストール

windowsの場合

starshipインストールの前にnerd fontsをインストール。  
nerd fontsの公式サイトでフォントをダウンロードし解凍しフォントファイルを展開する。

C:\Windows\Fontsフォルダに解凍したファイルをコピペしたらインストールされる。

starshipのインストール

```
> choco install starship
```

C:\Users\ユーザ名\Documents\WindowsPowerShellフォルダに  
Microsoft.PowerShell_profile.ps1ファイルを作成し下記コードを記載する。

```
Invoke-Expression (&starship init powershell)
```

### 設定

~/.config/starship.tomlに設定を書いていく。  
設定内容については後で追加

```
mkdir .config
cd .config
vim starship.toml
```

```
このシステムではスクリプトの実行が無効になっているため...Microsoft.PowerShell_profile.ps1を読み込むことができません。
```

というエラーメッセージが出たらスクリプトを有効にするため下記の対応を行う。  
ローカルで作成したスクリプトは署名なしで実行可能で、ネットから取得したスクリプトは署名があるときのみ実行できるようにする。

1.PowerShellを管理者権限で開く  
2.下記コマンドを実行

```
> Set-ExecutionPolicy RemoteSigned
```

通常スクリプトの実行はセキュリティにとって危ないのでデフォルトでスクリプトの実行ができないように設定されている。 
ローカルで作成したスクリプトか、ネット上から取得したスクリプトか、スクリプトの署名の有無という分類で  
スクリプトの実行の有効化を設定できるようになっている。


