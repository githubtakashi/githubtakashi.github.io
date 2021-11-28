# atcoderメモ

atcoder進めていて分からなかったことなどをメモしています。

## 再帰関数についての勉強メモ

再帰関数について動作を理解することが分かりにくかったのでメモ。

### 引数に渡した値までの連続した値を合計する関数

下はatcoderの再帰についてのコンテンツに載っている再帰の例コードを引用

```
#include <bits/stdc++.h>
using namespace std;

int sum(int n) {
  if (n == 0) {
    return 0;
  }

  // sum関数の中でsum関数を呼び出している
  int s = sum(n - 1);
  return s + n;
}

int main() {
  cout << sum(2) << endl;    // 0 + 1 + 2 = 3
  cout << sum(3) << endl;    // 0 + 1 + 2 + 3 = 6
  cout << sum(10) << endl;   // 0 + 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10 = 55
}
```

<br />

- main処理の中でsum(2)を呼び出した場合の例

<br />

int n = 2;がint sum(int n);に渡され、

int sum(2)が呼び出される。

int s = sum(n - 1);より int s = sum(2 - 1);よって int s = sum(1);となる。

int s = sum(1);　n = 2;なので

return s + n = sum(1) + 2; これが保持されている。 ->(b)

<br />

int s = sum(1);の右辺sum(1);により、n = 1;がint sum(int n);に渡され

int s = sum(n - 1);がsum(1 - 1);よって int s = sum(0);となる。

return s + n = sum(0) + 1;これが保持されている. ->(a)

<br />

int s = sum(0);の右辺sum(0);により、 n = 0;がint sum(int n);に渡され

return 0;により0が返される。 よってsum(0) = 0;

int s = sum(0) = 0;なので、int s = 0;

<br />

(a)の s + n = sum(0) + 1;にsum(0) = 0;が代入されて

return 0 + 1 = 1;が返される。これは、int  s = sum(1);のとき

返される値のことなのでint s = sum(1) = 1;である。



(b)の s + n = sum(1) + 2;にsum(1) = 1;が代入されて

return 1 + 2 = 3;が返される。

もうこれで未処理のものはないので、最終的な返される値は3となる。

<br />

以上で再帰の流れが分かった。上から下にいもづる式に関数を呼び出し、
最後に下から上に向かって順に処理が戻ってくるようなイメージになる。

<br />

## ベースケースと再帰ステップ

再帰関数を構成するもので、ベースケースと再帰ステップがある。

- ベースケースは再帰呼び出ししないで完結する処理
- 再帰ステップは再帰呼び出しをしてその結果を使って処理を連鎖する

先のコードでは下記の部分がベースケース

```
int sum(int n) {
  if (n == 0) {
    return 0;
  }
```

<br />

再帰ステップは下記のブロック

```
int s = sum(n - 1);
return s + n;
```

<br />

***

### AからBまでの合計を求める関数を作成する

引数にA,Bを渡してA～Bまでの連続した整数の合計を求める関数の例

関数名をsum_rangeとする(引数はA≦B)。

sum_range(2, 5);とすると、2+3+4+5の合計を計算する関数を作成する。

2, 5という2つの引数から連続した整数を計算して合計するので、

4 = 5-1, 3 =5-2,のように、Bから1ずつ引いていけば、A～Bの間の連続する整数が計算できる。

A～Bまでの合計は 2 + 3 + 4 + 5これを表すと、(aとb-1までの連続する整数+b) が合計なので、

sum_range(a, b-1) + b;で合計が計算される。あとはb-1の部分を再帰ステップで減らしていくことで

連続した整数が求まるようになる。

ここは再帰の処理の流れに慣れていないと作ることはかなり難しいと思った。

再帰に多く触れて作って慣れることが大切とのこと。

<br />

関数名を決めて引数を決めたので、まず関数は下記のように書ける。
この中に、ベースケースと再帰ステップを記載する。

```
int sum_range(int a, int b){
//ベースケース

//再帰ステップ

}
```

