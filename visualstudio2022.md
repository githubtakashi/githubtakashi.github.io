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




