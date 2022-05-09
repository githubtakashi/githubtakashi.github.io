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


## packpath

packpathはプラグインを置くディレクトリの総称のこと.

packpath配下にプラグインを配置することでvimがpackpathの中のプラグインを
読み込んでくれてプラグインが使える状態になる。

自分の環境でのpackpathを確認する方法

```
:set packpath?
```

linuxで上記コマンドを実行すると、下記のようにpackpathが出力される。  
```
packpath=~/.vim,/usr/local/share/vim/vimfiles,/usr/local/share/vim/vim82,/usr/
local/share/vim/vimfiles/after,~/.vim/after
```

windowsの場合のpackpath

```
C:\tools\vim\vim82
```

このディレクトリの中にプラグインディレクトリを配置する。

<br />

```
{packpath}/pack/plugins/start 
```

この配下にプラグインディレクトリを配置する。

<br />

packディレクトリまではデフォルトで存在するので、pluginsとstartディレクトリを作成しておく。

```
mkdir tools\vim\vim82\pack\plugins
mkdir tools\vim\vim82\pack\plugins\start
```

上記のようにstartディレクトリを作成すると、start直下に保存したディレクトリが1つのプラグインディレクトリとして  
vimに認識される。

<br />

## プラグインの構成

プラグインのディレクトリ構成は下記のようになる。

<プラグイン名>.vim/

  autoload/
  
  doc/
  
  plugin/

上記のように一つのプラグインのディレクトリ内に3つのディレクトリを作成する。

<br />

- autoload/

autoload配下はメイン処理のファイルを置く。
Vimの起動時ではなくコマンド実行時に一度だけ読み込まれる。
ファイル名はプラグイン名と同じにしないといけない。

<br />

- plugin/

plugin配下はExコマンドやオプションを書いたファイルを置く。
ファイル名はプラグイン名と同じにしないといけない。

<br />

- doc/

doc配下はヘルプファイルを置く。
このディレクトリにヘルプファイルを置くことで、:h xxx みたいにヘルプを引けるようになる。

<br />

以上から、プラグイン名がneko.vimだとしたら、

autoload/neko.vim

plugin/neko.vim

のように同じ名前を付けることになる。

autoload配下のファイルで定義している関数をplugin配下のファイルのプログラムから呼び出すことを想定している場合は

"ファイル名#関数名()"

と命名する。理由は、

plugin配下のファイルからautoload配下で定義されている関数を呼ぶとき、

ファイル名と関数名によってどのファイルのどの関数を呼ぶかを指定し探しているため。

特に、autoload配下に複数のファイルがあるときはどのファイルから関数を探すのを

特定するためにこの命名方法が必要になる。



