# vim pluginの勉強メモ

vim pluginの勉強メモを記載していく。

## runtimepath

下記のコマンドを実行すると、プラグインの読み込まれるパスが表示される。
表示されている順番に読み込まれる。

```
:set runtimepath
```

<br />

![スクリーンショット 2021-09-23 022804](https://user-images.githubusercontent.com/43819429/134392447-0fa86e12-82c8-40a2-ac5f-d0b6b4158b20.png)

<br />

vimのデフォルトでインストールされているプラグインやカラースキームなどが入った主要なディレクトリを
$VIMRUNTIMEといい、ディレクトリは下記にある。あくまで例なので:set runtimepathで確認するのが確実。

- Linux: /usr/share/vim/vim82
- Windows: C:tools\vim\vim82

<br />

