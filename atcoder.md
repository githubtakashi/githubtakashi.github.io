# atcoderメモ

atcoder進めていて分からなかったことなどをメモしています。

## 再帰関数について

再帰処理についてとても分かりにくかったのでメモ。

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

