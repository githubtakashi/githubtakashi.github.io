# kitty terminalを使うためのメモ

kittyがいい感じなので使っていきたいので設定などメモ。

os: ubuntu20.04lts

## kittyの設定もろもろ

設定ファイルの場所：  
~/.config/kitty/kitty.conf 

設定ファイルをショートカットキーで開く：  
shift + control + F2キーで設定ファイルを起動できる。

デフォルトのフォントでは間延びして見えるので、フォントを変更：  
なんでもフォントをつかえないみたいで、事前にkittyで対応フォントが決まっているらしい。

```
//kitty.conf
 font_family    Ubuntu Mono
 bold_font        auto
 italic_font      auto
 bold_italic_font auto
 font_size 11.0
```

日本語入力設定：  
デフォルトでは日本語入力ができないので、設定が必要。

~/.xprofileを作成し下記を記載。

GLFW_IM_MODULE=ibusを追加することで日本語入力できるようになる。
下記を記載したらpc再起動すると日本語入力できるようになる。

```
# ibusの設定(kitty)
export GLFW_IM_MODULE=ibus
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
```

## キーボードショートカット

基本的なものだけ記載。

コピペなど：  
shift + control + ｘやｃやｖでする。shiftがいるので注意。

透過：  
~/.config/kitty/kitty.conf

```
background_opacity 0.5
dynamic_background_opacity yes
```

透過をキーボードから調整できる。  
shift + control + aを同時押ししたあとに l で透過を強くする。    
shift + control + aを同時押ししたあとに m で透過を弱くする。  
shift + control + aを同時押ししたあとに 1 で透過をoffにする。  
shift + control + aを同時押ししたあとに d で透過をデフォルト値にする(background_opacityで設定している値)。

kitty shellの起動：  
kittyの設定やヘルプをみるためのシェル。  
shift + control + esc

window操作関係：  
新規ウィンドウを開く(分割ウィンドウになる)  shift + control + enter  
次のウィンドウにフォーカスを移動　shift + control + "]" または "["  
ウィンドウを閉じる shift + control + w

新規タブを開く shift + control + t  
タブを移動 shift + control + -> または <-
