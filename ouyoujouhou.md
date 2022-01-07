<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
 MathJax.Hub.Config({
 tex2jax: {
 inlineMath: [['$', '$'] ],
 displayMath: [ ['$$','$$'], ["\\[","\\]"] ]
 }
 });
</script>

# 応用情報技術の勉強ノート

応用情報の勉強ノートを書いていく。  
応用情報の参考書の2周めに入って最初の方のページを見たら勉強したことをすっかり忘れているので  
ノートを書く。

<br /> 

## 論理と集合

論理演算は集合で考えると分かりやすい。

- 論理和、論理積、排他的論理和、論理否定がある

論理和はOR, 論理積はAND, 排他的論理和はXORまたはEOR, 論理否定はNOT。

論理和はx+y, 論理積はx・y, 排他的論理和はx$\oplus$y,論理否定はx$\lnot$

<br />

### 論理演算の結果

x,yが0か1の値のとき、論理演算の結果は次のようになる。  
集合のベン図で考えると理解しやすい。  
0でベン図を塗りつぶさず、1でベン図を塗りつぶすと考える。  

<br />

#### 論理和

x,yのいずれかが1のとき1になる。

ベン図で考えるとわかりやすい。論理和x+yは、集合ではxとyの和集合と同じ考え方。
和集合のベン図で考えるとx,yの少なくとも片方が1であれば1となる。

<br />

#### 論理積

xもyも両方とも1のとき1になる。  
集合のベン図で考えると、論理積x・yはxとyの積集合なので、xとyの集合の共通部分と同じ考え方。

積集合で考えると、xもyも1じゃないと積集合が存在しないので、論理積はxもyも1のときだけ1となる。

<br />

#### 排他的論理和

xかyのどちらかだけ1のとき1になる。  
論理和に"排他的"という条件を加えたものと考えるとわかりやすい。  
集合のベン図で考えると、xとyの共通部分を除いたxまたはyの部分が排他的論理和に該当する。

xもyも1のときは、ベン図でイメージすると排他的論理和に該当する部分は存在しないので、出力は0となることが特徴なので覚えておく。


![排他的論理和](https://user-images.githubusercontent.com/43819429/148319117-4fb019d7-f76c-4630-bdf9-d43cadc692fc.png)

<br />

#### 論理否定

論理否定は集合のベン図がもろわかりやすい。  
集合xの否定はxバー(あとでlatexなどで書く)

<br />

### 論理演算の基本公式

パット見普通の計算とごっちゃになり訳が分からなくなりがち。普通の四則演算とは意味が違うので注意。

論理演算の基本公式として、0と1の演算、同一の法則、交換法則、結合法則、分配法則、吸収法則、ド・モルガンの法則がある。

#### 0と1の演算

$x\cdot0 = 0$

xが0でも1でも結果は0になることを表している。  
論理積なので、x,yのどちらかが0のときは論理積は0になる。x,yの両方とも1のとき1になるから。

<br />

$x\cdot1 = x$

y=1ならば、xの値がそのまま論理積の結果になることを表している。  
論理積なのでx=0のときは$0\cdot1=0$,x=1のときは$1\cdot1=1$になる。

<br />

x+0=x

論理和なので少なくともx,yのどちらかが1だったら結果は1になる。  
y=0なのでx=0だったら結果は0、x=1だったら結果は1になる。

<br />

x+1=1

論理和なので少なくともx,yのどちらかが1だったら結果は1になる。  
y=1なのでx=0か1にかかわらず結果は1になる。

<br />

#### 同一の法則

$x \cdot x=x$

論理積なので、x=0のときは$0\cdot0=0$,x=1のときは$1\cdot1=1$になり、xの値がそのまま結果となる。

<br />

x+x=x

論理和なので、x=0のときは0+0=0, x=1のときは1+1=1になり、xの値がそのまま結果となる。

<br />

#### 交換法則

$x \cdot y = y \cdot x$

x+y = y+x

これは位置を前後しただけ。

<br />

#### 結合法則

- 論理積の結合法則

$x \cdot (y \cdot z) = (x \cdot y) \cdot z$

左辺：xと(y,zの論理積)の論理積  
x=0, y=1, z=0とすると、$x \cdot (y \cdot z) = 0$

右辺：(x,yの論理積)とzの論理積  
左辺と同様にx=0, y=1, z=0とすると、$(x \cdot y) \cdot z = 0$

以上のような要領で、x,y,zすべての値の組み合わせで(左辺) = (右辺)が成立する。  
これを結合法則と呼ぶ。

<br />

- 論理和の結合法則

x+(y+z) = (x+y)+z

左辺：xと(y,zの論理和)の論理和  
x=0, y=1, z=0とすると、x+(y+z)= 0+1=1

右辺：(x,yの論理和)とzの論理和  
左辺と同様にx=0, y=1, z=0とすると、(x+y)+z = 1+0=1

以上のような要領で、x,y,zすべての値の組み合わせで(左辺) = (右辺)が成立する。  

<br />

#### 分配法則

1) $x \cdot (y + z) = (x \cdot y) + (x \cdot z)$

