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

### メイン関数に処理を追加する

作成したCalculateクラスをメイン関数の中から呼び出し使う。

```
#include <iostream>
#include "Calculator.h"

using namespace std;

int main()
{
	double x = 0.0;
	double y = 0.0;
	double result = 0.0;
	char oper = '+';

	cout << "Caluculator Console Application" << endl << endl;
	cout << "Please enter the operation to perform. Format: a+b | a-b | a*b | a/b" << endl;
	
	Calculator c;
	while (true) 
	{
		cin >> x >> oper >> y;
		result = c.Calculate(x, oper, y);
		cout << "Result is: " << result << endl;
	}	
	return 0;
}
```

C++のプログラムは常にmain()関数から始まって、そこから他のコードを呼び出す必要がある。   
#include ステートメントによってほかのコードを呼び出すことができる。

Calculator c; はCalculatorクラスのインスタンスとしてcというオブジェクトを宣言。  
このクラス自体(Calculatorクラス)は、電卓がどのように機能するかを示すただのブループリントにすぎない。  
ブループリントから生成したオブジェクトcが実際に計算を実行する特定の電卓となる。

whileの条件は単にtrueと指定しているため、常にtrueになり無限ループとなる。　　
無限ループのプログラムを閉じるには、ユーザーが手動でコンソールウィンドウを閉じたらよい。
それ以外の場合はプログラムは常に新しい入力を待機していることになる。

プログラムをビルドしてデバッグなしで実行をすると、コンソールが立ち上がり入力が促されるので  
入力すると計算がされ結果が表示される。

![calculateresult](https://user-images.githubusercontent.com/43819429/146174554-5af146c1-bf98-49fc-882a-f2d28dfe94d8.png)

<br />

### 作成した電卓アプリをデバッグする

ユーザが自由に入力できてしまう状態なので、ユーザが入力したデータが想定に収まるように改善が必要。  
visual studioではプログラムを実行するかわりにデバッグして実行内容を詳細に確認することができる。

<br />

#### ブレークポイントの設定方法

ブレークポイントを設定する。ブレークポイントを任意の行に設定すると、そこで処理が止まるように  
なる。ブレークポイントは画像のようにグレーの縦線の部分をクリックするだけで設定できる。  
赤い点がブレークポイント。

![breakpoint](https://user-images.githubusercontent.com/43819429/146176810-e685ef0e-91db-4b21-bc98-01facbcddbeb.png)

特定の条件に当てはまるときだけ実行を一時停止させたいときは、条件付きのブレークポイントを設定する。

ブレークポイントの赤丸を右クリックし "条件" を選択。 
条件の編集ボックスに "(y == 0) && (oper == '/')" と入力し"閉じる"ボタンを選択。

以上によりゼロで除算したときだけブレークポイントで処理がストップするようになる。

デバッグを開始するには、"ローカル Windowsデバッガー"をクリック。  
するとコンソールアプリが立ち上がるので、任意の計算を入力。

y == 0 && oper == /でゼロ除算を入力したときだけ処理がブレークポイントで止まる。

例えば1/0と入力した場合は、"自動"ウィンドウに処理が止まった時の変数の値が表示される。

![debug](https://user-images.githubusercontent.com/43819429/146244312-40887164-8d6e-4eb3-b8e7-743826a325b6.png)

コード内の変数にマウスカーソルのポインターをフォーカスすると、実行が一時停止されている現在の値を確認することもできる。 












