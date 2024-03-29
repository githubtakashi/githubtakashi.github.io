# vim メモ

vimを使う｜プラグインを作成する

ときの進め方やメモを書いていく。気づいたことなどなんでも

<br />

## プラグインを作成するために勉強を進めていたときの気付き

```
:h write-plugin
```

でマニュアルを読んで、note.muにメモ記事としてまとめていっていて気づいたこと。
量が膨大なので、勉強していっても終わらないということ。
これではプラグイン作成の段階に入る以前に勉強さえも終わらないので効率がかなりわるい。
プラグインを作りながらプラグインに必要なことを都度調べるという進め方が良さそう。
基本の流れとして、プラグインを作ることをメインにしてvimの勉強を並行して進めていくことがよさそう。
また、プラグインだけでなくて、操作方法やvimrcを書くこと、プラグインを使っていくことも同時に
進めていくので、そういったこととのバランスも意識したほうが良さそう。要はvimに時間をいっぱい使うことがよいのかも。

<br />

## vimの進め方

vim力をアップさせるために下記の方針でいく。

- vimjpのサイトを見る。

- vimtutorでわすれていることを復習する。たまにでいいかも。

- マニュアルを読んでできることを増やしていく。情報量が膨大できりがないので時間をかけすぎないようにする。

- thinkpad x220 kindleで実践vimを読みつつ手を動かしていく

- 便利なプラグインを使っていく

- vimrcの設定をすすめていく

- プラグイン作成していく

<br />

## vimでわからないことを調べる方法

vimでわからないことを調べるのが難しい。例えばnoremapなど、単語一つとってもマニュアルから
どうやって探すのがいいのかわからない。標準的な方法とかあるのかもしれない。
とりあえず思いつくのが、マニュアル内でコマンドモードで"/noremap"などと検索。
オンラインマニュアルがあるので、そっちの方が見やすいけど、vim使うなら普通のマニュアルに慣れておきたい。

<br />

## 各種マニュアル

いつも":h" や":h <調べたいキーワード>"でマニュアルを読んでいたけど、
下記にまとまっていて便利みたい。

:h user-manual 

:h howto

:h index

<br />

## vimのマニュアルを全画面で表示する

vimでマニュアルを開くと、vimのファイルから分割画面になってしまい見える範囲が狭くなって見づらい。

```
//vimを開く
$ vim
//vimのコマンドモード
:h
```


![vimhelp1](https://user-images.githubusercontent.com/43819429/133540603-e4097bce-74a0-427f-99be-1aa71ba18803.png)

<br />

解決方法：めっちゃ見づらいので全画面で表示する。

```
$ vim 
:h user-manual | only
```

上記の様に、":h <開きたいもの> | only" とすることで、vimのマニュアルが全画面で開けるようになる。


![vimhelp2](https://user-images.githubusercontent.com/43819429/133541645-e08c20a1-50a8-4d96-9d07-d0f336051510.png)

<br />

## vimのウィンドウとバッファ

メモリ上にロードされたファイルのことをバッファと呼ぶ。
バッファにはファイル名の他に、vimによって番号も付与されている。
見えてなくても、バッファにロードされたファイルを呼び出すことができる。
バッファはvimを終了させるか、コマンドの:bwipeoutを実行することで削除できる.

ウィンドウはバッファを表示させる領域のこと。windowにはIDが付与される。
ウィンドウを閉じてもバッファは残っているという特徴がある。

## レジスタという記憶領域もある

OSのクリップボードとは別に、vm独自のレジスタという保存領域があって、yankやddした文字はレジスタに保存されている。
レジスタには格納領域に名前があるので、保存領域を指定することで、保存したりデータを取り出したり
できる。

クリップボードには保存されないので注意する。

ヘルプは下記で確認できる。

```
:h reg
```

レジスタの状態を確認するコマンド

```
:reg
```

使用例：ノーマルモードで"2pと入力すると、レジスタ2に入っている文字列をカーソルの後ろにプットする。

[レジスタについてわかりやすかった記事](https://ylabdesk.com/vim-register-commands)を参照。

<br />

## プラグインを使うとき必要なpipとは

Pip Installs Packpagesの略で、
pythonのパーケージを管理するパッケージマネージャのこと。

python3がvimで有効になっているかを確認する。

:echo has('python3')で1ならpythonが有効な状態。0なら無効となっているので  
有効にする必要がある。

### python3をvimで有効にする方法

vimrc、nvimならinit.vimファイルに下記のようにpython3のパスを指定する。

```
let g:python3_host_prog = 'C:\Python310\python.exe'
```

Arch linuxでpip3をインストールする方法

```
> sudo pacman -S python-pip
```

<br />

python3で動作させるプラグインをつかうときは、vimとpythonを
つなぐインターフェースとしてpynvimというパッケージを利用する。
ので、pip3パッケージマネージャでpynvimをインストールする。
-
```
pip3 install --user pynvim
```

--userオプションをつけることで、ユーザーレベルのディレクトリにインストールされる。

※windowsならpynvimがインストールされていなかったらこのコマンドを実行してインストールしてくれ  
といったメッセージが出るのでそのメッセージをコピペしてインストールする。

<br />

## timeoutlen

set timeoutlen=3000などとすると、設定したキーマッピングの入力を3秒間待ってくれる。  
例えば、インサートモードでescキーをjjにマッピングしているとき、jを1文字押した時点で、vimがjをマッピングの文字だと判断して、  
最初のjを押した時点からの時間を見ていて、3秒以内に2文字目のｊを押したらjjはキーマッピングだと判断してjjに割り当てられているescキーの  
動作を実行してくれる。

## ttimeoutlen

ttimeoutlenの方は、キーコードが押されてからの時間をvimが見ている。  
通常は、set ttimeoutlen=100 ミリ秒程度の短い時間がデフォルトで設定されている。もしこの設定値を5秒とかにすると次のようになる。  
set ttimeoutlen=5000 に設定し、visualモードでescキーを押すと、escキーを押すという操作に対しvimが5秒待つことになる。  
ttimeoutlenの値を上記のような長い時間に設定するのは、極端に動作が遅いターミナルでescキーを押したときにターミナルからvimに押したキーコードの値を  
送る際に、ttimeoutlen=100のような短い値だとescキーを押されてから100ミリ秒待ってからescキーに割り当てられたvimの動作をするが、  
処理の遅いターミナルだと100ミリ秒を超えて、vim側で無効になりescキーが動作しないといったことが起こる。

※1つだけのキーを押したとしても、内部的にはターミナルからvimに複数のキーコードのシーケンスとして送られる。


例1：ttimeoutlen以内の場合  

ttimeoutlen=5000待つ設定。

escキーを押してvimにescキーが送出されタイマースタート。

vimがescキーのキーコードを受け取り認識するまでに3秒かかった。

5秒後にタイムアウトとなるが、タイマーの設定時間内にvimがescキーを認識したので、escキーに相当する機能をタイムアウトとなる5秒後に実行する。


例1：ttimeoutlenを超過の場合  

ttimeoutlen=100待つ設定。

escキーを押してvimにescキーが送出されタイマースタート。

処理の遅いターミナルソフトなので、vimにescキーに相当するキーコードを送ってvimがescキーを認識するまでに3秒かかる。

キーコードのシーケンス途中で0.1秒を超過したので、escキーであることを認識しなかった。  
タイムアウトされvimは何も実行しない。


































