## c++の基礎などメモ

c++の基礎などメモしていきます。

日本語ドキュメントがわかりやすい。

- [C++日本語ドキュメント](https://cpprefjp.github.io/)

<br />

### 関数のdefault宣言｜delete宣言

クラスを定義したときに下記メンバ関数が暗黙的(自動的)に定義される。

デフォルトコンストラクタ.  
コピーコンストラクタ.  
ムーブコンストラクタ.  
コピー代入演算子.  
ムーブ代入演算子.  
デストラクタ.  

通常だと暗黙的に定義されるものをdefault宣言、delete宣言することで暗黙的な定義に対して挙動を変えることができるイメージ。

default宣言、delete宣言を理解する前に上記に挙げたコンストラクタ類についてどんなものかを理解しておく必要がある。

<br />

#### コピーコンストラクタ

- コンストラクタとは.   
オブジェクトが生成される時に呼び出される、オブジェクトを初期化するためのメンバ関数。

コピーコンストラクタとは、例えば同じクラスのブループリントからオブジェクトを２個生成し、  
コンストラクタでオブジェクトを初期化したオブジェクトの値を使ってもう１個のオブジェクトにコピーする(仕組み・挙動の)こと。

このように、同じクラスのオブジェクトを使って初期化する時にコピーコンストラクタが使われる。

下記のサンプルコードではmain()関数の中でコピーコンストラクタによって暗黙的にposAの値がコピーされて　　
posBにセット(代入)される。

コピーコンストラクタを定義していない場合は自動的に定義が行われクラスのメンバ変数の値がそのままコピーされることになる。

下記サンプルの場合は、posBのコンストラクタはposAのZZZ posA(29, 30)のように定義していないので、ZZZ posB = posA;によって　　
クラスのメンバ変数であるposAの値がそのままコピーされることになる。

```
#include <stdio.h>

class ZZZ
{
public:
    int x;
    int y;

    ZZZ(int tmpx, int tmpy); // クラスZZZのコンストラクタ
};

//  引数付きのコンストラクタ
ZZZ::ZZZ(int tmpx, int tmpy) // <基底クラス名>::<コンストラクタ名>()
{
    x = tmpx;
    y = tmpy;
}

int main()
{
    ZZZ posA(29, 30); //  posAに対するコンストラクタ呼び出し

    ZZZ posB = posA;    //  posBに対するコピーコンストラクタ呼び出し

    printf("posB.x:%d posB.y:%d", posB.x, posB.y); // posB.x:29 posB.y:30

    return 0;
}
```

#### コピーコンストラクタを自分で定義する理由

同じクラス内でポインタのオブジェクトAがあるとし、ポインタが指し示すメモリ領域をMとする。　　
すると、オブジェクトAのデータはメモリ領域Mに存在する。

この状態でオブジェクトBがコピーコンストラクタによってオブジェクトAのデータで初期化されると、　　
オブジェクトAとオブジェクトBは同じメモリ領域Mのデータを共有していることになる。

この状態でデストラクタでどちらかのオブジェクトを削除すると、メモリ領域Mのデータが消去されるので、　　
もう片方のオブジェクトのデストラクタが実行されてメモリ領域Mのデータを削除しようとした時に既に　　
メモリ領域Mにデータが存在しないので例外エラーとなる。

そのほかにも、２つのオブジェクトで共有しているデータを片方のオブジェクトが変更してしまうと、　　
もう片方のオブジェクトにも予期しない影響が出てくる。

コピーコンストラクタ内の処理で新規でメモリ領域を作成しておくことで、メモリ領域を共有しないようにし、　　
オブジェクトごとにメモリ領域を確保するようにしておく。すると、コピーコンストラクタを使うときにデータはコピーにより　　
同じでも格納されるメモリ領域が異なるので共有による不具合を避けることができる。

```
//  コピーコンストラクタ
Neko::Neko(const Neko & neko)
{
    //  ヒープメモリを新たに確保
    nName = new char[strlen(neko.nName) + 1]();

    //  コピー元オブジェクトの猫名をコピー
    strcpy_s(nName, strlen(neko.nName) + 1, neko.nName);
}
```

<br />

##### コピーコンストラクタの定義方法

- コピーコンストラクタの書式　　

```
<クラス名>::<コンストラクタ名>(const <クラス名>& <オブジェクト名>){<コピー処理の内容>}
```

引数にconst修飾したクラスの参照型のオブジェクトを渡す。　　
言い換えると、参照しにいくクラスをconst修飾し、そのconst修飾したクラスをもとにオブジェクトを生成しそのオブジェクトを　　
引数とする。

クラスをコンスト修飾しておくことで、参照するクラスのメンバが勝手に書き換えられないことを保証する。　　
もしコピーコンストラクタが参照するクラスのメンバが勝手に他から書き変えてしまっていると、　　
それはコピーコンストラクタにとっては、予期せぬことかもしれないので期待と違う結果になってしまうかもしれない。　

そのため、コピーコンストラクタが参照するクラスをconst修飾しておき、　コピーコンストラクタで参照するメンバが　　
他から勝手に書き換えられないようにしておく。

下記サンプルコードではコピーコンストラクタの定義をすることでコピーコンストラクタの挙動を明示している。　

```
class ZZZ
{
public:
    int x;
    int y;

    ZZZ(int tmpx, int tmpy);
    ZZZ(const ZZZ & pos);   //  コピーコンストラクタ
};

//  引数付きのコンストラクタ
ZZZ::ZZZ(int tmpx, int tmpy)
{
    x = tmpx;
    y = tmpy;
}

//  コピーコンストラクタの定義
ZZZ::ZZZ(const ZZZ & pos)
{
    x = pos.x;
    y = pos.y;
}
```

<br />

#### コピーコンストラクタの使い方

コピーコンストラクタは次のように呼び出すことができる。

```
ZZZ posA(100, 200);
ZZZ posB = posA;    //  コピーコンストラクタの呼び出し
```

このサンプルコードでは、posBオブジェクトの初期化に"="演算子を使うことでコピーコンストラクタを呼び出している。  
他にも、下記サンプルコードのように()でコピーコンストラクタを呼び出すこともできる。

```
ZZZ posA(100, 200);
ZZZ posB(posA);         //  （）を使ったコピーコンストラクタの呼び出し
```

