## QMK Firmwareのメモ

環境：windows qmk msysを使用

qmk setupして以降の手順は忘れそうなのでメモ。

keyboardは biacco42/meishi2 をデフォルトとして設定済。その後の作業をメモしていく。

qmkファームウェアに登録されていてキーマップ設定の対応可能なキーボード一覧を確認するコマンドは下記。

```
qmk list-keyboards
```

自分用のキーマップを作成するために、まず下記のコマンドを実行する。

```
qmk new-keymap
```

すると、CLIでKeyboard nameとKeymap nameを聞かれるので入力。  

```
> Keyboard name: biacco42/meishi2
> Keymap name: katsuo1 //自分が分かれば名前は何でもよさそう。今回は左記のようにした。
```

上記から、下記のように設定ファイルが生成される。生成されたディレクトリ内のファイルが新たなキーマップを設定するファイルとなり、  
ファイル名はkeymap.cというファイル。

```
katsuo1 keymap directory created in:
C:/Users/takas/qmk_firmware/keyboards/biacco42/meishi2/keymaps/katsuo1
```

上記に加えてさらにメッセージが表示され、  
新しいキーマップをコンパイルするときには、下記のコマンドを実行するように表示される。

```
Compile a firmware with your new keymap by typing:

        qmk compile -kb biacco42/meishi2 -km katsuo1
```