<br />

上記関数の中でsum_range()を繰り返し呼び出していくので、
再帰ステップの部分にsum_range()を書けばよさそうなことがわかる。

A～Bまでの連続する整数はb-1, b-2,...のようにBから１ずつ減らしていけばいいので、再帰ステップの
sum_range()の引数に(a, b-1)を渡したらよさそう。

引数a,b = (2,5)とすると、この引数から再帰ステップでa,b-1が計算されa=2, b-1=5-1=4より再帰ステップで
sum_range(2, 4) + 5となる。ここからまた最初のsum_range(2, 4)が呼ばれ、
再帰ステップの中でsum_range(2, 3) + 4となる。
この引数の値からまた最初のsum_range(2, 3)が呼ばれ、再帰ステップのでsum_range(2, 2) + 3となる。
ここで、a==bとなったらaをリターンするようにしたらよい。


以上で未処理のsum_range()が記憶領域に格納される。

sum_range(2, 4) + 5; ->(3)

sum_range(2, 3) + 4; ->(2)

sum_range(2, 2) + 3; ->(1)

最後にa == b とならないようにするには、再帰ステップのsum_range()で
sum_range(2, 2) + 3;から最初のsum_range()に(2, 2)を渡したあとに判定をして
sum_range()の処理が終わるようにすればいいので、

if(a == b) return a;

とする。これがベースケースになる。

sum_range(2, 2)の値は2となる。

ここから、

(1)のsum_range(2, 2) + 3;より2 + 3 = 5;となる。

ここで注意したいのが、再帰ステップのsum_range(2, 2) + 3 = 5;は
sum_range(2, 3)の実行結果なことを見落とさないようにする。

当たり前だけどなかなか気づかずsum(2, 3)の値がしばらく分からなかった。

(1)からsum(2, 3) = 5;なので、

(2)のsum_range(2, 3) + 4;は5 + 4 = 9;となる。

sum_range(2, 4) = 9;なので、

(3)のsum_range(2, 4) + 5;より9 + 5 = 14;となる。


以上で未処理のものはなくなったので、14が返り値となる。

<br />

完成コードは下記

```
int sum_range(int a, int b){

  //ベースケース
　if(a == b) {
      return a;
  }

  //再帰ステップ
  return sum_range(a, b -1) + b;

}
```

<br />

***

## 配列の要素の合計を求める関数を作成

引数にint型の配列を参照で渡して、その配列の要素の合計を計算する関数を作成する。

### 引数と返り値と処理内容を決める

- 引数
- 返り値
- 処理内容

をまずは決める。

引数はvector配列を参照で渡すようにする。

返り値はint型

処理内容は、配列の全ての要素を順番に足して合計を計算する。

以上から、まず下記のコードになる。

```
int arrary_sum(vector<int> &data) {
}
```

### 再帰ステップとベースケースを作成する。

配列の要素の合計は下記のように計算できる。

(n個の配列の要素の合計) = (配列の1番目の要素) + (配列の2番目以降の要素の合計)

(n個の配列の要素の合計) = (配列のi番目の要素) + (配列のi+1番目以降の要素の合計)

i=0とすると、1番目の要素から全部の要素の合計を求めることになる。

i+1番目の部分は再帰呼び出しできる。

変数iを使って再帰呼び出しをするということは、iも関数の引数に追加してあげる必要があるので、引数iを追加する。

引数iを追加するので、再帰呼び出しする関数と再帰ステップの関数名をarray_sum_from_iに変更する。

iを再帰的に実行することで変化させるので、そのために補助関数を追加する。


```
// (補助関数)
// dataのi番目以降の要素の合計を計算する
int array_sum_from_i(vector<int> &data, int i) {
}

// dataの全ての要素の合計を計算する
int array_sum(vector<int> &data) {
  return array_sum_from_i(data, 0);
}
```

<br />

i + 1番め以降の要素の合計は再帰呼び出しすることで求める。

