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

## pragma once

二重インクルードを防止するために、visual c++が自動的にこの宣言を挿入してくれる。
visual c++に特有の機能なので、他では宣言しても使えない可能性があるので注意する。

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

<br />

### 一時停止したデバッグを再開する方法

ステップイン(F11)とステップオーバー(F10)を使うことで処理を進めることができる。  
細かな動きを見ないでもいいときはステップオーバーで進める。  
ステップインで進めると関数など詳細に進めることができる。

<br />

### デバッグ結果からソースコードを修正

![result](https://user-images.githubusercontent.com/43819429/146260056-3ce46b38-b45a-4794-888f-b90ea9e430b3.png)

今のソースコードのままではゼロ除算が定義されていないのでresultがinfという値になり、  
数値で得られないことがわかる。

コンソールにresult is: infと表示されるので、ユーザーがゼロ除算してしまったよという問題点がわかるようにする。  
そのためには、ゼロ除算を適切に処理するようソースコードを修正する。

visual studioにはデバッグ中であってもソースコードを編集できるエディットコンティニューという機能があるので、  
そのままソースコードを編集する。

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
		if (oper == '/' && y == 0)
		{
			cout << "Division by 0 exception" << endl;
			continue;
		}
		else
		{
			result = c.Calculate(x, oper, y);
		}
		cout << "Result is: " << result << endl;
	}	
	return 0;
}
```

while文の中でゼロ除算が入力されたら条件分岐して例外メッセージを表示するように変更したので、  
ゼロ除算してしまったことがユーザーがわかるようになった。

例外メッセージの後にcontinue文を入れたことで、そのままループは継続できるので、次の入力を受け付ける  
状態になる。

F5キーでデバッグを再開するとソースコードの変更が自動的に反映される。  
ステップインまたはステップオーバーで進めて、ゼロ除算をコンソールから入力すると  
ソースコードの編集がちゃんと反映されており例外メッセージが表示される。

![debugfix](https://user-images.githubusercontent.com/43819429/146263340-613cc2a7-0d36-47b4-ac44-e334b6707993.png)

もし上記のデバッグ中のソースコード編集でのデバッグがうまく動いてくれないときはいったん"デバッグの停止"ボタンで中止をして  
再度F5キーでデバッグを再開させる。

<br />

---

### visual studioのソースコードをgitで管理する

visual studioの右下にある"ソース管理に追加"をクリックする。

"gitリポジトリの作成"メニューが表示されるのでgithubにサインインする。

![git](https://user-images.githubusercontent.com/43819429/146285465-36ce44ae-7dc3-419d-a799-73be4f556669.png)

リポジトリの名前はPCのプロジェクトのフォルダの場所から自動的に生成される。

デフォルトでは"プライベート"のチェックボックスにチェックが入っており、プライベート  
リポジトリとなる。プライベートは、自分以外はgithub上のリポジトリは見れない設定。

作成とプッシュ"ボタンをクリック。

リポジトリの作成が完了すると、visual studioの画面下部のステータスバーに状態の詳細が表示される。

![gitstatus](https://user-images.githubusercontent.com/43819429/146285563-0fb330f1-9861-4f29-8490-ea48dbc90138.png)

上下の矢印の付いたアイコンには現在のブランチにある出力・入力方向のコミットの数が表示される。   
このアイコンを使用して入力方向のコミットをpullしたり出力方向のコミットをpushしたりできる。  
出力・入力のコミットを表示することもできる。 アイコンを選択しメニューから表示させるメニューを選択する。

鉛筆のアイコンはコードに対する確定されてない変更の数を示している。  
このアイコンを選択すると"Git 変更"ウィンドウが立ち上がり、変更が表示される。

