x=1, y=0, z=1とする。  
左辺：xと(y,zの論理和)の論理積なので、$1 \cdot 1 = 1$となる。  
右辺：(x,yの論理積)と(x,zの論理積)の論理和なので、0 + 1 = 1となる。

以上のような要領で、z,y,zすべての値の組み合わせで(左辺) = (右辺)が成立する。

<br />

2) $x + (y \cdot z) = (x + y) \cdot (x + z)$

x=1, y=0, z=1とする。  
左辺：xと(y,zの論理積)の論理和なので、1 + 0 = 1となる。  
右辺：(x,yの論理和)と(x,zの論理和)の論理積なので、1 + 1 = 1となる。

以上のような要領で、z,y,zすべての値の組み合わせで(左辺) = (右辺)が成立する。

分配法則は 1) は$x \cdot (y + z) = (x \cdot y) + (x \cdot z)$  
であり四則演算の分配法則と同じ展開方法なので、最初の方を覚えておく。

**2)の方は 1)の両辺の論理演算子をすべて逆にしたものなので、2)は 1)の論理演算子をすべて逆にしたものとして覚えておく。**

<br />

#### 吸収法則

1) $x \cdot (x + y) = x$

xと(x,yの論理和)の論理積はxとなることを表している。  
x=0, y=0のとき、右辺は0=xとなる。  
x=0, y=1のとき、右辺は0=xとなる。  
x=1, y=0のとき、右辺は1=xとなる。  
x=1, y=1のとき、右辺は1=xとなる。

以上から、結果がxの値と等しくなることがわかる。

<br />

2) $x + (x \cdot y) = x$

2)は1)の論理演算子をすべて逆にしたパターンで、この場合も左辺の結果がxの値と等しいことが成立する。
1)と同様にx,yに値を代入したら確認できるので説明は省略。

<br />

3) $x \cdot (\overline{x} + y) = x \cdot y$

x=1, y=0のとき、$1 \cdot (0 + 0) = 1 \cdot 0$  
ここで右辺を見ると、1=x, 0=yとなっていることがわかる。

x,yのすべての取りうる値で3)が成立する。

<br />

4) $x + (\overline{x} \cdot y) = x + y$

4)は3)の論理演算子が全て逆の場合であり、この場合も4)が成立する。

**3)の吸収法則を覚えておき、そこから4)は3)の論理演算子をすべて逆にしたものとして覚えておく。**

<br />

#### ド・モルガンの法則

論理演算にもド・モルガンの法則が使える。

$\overline{(x \cdot y)} = \overline{x} + \overline{y}$

左辺の論理否定、論理積の全部逆にしたものが右辺になる。

<br />

$\overline{(x + y)} = \overline{x} \cdot \overline{y}$

左辺の論理否定、論理積の全部逆にしたものが右辺になる。

<br />

### 複雑な論理演算式の簡略化

xとyの否定論理積：$\overline{(x AND y)} = \overline{(x \cdot y)}$を"x NAND y"と表記する。

NANDはnot andで、論理積の否定のこと。