```
// (補助関数)
// dataのi番目以降の要素の合計を計算する
int array_sum_from_i(vector<int> &data, int i) {
  // 再帰ステップ
  int s = array_sum_from_i(data, i + 1);  // i+1番目以降の要素の合計
  return data.at(i) + s;  // (i番目以降の要素の合計) = (i番目の要素) + s
}
```

<br />

```
// (補助関数)
// dataのi番目以降の要素の合計を計算
int array_sum_from_i(vector<int> &data, int i) {
  // ベースケース
  if (i == data.size()) {
    return 0;  // 対象の要素がないので合計は0
  }
  // 再帰ステップ
  int s = array_sum_from_i(data, i + 1);  // i+1番目以降の要素の合計
  return data.at(i) + s;  // (i番目以降の要素の合計)=(i番目の要素)+ s
}
```
<br />

main関数の中のarray_sum関数を起点にして再帰処理を進めると下記のようなコードになる。

```
#include <bits/stdc++.h>
using namespace std;

// (補助関数)
// dataのi番目以降の要素の合計を計算する
int array_sum_from_i(vector<int> &data, int i) {
  // ベースケース
  if (i == data.size()) {
    return 0;  // 対象の要素がないの合計は0
  }
  // 再帰ステップ
  int s = array_sum_from_i(data, i + 1);  // i+1番目以降の要素の合計
  return data.at(i) + s;  // (i番目以降の要素の合計)=(i番目の要素)+ s
}

// dataの全ての要素の合計を計算する
int array_sum(vector<int> &data) {
  return array_sum_from_i(data, 0);
}

int main() {
  vector<int> a = {0, 3, 9, 1, 5};
  cout << array_sum(a) << endl;   // 0 + 3 + 9 + 1 + 5 = 18
}
```

<br />

配列とiをarray_sum_from_iに渡す。

int s = array_sum_from_i(data, i + 1)に渡されたiをi+1する。

data.at(i) + s;でi番目の要素であるdata.at(i)とi+1番目の要素であるsを足し算する。

例えばi=0が渡されると、int s = array_sum_from_i(data, i + 1)は(data, 1)となる。

return data.at(i) + s;ではdata.at(0) + array_sum_from_i(data, 1);となる。

int s の右辺array_sum_from_i(data, 1)から再帰呼び出しを行い、

array_sum_from_i(vector<int> &data, int i)のiに1が渡される。
  
そしてint s = array_sum_from_i(data, i + 1)にiが渡され、iは1+1=2になる。
  
この再帰を配列の一番最後まで続ける。
  
iが配列の一番最後まで増加したときにiの増加を止める必要がある。
  
例えばdata = {10, 20, 30, 40, 50}

5個の配列とすると、iは0,1,2,3,4となる。

配列の要素数は5個なので、data.size() = 5となる。
  
i == data.size()となったときは、対象の要素がないので、合計0を返すようにする。

すると、i = 5のときはreturn 0;を返すので、

array_sum_from_i(data, 5);の値は0

- return data.at(0) + array_sum_from_i(data, 1); ->(e)
- return data.at(1) + array_sum_from_i(data, 2); ->(d)
- return data.at(2) + array_sum_from_i(data, 3); ->(c)
- return data.at(3) + array_sum_from_i(data, 4); ->(b)
- return data.at(4) + array_sum_from_i(data, 5); ->(a)

最後のarray_sum_from_i(data, 5);の値は0なので、

(a)の値はdata.at(4) + 0 = 50;

つまりint array_sum_from_i(vector<int> &data, int 4)の実行結果が50。
  
(b)のarray_sum_from_i(data, 4);は上記と同じなので、値は(a)の値である50となる。
  
よって(b)は return data.at(3) + data.at(4) + 0;

同様にして、(c)のarray_sum_from_i(data, 3);は(b)のint array_sum_from_i(vector<int> &data, int 3)の実行結果
  
data.at(3) + data.at(4) + 0である。

