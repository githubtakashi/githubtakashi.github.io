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
  
素数を判定する方法として、Nを2からN-1までの数で割っていき、割り切れる数が
  
あったらそのNは素数であると判断できる。
  
なので、Nに対し、iからN-1の範囲で順に割っていき、割り切れたらそれが約数なので、
  
iからN-1の範囲でNの約数が存在するかを判定する。
  
<br />

例えば、N/i = 4/1=4, 4/2=2, 4/3=1余り1, 4/4=1となり、
  
１と4以外の数である2で割り切れているので4は素数ではない。
  
どんなNもN自身と1は割り切れるので処理から除外するので、2～N-1までの数

で割っていくことになり、割り切れたら約数が存在するので素数ではないことが分かる。
  
なのでN=4だったら、i=2～3の範囲で約数が存在するかを判定する。
  
<br />
  
2または3で割り切れる場合は約数が2つ以上存在することになり、素数ではないことが明らかになる。
  
N=4のとき、素数かどうか判定するには、i=1,4では当然割り切れるので、
  
i=2,3で割り切れるかを検証する。
  
N=4のケースでは、i=2のとき、4%i = 4%2 == 0;となり、
  
割り切れるので4は素数ではないことが明らかになる。

<br />

iからN-1の範囲にNの約数が存在するかを判定する補助関数の名前をhas_divisorとする。
  
has_divisorという関数名は、Nを割り切れる数を持っているかを判定する関数なので、この名前が適当。

約数が存在する場合は素数ではない。存在しない場合は素数である。
  
⇒has_divisorは、返り値としてtrueかfalseを返すようにする。
  
<br />

### 引数、返り値、処理内容を決める

補助関数has_divisorに渡す引数Nを考える。

1は素数でないが、1を引数として渡してしまうとiからN-1の範囲にNの約数が存在するかを判定する関数に

そもそも合わないので1が渡された場合は素数ではないと判定する。
  
2は素数。N=2を渡すとi=N-1=1となり1でしか割れないので、i～N-1までの間の数が無いので、
  
2が渡された時もベースケースとして素数であると判定するようにする。
  
<br />
  
以上から、メインの関数であるis_prime関数(素数=prime number)で
  
引数Nについて、N=1,2,または3以上の選別を行い、
  
引数がN≧3である場合(1でも2でもない場合)は補助関数has_divisorを呼び出して素数であるかを判定する。

has_divisor関数では再帰呼び出しによる再帰ステップでiをインクリメントしつつNをiで割っていく。

割り切れた時点で素数でないと確定し約数が存在することを意味するtrueを返り値として返す。
  
割り切れた時点で再帰ステップが終わるので割り切れるかの計算はベースケースとなる。
  
割り切れず再帰ステップでiをインクリメントしていき最終的にi==Nとなった場合は、
  
割り切れる数が存在しなかったことを意味しているので、Nは素数であることが確定し約数が存在しないことを意味するfalseを返す。
  
これもi==Nという条件判定も再帰ステップがここで終わるのでベースケースとなる。
  
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
