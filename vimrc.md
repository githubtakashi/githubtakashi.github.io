# vimrcについてのメモ

主にvimrcの設定内容についてメモ。
どこかからコピペして作ることが多く、内容がわからないまま設定している項目も多いので、
設定した内容についてメモや説明など。基本的に便利だと思って実際に設定する設定だけメモする。

<br />

## set number

vimの左側に行番号を表示する。

## syntax on

プログラミング言語など内容に合わせて色を変えて表示されるのでソースコードが見やすくなる。

## set incsearch

文字の検索を入力している途中で候補が表示される。

## set hlsearch

検索でヒットした文字を強調表示する。
検索後もハイライトされたままやウザいみたいなのを見かけるので設定はしない。
あとで忘れてまた設定してしまいそうなのでメモとして書いておく。

<br />

## set backspace=indent,eol,start

backspaceキーが効かない場合は設定する。

indent: indentによる空白を削除
vim
eol: 行末を削除

start: カーソルよりも前(左側)の文字を削除

startについては日本語では"カーソルよりも前"と書いてあってどっちにも解釈できるので
説明がわかりにくいけど、カーソルのbefore,つまり普通のbackspaceキーの動作のこと。
vimは普通のbackspaceの動作がデフォルトでは効かなかったりする。

下記のように数値でも設定できる。

```
set backspace=0 //set backspace= と同じ
set backspace=1 //set backspace=indent,eolと同じ
set backspace=2 //set backspace=indent,eol,startと同じ
```

<br />

## set history=200

コマンドの履歴と検索履歴を200個ずつ残す。

<br />

## set ruler
現在のカーソル位置(行,列)を画面の右下にずっと表示する。

<br />

## set laststatus=2

画面最下部のステータスラインを2に設定すると常にステータスラインが表示される。

<br />

## set showcmd

入力中のコマンドの文字をステータスラインに表示する。入力が完了=コマンドが実行されると表示は消える。

<br />

## set wildmenu

コマンドを入力してtabを押したときにコマンドの候補がステータスラインに表示される。

<br />

## inoremap <C-U> <C-G>u<C-U>

insertモードで行の最後尾にカーソルがある状態で、Ctrl + u で行の文字を一括で削除できる。
便利なキーマッピング。
  
一時的にもとに戻したいときは:iunmap <C-U>とする。
  
<br />

## filetype plugin indent on
 
filetypeの検出、ファイルタイププラグインの適用、ファイルタイプに合わせたインデントの自動調整

<br />

## DiffOrigコマンド
  
下記を記述することでDiffOrigコマンドがつかえるようになる。
  
```
command DiffOrig vert new | set bt=nofile | r ++edit # | 0d_ | diffthis
                  \ | wincmd p | diffthis
```
  
下記コマンドを実行することで、差分モードで表示される。
変更前とこれから変更するファイルが同時に左右に表示され、新しく変更するとそこがハイライトされる。 
  
```
:DiffOrig
```

<br />
  
## packadd! matchit
  
デフォルトで入っているけど無効になっているmatchitプラグインを有効にする。
有効にすると、'%'キーを押したときに()だけでなくif/endifなどの組み合わせにも
ハイライトが対応できるようになる。
  
<br />