よって、(c)は return data.at(2) + data.at(3) + data.at(4) + 0;
  
同様にして、(d)のarray_sum_from_i(data, 2);は(c)のint array_sum_from_i(vector<int> &data, int 2)の実行結果
  
data.at(2) + data.at(3) + data.at(4) + 0である。

よって、(d)は return data.at(1) + data.at(2) + data.at(3) + data.at(4) + 0;

同様にして、(e)のarray_sum_from_i(data, 1);は(d)のint array_sum_from_i(vector<int> &data, int 1)の実行結果
  
data.at(1) + data.at(2) + data.at(3) + data.at(4) + 0である。

よって、(e)は return data.at(0) + data.at(1) + data.at(2) + data.at(3) + data.at(4) + 0;

以上の流れで合計値が求まる。

<br />

***
  
## Nが素数であるかを判定する再帰関数を作成

- 素数とは、1より大きい自然数で、1とその数自身の2つしか約数が存在しない数のこと。
  
- 1は約数を2つ持たず、素数の定義に当てはまらないので素数ではない。
  
以上を踏まえて、正の整数Nが素数であるかを判定する関数を作成する。

<br />
  
素数をプログラムで判定する方法として、
  
Nを1とNを除いた、2からN-1までの数で順番に割っていき、割り切れなかったら、
  
そのNは1とN自身でしか割り切れないことになるので、素数であると判定できる。
   
<br />

例えば、N/i = 4/1=4, 4/2=2, 4/3=1余り1, 4/4=1となり、
  
１と4以外の数である2で割り切れているので4は素数ではない。
  
どんなNもN自身と1は割り切れるので処理から除外するので、2～N-1までの数

で割っていくことになり、割り切れたら約数が存在するので素数ではないことが分かる。
  
なのでN=4の場合はi=2～3の範囲で約数が存在するかを判定することになる。
  
<br />
  
プログラムでNがiで割り切れるかどうかを判定する方法としては、
  
N % iが0かどうかで判定する。
 
N=4のケースでは、i=2のとき、4%i = 4%2 == 0;となり、
  
割り切れるので4は素数ではないことが明らかになる。

<br />

iからN-1の範囲にNの約数が存在するかを判定する補助関数の名前をhas_divisorとする。
  
has_divisorという関数名は、Nを割り切れる数を持っているかどうかを判定する関数なのでこの名前。

約数が存在する場合と存在しない場合のどちらかが分かればよいので
  
has_divisor関数は、返り値としてtrueかfalseを返すようにする。
  
<br />

### 引数、返り値、処理内容を決める

補助関数has_divisorに渡す引数Nを考える。

Nとして1を渡す場合、1は素数でないが、1を引数として渡してしまうと、
  
iからN-1の範囲にNの約数が存在するかを判定するhas_divisor関数の処理に

合わないので1が渡された場合はhas_divisor関数で扱わずメインの関数で処理し、素数ではないと判定する。
  
この処理は1回で完結するのでベースケースとなる。
  
Nとして2を渡す場合、2は素数だけど、N=2を渡すとi=N-1=1となり1でしか割れないので、i～N-1までの間の数が無いので、
  
has_divisor関数の処理に合わないので2が渡された時もhas_divisor関数で扱わずメインの関数で処理し、
  
ベースケースとして素数であると判定するようにする。
  
<br />
  
以上から、メインの関数であるis_prime関数(素数は英語でprime number)で
  
引数Nについて、N=1,2,または3以上の選別を行い、
  
引数がN≧3である場合(1でも2でもない場合)は補助関数has_divisorを呼び出して素数であるかを判定する。

has_divisor関数で再帰呼び出しによる再帰ステップでiをインクリメントしつつNをiで割っていく。

割り切れた時点で、約数が存在し素数ではないことを意味するtrueを返り値として返す。
  
割り切れた時点で再帰ステップが終わるので割り切れるかの計算はベースケースとなる。
  
