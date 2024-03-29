# cmakeのメモ

c++のコードをvimで作成し実行ファイルを作成するにあたってcmakeを使えるようにしていく。

ファイル数個だったら自分でコンパイルしリンクして実行ファイルを作成するのは手間はそれほど
かからないけど、それ以上に増えてくると、cmakeを使うことで作業が楽になる。

CMakeLists.txt

に設定を書くことでmakefileやプロジェクトファイルを生成してくれる。

makefileに設定を書いてmakeにそれを解釈させる方法よりもcmakeの方が簡単とのこと。

- CMakeLists.txtに下記を記載する。ファイルはプロジェクトファイルのあるディレクトリに作成する。

```
project(hello)
add_executable(hello hello.cpp)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
```

project文はプロジェクトの名前にする。visual C++におけるソリューション名。
ここはあんまり気にしなくてよいみたい。

add_executable()の第一引数は実行ファイルの名前、第二引数はコンパイル対象のファイル

set()文はオプションで。警告をできるだけ出したいときのオプションを記述する。
上記はgccをコンパイラで使うときになるべく多くの警告を出すための記述。

以上を書いたらcmakeでビルドする。

cmakeで一連のファイルが生成されると元のソースファイルとビルドファイルが混在してごちゃごちゃ
するので、ビルド用のディレクトリを専用に作っておいたほうがよい。

<br />

```
> mkdir build
```

<br />

ビルドディレクトリに移動し、ビルドディレクトリでcmakeコマンドを実行し実行ファイルを生成する。
ビルドディレクトリがカレントディレクトリで、コンパイル対象のcppソースファイルがカレントディレクトリ
からひとつ上の階層にある場合は、cmake .. とする。

```
> cd build
> cmake ..

```

## スクリプトモード

Cmakeにはスクリプトモードという機能がある。

bashのようなスクリプト言語。

.cmakeという拡張子。

scriptモードの使い方は、cmake -pの引数にスクリプトファイルを渡すことで
スクリプトファイルに書いたスクリプトモードのコマンドが実行できる。

```
$ cmake -P <スクリプトファイル名>
```

スクリプトコマンドの例)
自由に設定できるメッセージの前に<mode>か<check_state>を渡すことで任意のエラーなどを
検出しその後の処理も行ってくれる。
  
messageコマンドについてのドキュメントが[こちら](https://cmake.org/cmake/help/latest/command/message.html)

```
message("hello")
message(WARNING "警告")
```

### 変数の設定方法
  
変数の設定は.cmakeのスクリプトファイルではsetコマンドで変数を定義し設定できる。

cmakeコマンドでは-Dオプションで変数を定義し設定できる。
  
```
//hello.cmake
set(NEKO "katsuo")
message(${NEKO} " " ${WORLD})
message("${NEKO} ${WORLD}")
```

実行結果(-Dオプションで変数名WORLD=worldに設定)

```
$ cmake -D WORLD=world -P hello.cmake
hello katsuo
katsuo world
katsuo world
```

以上のように、ブレースでくくった変数を展開してくれる。
  