このとき、論理式 "(x NAND x) NAND (y NAND y)"を展開しわかりやすく簡略化する。

1) $x NAND x = \overline{(x \cdot x)} = \overline{x} + \overline{x} = \overline{x}$ (ド・モルガンの法則),(同一の法則)  
2) $y NAND y = \overline{(y \cdot y)} = \overline{y} + \overline{y} = \overline{y}$ (ド・モルガンの法則),(同一の法則)  

1),2)により、与式(x NAND x) NAND (y NAND y) = $\overline{x} NAND \overline{y}$  
$=\overline{(\overline{x} \cdot \overline{y})} = \overline{\overline{x}} + \overline{\overline{y}}$ (ド・モルガンの法則)  
$= x + y$ (論理否定の論理否定なので元にもどる)  

<br />

### カルノー図法

複雑な論理和の論理式を簡略化するために利用される表のこと。

式の各変数の値と出力が分かるようになっている。ABCDのとる値は下表のように0に1ビットを加えて表す。

| AB\CD | 00 | 01 | 11 | 10 |
| ---- | ---- | ---- | ---- | ---- |
| 00 | 1 | 0 | 0 | 1 |
| 01 | 0 | 1 | 1 | 0 |
| 11 | 0 | 1 | 1 | 0 |
| 10 | 0 | 0 | 0 | 0 |

縦はAB, 横はCDのとる値を表している。  
AB=00は、A=0,B=0の値をとるという意味で、0は偽、1は真を表している。  

例) AB=00, CD=00の交わるセルの出力は1となっている。  
ここから式を読み取ることが必要となる。  
A,B,C,D=0のときABCDの論理積が出力1になるので、A,B,C,Dは全て1であることが分かる。
なので、$\overline{A} \cdot \overline{B} \cdot \overline{C} \cdot \overline{D}$  
がAB=00,CD=00,出力1という表の情報から読み取れる式となる。

この表から論理式を次のように導く。  
出力1だけでかたまっているところを四角で囲む。囲むときは2の階乗個の個数を囲まないと正しい論理式は導き出せない。  
四角で囲める部分は1箇所とは限らない。  
表の両端は連続するものとみなすので、最初と最後のセルはひと続きとしてみなす。  
すると、この表では真ん中あたりと最上段の2箇所を四角で囲めることになる。  

次に、囲んだ1つの四角ごとに、四角で囲んだ各セルの論理式を求めて縦に並べて書く。

#### 真ん中あたりの四角で囲んだセルの論理式

まず真ん中あたりの四角で囲んだ4つの出力1のセルの論理式を書く。

(AB=01,CD=01の論理式) $\overline{A} \cdot B \cdot \overline{C} \cdot D$  
(AB=01,CD=11の論理式) $\overline{A} \cdot B \cdot C \cdot D$  
(AB=11,CD=01の論理式) $A \cdot B \cdot \overline{C} \cdot D$  
(AB=11,CD=11の論理式) $A \cdot B \cdot C \cdot D$

すると、4つの論理式に共通する変数があることが分かる。  
この共通変数を抽出すると、B,Dなので抽出する論理式は$B \cdot D$となる。

#### 表の最上段の四角で囲んだ2つの出力1のセルの論理式

(AB=00,CD=00の論理式) $\overline{A} \cdot \overline{B} \cdot \overline{C} \cdot \overline{D}$  
(AB=00,CD=10の論理式) $\overline{A} \cdot \overline{B} \cdot C \cdot \overline{D}$

すると、2つの論理式に共通する変数があることがわかる。  
この共通変数を抽出すると、$\overline{A}$, $\overline{B}$, $\overline{D}$なので  
抽出する論理式は$\overline{A} \cdot \overline{B} \cdot C \cdot \overline{D}$となる。

カルノー図が示す論理式は、2箇所の四角で抽出した論理式の論理和となる。

よって、カルノー図から導き出す論理式は  
$\overline{A} \cdot \overline{B} \cdot C \cdot \overline{D} + B \cdot D$  
となる。

<br />

### 集合

集合Sとある要素aがあった場合に、Sにaが含まれているかを下記のように表す。