割り切れず再帰ステップでiをインクリメントしていき最終的にi==Nとなった場合は、
  
割り切れる数が存在しなかったことを意味しているので、約数が存在せず素数であることを意味するfalseを返す。
  
i==Nという条件判定も再帰ステップがここで終わるのでベースケースとなる。
  
以上から、下記のようなソースコードになる。
  
<br />
  
```
#include <bits/stdc++.h>
using namespace std;

// i ~ N-1の範囲にNの約数が存在するか
bool has_divisor(int N, int i) {
  // ベースケース1
  if (i == N) {
    return false;
  }
  // ベースケース2
  if (N % i == 0) {
    // 実際にiはNの約数なので、i ~ N-1の範囲に約数が存在する
    return true;
  }

  // 再帰ステップ
  // i+1 ~ N-1の範囲の結果がi ~ N-1の範囲の結果となる
  // (ベースケース2によって、iがNの約数の場合は取り除かれているので、あとはi+1 ~ N-1の範囲を調べればよい)
  return has_divisor(N, i + 1);
}

bool is_prime(int N) {
  if (N == 1) {
    // 1は素数ではない
    return false;
  }
  else if (N == 2) {
    // 2は素数
    return true;
  }
  else {
    // 2~(N-1)の範囲に約数が無ければ、Nは素数
    return !has_divisor(N, 2);
  }
}

int main() {
  cout << is_prime(1) << endl;  // 0
  cout << is_prime(2) << endl;  // 1
  cout << is_prime(12) << endl; // 0
  cout << is_prime(13) << endl; // 1
  cout << is_prime(57) << endl; // 0
}

```
  
<br />
  
***

## 配列を逆に並べ替える再帰関数を作成

vector配列から参照渡しで渡した要素を逆順に並び替える関数を再帰処理で作成。

要素を逆順に並び替える関数名をreverse_arrayとする。

まずmainの処理は下記のようになる。
  
並び替える元データとなるvector配列を作成。
  
その元データの配列をreverse_arrayに渡す
  
逆順の処理を実行し逆順に並び替える。
  
逆順の結果を出力する。
 
<br />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  vector<int> a = {1, 2, 3, 4, 5};
  vector<int> b = reverse_array(a);
  for (int i = 0; i < b.size(); i++) {
    cout << b.at(i) << endl;
  }
}
```
                           
<br />

次は逆順に並び替える関数reverse_arrayを作成する。

reverse_arrayは配列aを参照で受け取るので引数はvector<int> &dataとする。

参照で受け取った配列を逆順に並び替える処理を実装する。

a = {1, 2, 3, 4, 5}

を並び替えた要素を格納するvector配列を準備する。

vector<int> b = reverse_array(a);

a = {1, 2, 3, 4, 5}のデータが下記に参照される。
  
vector<int>配列reverse_arrayは上記のa = {1, 2, 3, 4, 5}

を参照する。
  
reverse_array関数の補助関数をreverse_array_from_iとし、この間数で
  
再帰処理を行い要素を逆順に並び替える。

vector<int> reverse_array(vector<int> &data) {
  return reverse_array_from_i(data, 0);
} 

a = {1, 2, 3, 4, 5}を処理するため補助関数reverse_array_from_iに

a = {1, 2, 3, 4, 5}を渡す。第二引数にi=0を渡す。

これによってreverse_array_from_iの処理に入る。
  
reverse_array_from_iもvector<int>型の配列。

まず引数として受け取ったdataのa = {1, 2, 3, 4, 5}とi=0を元にして処理を進める。
  
i = 0; data.size == 5なので下記のif文は実行されない。

```
if (i == data.size()) {
    vector<int> empty_array(0);  // 要素数0の配列
    return empty_array;
  }
