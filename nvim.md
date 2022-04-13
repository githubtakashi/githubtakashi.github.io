# nvimを使うためのメモ

ubuntuでの作業

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

コマンドを実行した結果、~/.bash_profileと~/.profileが両方存在している場合、いらない方を削除しておく。

.profileを使っていく場合は、下記コマンドを実行

```
source ~/.profile
```

pcを再起動したらubuntuでbrewコマンドがつかえるようになる。

<br />

## プラグインで使うためのpython管理

pythonのバージョンを手軽に変更できる管理ツールであるpyenvをbrewでインストールする。

```
brew install pyenv
//続いて下記を実施しパスを通したりする
echo 'eval "$(pyenv init --path)"' >>~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.profile
source ~/.bashrc
```

windowsにpyenvをインストールする方法：  
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

pipenvのインストール

```
brew install pipenv
```

pipenvは[venv](https://e-words.jp/w/venv.html)とpythonのパッケージ管理のpipがセットになったツール。


仮想環境専用のディレクトリをつくる。~/python_envs/nvimを作ってこのディレクトリ配下にpythonの仮想環境を  
作るようにする。同時に、pythonのパスを通すようにする。  


pipenvはデフォルトで1つのフォルダにすべての仮想環境がまとめられて、フォルダ名の中に乱数が入っていて環境によって乱数の数字が変わるため、  
乱数が変わるたびに、neovimに対するpythonのpathが通らなくなり、neovimでpythonが使えないので、  
その乱数に合致したパス名にpathを変更する必要があるため大変。  
そのため、下記のコマンドを実行して仮想環境を仮想環境専用のフォルダの下に作るようにすることで、乱数の部分が固定の静的パスになるので、  
乱数の影響を受けなくなる。あんまりこの辺はわかってないのであくまで推測。

```
echo 'export PIPENV_VENV_IN_PROJECT=true' >> ~/.bashrc
source ~/.bashrc
```

仮想環境専用のディレクトリ~/python_envs/nvimの中で下記コマンドを実行し、  
neovimに必要なpythonパッケージのpynvimをインストール。

```
pipenv install pynvim
```

以上によって、neovimが参照するpythonのpathは~/python_envs/nvim/.venv/bin/pythonとなる。

