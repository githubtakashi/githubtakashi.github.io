# visual studio2022のメモ

visual studio2022 C++を使ってvisual studioを勉強する。

hello world

c++のコンソールアプリを作成する。

デフォルトでhello worldのコードが準備されている。

新規プロジェクトでc++コンソールアプリを指定して作成。

<br />

## プロジェクトとソリューションとは

1つ以上の関連するプロジェクトを包むコンテナがソリューション。  
ソリューションはプロジェクトを入れるディレクトリと同じ。

<br />

## ビルドとデバッグ

ビルドしただけでは何も実行されない。  
デバッグ、またはデバッグなしで実行をすると実行できる。

<br />

## #include

#includeは<>で囲むのはは標準ライブラリの場合。  
""で囲むのは標準ライブラリ以外の他のファイルをインクルードしたいとき。

<br />

## using namespace std

このファイルにC++ 標準ライブラリの内容が使用されることを想定するようコンパイラに指示する。   
この行を含めない場合ライブラリの各キーワードの前に std:: を付けてそのスコープを示す必要がある。  
using namespace std宣言をすることでstd::の部分を省略できるのでコードを書くのが楽になる。

<br />

## cout << endl

coutはc++の標準出力に出力するために使用。  
<< 演算子はその右側のすべてを標準出力に送信するようコンパイラに指示する。  
endlはEnterキーのようなもので、その行を終了しカーソルを次の行に移動する。   
endlを使うと常にバッファーがフラッシュされるため、プログラムのパフォーマンスが低下する。  
endlと同等の処理として文字列内に\nを配置することでendlによるパフォーマンスの低下を避けられる。

<br />

## Calculatorアプリの作成

main()関数の中身を作成

```
#include <iostream>

using namespace std;

int main()
{
	cout << "Caluculator Console Application" << endl << endl;
	cout << "Please enter the operation to perform. Format: a+b | a-b | a*b | a/b" << endl;
	return 0;

}
```

次に、計算を実行するクラスを作成し追加する。

"プロジェクト" -> "クラスの追加" を選択する。

任意のクラス名を名付けて"ok"をクリックする。

![classadd](https://user-images.githubusercontent.com/43819429/146111701-dcc13c5d-e128-4e28-81f5-a26a40197e57.png)

クラス名と同じhヘッダーファイルとcppファイルが作成される。

ヘッダーファイルにクラスの関数や変数の名前と型の定義(プロトタイプ宣言)を書き、  
ソースファイルのcppファイルに処理の実装を書くのが標準的な作成方法。

<br />

### プロトタイプ宣言の効果

.hヘッダーファイルは、関数のプロトタイプを宣言。プロトタイプ宣言することで、必要なパラメーターとそれから返される  
戻り値の型をコンパイラに事前に知らせておける。

<br />

### 単純なソースコードの場合はコンストラクタとデストラクタは省略できる

コンストラクタとデストラクタは単純なクラスでは省略してもコンパイラが自動的に作成してくれる仕組みとなっている。

<br />

### ファイルは細かい単位で分けたほうがよい

ファイルはなるべく複数のファイルに分けたほうがメンテナンス性がよい。

<br />

### ヘッダーファイルからソースファイルにクラスを追加

ヘッダーファイルにクラス定義を書いた時点では、ソースファイルにまだクラスを作成していないのでクラス名の下に  
波線が表示される。クラス名の単語にマウスカーソルのポインターをフォーカスする。  
すると、ねじみたいな表示が出るので、そこで"Create definition of 'Calculate' in Calculator.cpp  
calculator.cpp で 'Calculate' の定義を作成"を選択する。

![classadd2](https://user-images.githubusercontent.com/43819429/146159101-d09a7b98-d10f-4534-ba2b-3b4262bbee8e.png)


すると、cppのソースファイルにCalculateクラスが自動的に追記される。

![calculateクラスの追加](https://user-images.githubusercontent.com/43819429/146160942-4830ecd6-c9a2-4a01-b9c2-d2a4258e7bb1.png)

<br />

### Calculateクラスにソースコードを記載する

Calculator.cppにCalculateクラスの実装としてswitch文で引数に渡された演算子に応じて  
計算を行うソースコードを記載する。

```
#include "Calculator.h"

double Calculator::Calculate(double x, char oper, double y)
{
	switch (oper)
	{
		case '+':
			return x + y;
		case '-':
			return x - y;
		case '*':
			return x * y;
		case '/':
			return x / y;
		default:
			return 0.0;
	}
}
```

戻り値の型(クラスの型)をdouble型にしておくことで、小数と整数どちらの引数にも対応できる。