```

a = {1, 2, 3, 4, 5}, i + 1 = 0 + 1 = 1が下記のvector<int>配列tmpに渡される。

vector<int> tmp = reverse_array_from_i(data, i + 1); 
  
逆順に並び替えた要素を格納するvector<int> tmp はint型の配列で、
  
最初はtmp = {}のような空の配列となる。

tmp = {}の中に右辺のreverse_array_from_i(data, i + 1);の結果を格納していくことになる。

ここで、右辺reverse_array_from_i(data, i + 1);は再帰処理となる。
  
tmp.push_back(data.at(i));でtmp = {} の中にdata.at(i)の要素を格納する。
  
例えばi = 0の場合、data.at(0) = 1がtmpに格納される。
  

再帰処理でたまっていくスタック
  
vector<int> tmp = reverse_array_from_i(data, 1);
tmp.push_back(data.at(0));
  
vector<int> tmp = reverse_array_from_i(data, 2)
tmp.push_back(data.at(1)); 

vector<int> tmp = reverse_array_from_i(data, 3)
tmp.push_back(data.at(2));
  
vector<int> tmp = reverse_array_from_i(data, 4)
tmp.push_back(data.at(3));

i = 4のとき、下記の流れで処理される。
vector<int> tmp = reverse_array_from_i(data, 5)
  
if (i == data.size()) {
    vector<int> empty_array(0);  // 要素数0の配列
    return empty_array;
}

i = 5, data.size() = 5となり、i == data.size()なのでif文の中身が実行される。

要素数0の配列すなわち0をリターンすることでreverse_array_from_iの再帰の繰り返しが終了する。
  
reverse_array_from_iの実行結果が結局empty_array(0)で、空の配列となる。
  
すなわち、vector<int> tmp = reverse_array_from_i(data, i + 1);
  
の実行結果はvector<int> tmp =　empty_array；となり、空の配列となる。

ここで、未処理のスタックに格納された処理が実行されていく。

スタックなので、一番最後のスタックから順に実行されていく。

```
tmp.push_back(data.at(4)); // tmp = {5}
tmp.push_back(data.at(3)); // tmp = {5,4}
tmp.push_back(data.at(2)); // tmp = {5,4,3}
tmp.push_back(data.at(1)); // tmp = {5,4,3,2}
tmp.push_back(data.at(0)); // tmp = {5,4,3,2,1}
return tmp;
```

tmp = {5,4,3,2,1}が最終的にリターンされる。これがreverse_array_from_i
  
の実行結果、すなわちreverse_arrayの実行結果になる。
  
よって、vector<int> b = reverse_array(a);の実行結果は
  
b = {5,4,3,2,1}となり、あとはfor文で要素を出力して完了。
  
完成のソースコードは下記となる。

```
#include <bits/stdc++.h>
using namespace std;

// dataのi番目以降の要素を逆順にした配列を返す
vector<int> reverse_array_from_i(vector<int> &data, int i) {
  // ベースケース
  if (i == data.size()) {
    vector<int> empty_array(0);  // 要素数0の配列
    return empty_array;
  }

  // 再帰ステップ
  vector<int> tmp = reverse_array_from_i(data, i + 1);  // dataのi+1番目以降の要素を逆順にした配列を得る
  tmp.push_back(data.at(i));  // 末尾にdataのi番目の要素を追加
  return tmp;
}

// 配列を逆順にしたものを返す
vector<int> reverse_array(vector<int> &data) {
  return reverse_array_from_i(data, 0);
}

int main() {
  vector<int> a = {1, 2, 3, 4, 5};
  vector<int> b = reverse_array(a);
  for (int i = 0; i < b.size(); i++) {
    cout << b.at(i) << endl;
  }
}
```

***
                          
## 報告書の伝達時間を再起関数で作成

N個の親組織と子組織があって、親以外は全ての組織が1つ以上親を持っているフォルダみたいな構造の組織とする。
                                                  
子から親に報告書を送る時間が1分のとき、報告書がトップの親に届くまで何分かかるかという問題。

トップの組織は0番で表す。

```
入力

6

0 0 1 1 4

出力

