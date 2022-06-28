# nvimを使うためのメモ

ubuntuまたはwindowsでの作業。

nvimでプラグインを使うための手順を書いていく。

## linux版のbrewをインストールする

まずaptからだといろいろパッケージが古くて困ることが多いので、brewのlinux版の  
[linuxbrewをインストール](https://docs.brew.sh/Homebrew-on-Linux)してbrewでパッケージをインストールする。

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

```

続いて下記コマンドを実行

```
test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"
test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
test -r ~/.bash_profile && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >>~/.bash_profile
echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >>~/.profile
```

コマンドを実行した結果、 ~/.bash_profile と~/.profileが両方存在している場合、いらない方を削除しておく。

.profileを使っていく場合は、下記コマンドを実行

```
source ~/.profile
```

pcを再起動したらubuntuでbrewコマンドがつかえるようになる。

<br />

## プラグインで使うためのpython管理

pyenvとpipenvと、nvm-windows(windowsの場合)、nvm(linuxの場合はgithubから)をインストールし設定していく。  
pyenvはpythonのバージョンを簡単に切り替えるためのツール。  
pipenvはpythonの仮想環境をつくるためのツール。
nvm-windowsはnode.jsのバージョンを簡単に切り替えるためのツール。

node.jsはいるの？と思ったけど、プラグインが動作するためにpythonとnode.jsの連携が必要だったりするみたい。

linuxでbrewでnvmをインストールしても何故かパスが通ってなかったりするので、[nvmのgithub](https://github.com/nvm-sh/nvm)見てインストールする。

### pyenvのインストールと設定

まずはpythonのバージョンを手軽に変更できる管理ツールであるpyenvをbrewでインストールする。

#### ubuntuにpyenvをインストール

```
brew install pyenv
//続いて下記を実施しパスを通したりする
echo 'eval "$(pyenv init --path)"' >>~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.profile
source ~/.bashrc
```

#### windowsにpyenvをインストール  

pythonの標準のパッケージ管理ツールのpipでインストールする(chocoでもできる)。  
windowsの場合はpyenv-winというパッケージが推奨されている。

```
pip install pyenv-win --target .pyenv //userディレクトリに.pyenvディレクトリを作って中にインストールされる
```

下記2つのパスを新規登録し、既存のPythonのパスがあれば、それより上に設定する。

まずユーザの環境変数を作成： 変数名=PYENV パス=C:\Users\katsuo\.pyenv\pyenv-win

そしてユーザのpathに下記を追加。  
%PYENV%\bin  
%PYENV%\shims

pyenvでインストールできるpythonを表示

```
pyenv install -l
//インストール可能なバージョンが一覧表示される
```

任意のバージョンのpythonインストール

```
pyenv install 3.10.3
```

デフォルトで使うpythonのバージョンをセットする

```
pyenv global 3.10.3
```

### pipenvのインストールと設定

pipenvをインストールする。  
pipenvは[venv](https://e-words.jp/w/venv.html)とpythonのパッケージ管理のpipがセットになったツール。

#### ubuntuにpipenvをインストール

```
brew install pipenv
```

#### windowsにpipenvをインストール

```
pip install --user pipenv //userオプションをつけることでuserディレクトリにインストールされる。
```

userオプションなしだと管理者権限の必要なpython本体のディレクトリにpipenvパッケージが  
インストールされるので、エラーがでる。


### 仮想環境専用のディレクトリをつくる

~/python_envs/nvimを作ってこのディレクトリ配下にpythonの仮想環境を  
作るようにする。同時に、pythonのパスを通すようにする。  

pipenvはデフォルトで1つのフォルダにすべての仮想環境がまとめられて、フォルダ名の中に乱数が入っていて環境によって乱数の数字が変わるため、  
乱数が変わるたびにneovimに対するpythonのpathが通らなくなりneovimからpythonが使えるようにするために毎回neovimが参照するpythonのパスを  設定しないといけない(その乱数に合致したパス名にpathを変更する必要があるため大変)。  

そのため、下記のコマンドを実行して仮想環境を仮想環境専用のフォルダの下に作るようにすることで、乱数の部分が固定の静的パスになるので、  
乱数の影響を受けなくなる。あんまりこの辺はわかってないのであくまで推測。

ubuntuの場合：

```
echo 'export PIPENV_VENV_IN_PROJECT=true' >> ~/.bashrc
source ~/.bashrc
``` 

windowsの場合：

システムの詳細メニューで、環境変数を新規作成する。  
変数名は、PIPENV_VENV_IN_PROJECT 値は、true

ちゃんと設定が反映されているかを下記コマンドで確認できる。

```
Get-ChildItem env:PIPENV_VENV_IN_PROJECT
```

システムの詳細メニューで、環境変数を新規作成する。  
変数名は、PYENV_ROOTで、値はC:\Users\takas\.pyenv

PYENV_ROOTとは、pyenvがバージョン管理するpythonが格納されるフォルダ。  
設定しておかないと、neovimがpythonがあるパスを参照できないので、:checkhealthでエラーが  
出力される。

仮想環境専用のディレクトリ~/python_envs/nvimを作成し、その中で下記コマンドを実行し、  
neovimでプラグインを使用するときに必要なpythonパッケージのpynvimをインストール。

```
pipenv install pynvim
```

以上によって、neovimが参照するpythonのpathは~/python_envs/nvim/.venv/bin/pythonとなる(あとでneovim側にパスを認識させる設定が必要)。 

#### pipenvのコマンド

仮想環境のpathが知りたい場合は、下記コマンドで確認できる。

```
pipenv --venv
```

仮想環境の削除方法：

```
pipenv --rm
```

仮想環境でpipenv shellコマンドを実行すると、仮想環境のshellが立ち上がる。  
nvimで使うだけなので使わないと思うけど、一応情報としてメモ。

仮想環境のディレクトリ内で下記コマンドを実行すると、仮想環境にインストールした  
パッケージの一覧を確認できる。

```
pipenv run pip list
```

### nvm-windowsのインストールと設定

[github](https://github.com/coreybutler/nvm-windows/releases)からsetup.zipをダウンロードしてインストーラーを実行するとインストールできる。

下記コマンドでバージョンが表示されたらok。

```
> nvm version
```

※wsl2でのubuntuの場合、brewからインストールでよさそう。  
node.jsのバージョン管理するパッケージはnodebrewというパッケージもあるけど、nvmの方が使っている人が多いらしいのでnvmを使うのが無難そう。

```
brew install nvm
//nvmがインストールされる。されたら下記コマンドを実行(brewから実行せよとメッセージが表示されるので)
mkdir ~/.nvm
nvim .profile //.profileに下記を追加
export NVM_DIR="$HOME/.nvm"
  [ -s "/home/linuxbrew/.linuxbrew/opt/nvm/nvm.sh" ] && \. "/home/linuxbrew/.linuxbrew/opt/nvm/nvm.sh"  # This loads nvm
  [ -s "/home/linuxbrew/.linuxbrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/home/linuxbrew/.linuxbrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion

//追加したら下記コマンドを実行
source .profile
command -v nvm //commandコマンドでコマンドがインストールされているかを確かめることができる
//"nvm"と表示されたらOK
```

#### インストールできるnode.jsバージョンの一覧を確認

下記コマンドを実行すると、インストール可能なnode.jsの一覧が表示される。

```
> nvm list available
```

#### node.jsの任意バージョンをインストール

最新版をインストールしたいときは、下記コマンドで簡単にインストールできる。

```
> nvm install latest
```

任意のバージョンをインストールしたいときは、nvm install 17.9.0 のように、バージョンを引数に渡す。

#### 任意のバージョンのnode.jsをセット

インストール後、任意のバージョンを使うようにセットするには下記のコマンドを管理者権限で実行。  
バージョンの切り替え先となるパッケージがprogram files内の管理者権限が必要なディレクトリ内で  
されるので、管理者権限でコマンドを実行しないといけない。

windows terminalでは複数タブを開くことができるけど、セキュリティ上、管理者権限のタブとそれ以外の  
タブを混在できないようになっている。

そのため、スタートメニュー等から新たにpowershellを右クリックし管理者権限で開き、コマンドを実行する。

```
> nvm use 16.14.2
```

現在useしているnode.jsのバージョンを確認するには、下記のコマンドを実行する。

```
> nvm list
```

以上で、node.jsとnpmが使えるようになっている。下記コマンドでバージョンを確認し表示されたらok。

```
> node -v
> npm -v
```

#### node.jsにneovim用パッケージをインストールする必要がある

neovimというパッケージをnode.jsにインストールしとかないと、:checkhealthでnode.jsがwarning出力される。

```
npm install -g neovim
```

#### インストールしたnode.jsの任意のバージョンの削除方法

```
nvm uninstall 16.14.2
```

### perlをwindowsにインストール

chocoでchoco install strawberryperlでインストールしcpanmで下記をインストールする。

```
> cpanm -n Neovim::Ext
```

上記を実行してもwindowsではcheckhealthをパスできない。

### windows ubuntu環境でのnvim

:checkhealthでクリップボードの警告が表示され、クリップボードのツールが必要となる。

aptで下記のクリップボードツールをインストールすることで警告が解消される。

```
sudo apt install xsel
```