要素aが集合Sに含まれる場合： $a \in S$

要素aが集合Sに含まれない場合： $a \notin S$

<br />

#### 部分集合の表し方

ある集合S1の要素がすべて他の集合であるS2に含まれるとき、S1をS2の部分集合と呼び、下記のように表す。

$S1 \subset S2$

上記の場合でS2がS1の要素以外を含んでいる場合はS1はS2の"真部分集合"と呼ぶ。

<br />

#### 集合の表しかた

集合全体を全体集合または普遍集合と呼び、Ωで表す。

補集合は$\overline{S}$または$S^c$と表す。

<br />

和集合は$S1 \cup S2$と表す。

積集合は$S1 \cap S2$と表す。

差集合はS1 - S2または$S1 \setminus S2$と表す。  
この場合はS1からS2と共通する要素(積集合$S1 \cap S1$)を除いた集合を表している。

差集合は積集合におきかえることができる。  
$S1 - S2 = S1 \cap \overline{S2}$  
差集合S1 - S2は、S1と$\overline{S2}$の共通部分に等しいので、上記の等式が成り立つ。

<br />

#### 集合演算の公式

論理演算と同じように、集合演算子を使った集合演算にも基本的な公式がある。

和集合は論理和、積集合は論理積と同じ。

##### 交換法則

集合演算子の左と右の集合を入れ替えただけのものなので当たり前に成り立つことがわかるので覚えなくてもよい。

$S1 \cap S2 = S2 \cap S1$  
$S1 \cup S2 = S2 \cup S1$

<br />

##### 結合則

論理演算の論理和、論理積の結合法則と全く同じ考え方。集合の概念で結合則を理解しようとすると大変なので、  
論理演算の結合法則の方をちゃんと理解しといたら大丈夫。

$S1 \cap (S2 \cap S3) = (S1 \cap S2) \cap S3$  
$S1 \cup (S2 \cup S3) = (S1 \cup S2) \cup S3$

積と和の記号が違うだけなので、どちらかだけ覚えておく。

<br />

##### 分配則

集合演算の分配則は論理演算の分配法則と同じ考え方。集合の概念で分配則を理解しようとすると大変なので、  
論理演算の分配法則の方をちゃんと理解しといたら大丈夫。

$S1 \cap (S2 \cup S3) = (S1 \cap S2) \cup (S1 \cap S3)$  
$S1 \cup (S2 \cap S3) = (S1 \cup S2) \cap (S1 \cup S3)$

積と和の記号が違うだけなので、どちらかだけ覚えておく。

<br />

##### 吸収則

集合演算の吸収則は論理演算の吸収法則と同じ考え方。集合の概念で吸収則を理解しようとすると大変なので、  
論理演算の吸収則の方をちゃんと理解しといたら大丈夫。

$S1 \cap (S1 \cup S2) = S1$  
$S1 \cup (S1 \cap S2) = S1$  
記号が変わるだけなのでどちらか一つを覚えておくだけでいい。

$S1 \cap (\overline{S1} \cup S2) = S1 \cap S2$  
$S1 \cup (\overline{S1} \cap S2) = S1 \cup S2$  
記号が変わるだけなのでどちらか一つを覚えておくだけでいい。

<br />

##### 補元則

補元則は論理演算で考えなくても集合の概念で意味をそのままイメージしやすい。

$S \cup \overline{S} = Ω$  
$S \cap \overline{S} = \emptyset$

<br />

##### ド・モルガンの法則

集合のド・モルガンの法則も論理演算で考えると等式が成り立つ理由がわかりやすい。

$\overline{(S1 \cap S2)} = \overline{S1} \cup \overline{S2}$  
$\overline{(S1 \cup S2)} = \overline{S1} \cap \overline{S2}$

<br />

#### 複雑な集合演算の式をかんたんにする

複雑な集合演算はベン図で考えると余計にわかりにくくなるので論理演算で考えて簡単に整理する。

例：

$X = (\overline{A} \cap \overline{B}) \cup (\overline{A} \cap B) \cup (A \cap \overline{B})$を整理する。