3
```

- 入力値の意味

入力していった順が組織の番号を表していて、数字はその組織の親組織の番号を表している。
                           
1番目の組織の親組織は0番
 
2番目の組織の親組織は0番

3番目の組織の親組織は1番
                           
4番目の組織の親組織は1番

5番目の組織の親組織は4番

図に書くと木構造になっている。木構造について処理をするときには再帰関数が役立つ場合が多い。

<br />

### メインの処理の流れを作成する

int main() の中身をざっくり作成していく。

入力値Nは組織の数。これを入力で受け取る。

親組織の番号を入力していった順が組織の番号を表している。
  
0番目はトップかつ親が存在しないので入力で受け取る必要はないので省く。
  
N=6の場合は組織番号1から5までの5個の組織について、親組織の番号を入力することになる。

組織番号1から5までの組織の親組織の番号を格納する配列を作成する。
  
この配列は配列の添え字が組織番号を示していて、要素が親組織の番号を意味している。
  
この配列を作成するとき、くどいけどトップ組織を意味する配列の0番目には親組織は存在しないので値として-1を代入しておく。
  
そして入力からは添え字i=1から5までを受け取り要素を格納するようにする。
  
ここまでのソースコードは下記のようになる。
  
<br />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int N;
  cin >> N;
  
  vector<int> p(N);//組織番号と親組織の番号を示す配列
  p.at(0) = -1;//0番組織はトップ組織で親組織は存在しないので-1を代入しておく
  
  //配列に組織(添え字)と親番号を格納
  for (int i = 1; i < N; i++) {
      cin >> p.at(i);
  }
}
```

<br />
 
親組織の子組織を上から順に、親組織－子組織－子組織...という関係で格納できる配列を作成する。

子組織の一覧という意味合いで、配列名をchildrenとする。この配列を2次元配列にすることで、
  
一覧表の形式で配列を作成できる。

vector pに格納した1番目の組織から順に、親組織の番号をint型の変数parentに代入する。
  
例の場合は、組織番号i=1の親組織番号0をparent変数に代入する。
  
そして、childre.at(parent).push_back(i);とする。
  
children.at(parent)のparent=0なので、children.at(0)となる。
  
配列pは組織番号と親組織の対を意味しているので、組織1の親組織0

組織2の親組織0

i=1なのでpush_back(1)となり、children.at(0).push_back(1)であり、0の行に1が挿入される。

次のループに入る。i=2, parent=p.at(2)となる。ここで、p.at(2)は0なので、parent=0となる。

children.at(0).push_back(2)となり、0の行に2が挿入される。
  
ここまでで、children配列の0の行(トップ組織に紐づく子組織)の一覧は{0, 1, 2}となる。
 
次のループに入る。

i=3, parent=p.at(3)となる。ここで、p.at(3)は1なので、parent=1となる。
  
children.at(1).push_back(3)となり、1の行に3が挿入される。
  
次のループに入る。
  
i=4, parent=p.at(4)となる。ここで、p.at(4)は1なので、parent=1となる。
 
children.at(1).push_back(4)となり、1の行に4が代入される。
  
ここまでで、children配列の1の行(トップ組織に紐づく子組織)の一覧は{1, 3, 4}となる。
  
次のループに入る。

i=5, parent=p.at(5)となる。ここで、p.at(5)は4なので、parent=4となる。
  
children.at(4).push_back(5)となり、4の行に5が代入される。
  
ここまでで、children配列の4の行(トップ組織に紐づく子組織)の一覧は{4, 5}となる。
  
i=6となる。6 > N=5なのでループを抜ける。
  
以上で親組織と子組織の一覧が得られる

コードは下記のようになる。
  
```
// 組織の関係から2次元配列を作る
vector<vector<int>> children(N);  // ある組織の子組織の番号一覧  // N×0の二次元配列
  for (int i = 1; i < N; i++) {
    int parent = p.at(i);  // i番の親組織の番号
    children.at(parent).push_back(i);  // parentの子組織一覧にi番を追加
  }
```





 




   