$X = (\overline{A} \cap \overline{B}) \cup (\overline{A} \cap B) \cup (A \cap \overline{B})$

// 第1項と第2項に分配則を適用(分配則の右辺側のパターンなので分配則の左辺側に変換)。  
$= \overline{A} \cap (\overline{B} \cup B) \cup (A \cap \overline{B})$ 

// $(\overline{B} \cap B)$は全体集合なので1となる。  
$= \overline{A} \cup (A \cap \overline{B})$  

$\overline{A} \cap (\overline{B} \cup B)$は$\overline{A}$と1の積集合なので論理積と同じ。  
ということは、$\overline{A} \cdot 1$なので、この出力値は$\overline{A}$がとる値そのものなので  
省略できるから$\overline{A} \cup (A \cap \overline{B})$となる。

以上で$X = (\overline{A} \cap \overline{B}) \cup (\overline{A} \cap B) \cup (A \cap \overline{B})$  
が$X = \overline{A} \cup (A \cap \overline{B})$と簡単に整理できた。

ここで、$\overline{A} \cup (A \cap \overline{B})$に対して吸収則が使えるように工夫をする。  
吸収則を適用することでもっと簡単に整理する。

$X = \overline{A} \cup (A \cap \overline{B})$の$\overline{A} = S1$, $\overline{B} = S2$とおくと、

$X = S1 \cup (\overline{S1} \cap S2) = S1 \cup S2$ //吸収則

ここで、S1とS2をもとに戻すと、$\overline{A} \cup \overline{B}$

さらにド・モルガンの法則を適用し、$\overline{A} \cup \overline{B} = \overline{A \cap B}$

以上のように、複雑な集合演算の式を簡略化できた。

<br />

論理演算と集合演算ともに、法則をちゃんと覚えておく。問題解くときにすぐに法則を適用することができないと  
問題を解く時間が足りないため。何度も法則を繰り返し読んで覚える。




---

## グラフ理論

木は閉じていないグラフ。完全グラフはすべての2点間が辺でつながっているグラフのこと。

無向グラフとは、辺に流れ方向など向きがないグラフのこと。有向グラフは流れ方向が決まっているグラフのこと。

### 木の巡回

木の巡回方法は、幅優先順と深さ優先順の2種類がある。  
幅優先順は、"幅"という単語からイメージできるように、横並びの同じレベルの点を順番に巡回する巡回方法。  
深さ優先順は"深さ"という単語からイメージできるように、縦方向の点を巡回する巡回方法。  
深さ優先順は、さらに3つの巡回方法に分かれている。先行順、中間順、後行順。  

深さ優先順は、根(親)から巡回をスタートする。根から巡回するけど点の取りだし方が先行順、中間順、後行順  
で異なるので、同じ内容の木であっても取り出した点の順番が異なる結果となる。

深さ優先順の巡回方法は下記を覚えておくと覚えやすい。

#### 先行順

点の左側を通るときに点の値を取り出す巡回方法。

#### 中間順

点の下を通るときに点の値を取り出す巡回方法。

#### 後行順

点の右側を通るときに点の値を取り出す巡回方法。

<br />

### グラフのデータ構造

ヒープ、2分探索木、B木などがある。

#### ヒープ

ヒープとは、子ノードの値は親ノードの値より大きいか等しい、または小さいか等しい、という大小関係の制約を持った木構造のこと。  
深さの浅い順(木構造の上から順)にノードが配置される。(親のノードの値) < (子のノードの値)または逆の大きさ順に配置される。  
同じ深さでは、普通は左のノードから順に、値が小さい順にノードが配置される。

<br />

#### 2分探索木

2分探索木とは、各ノードの値に下記の制約を持った木構造のこと。  
(左の子のノードの値) < (親のノードの値) < (右の子のノードの値)

2分探索木でAVL木という木構造もある。  
AVL木はどの左右のノードについても深さの差が1以下という条件を満たす木のこと。  

<br />

#### B木(B Tree)

B木は1つのノードに複数の値を格納した木構造。キーとなる値に対しての大小を比較して子のノードに値を振り分ける。







