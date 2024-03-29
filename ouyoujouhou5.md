## 応用情報の勉強ノート|5ページ目

応用情報の勉強をある程度してきたけど抜けがあると感じた知識やメモしておきたい内容をこのページにかいている。

<br />

### 応用数学の午前問題

テクノロジ系 > 基礎理論 > 応用数学

令和3年秋の午前問題の第1問目でニュートン法についての説明を選ぶ問題が出題。

解答の選択肢として、  
オイラー法、ガウスの消去法、シンプソン法、ニュートン法があったが、どれも知らなかった。

前提として知っておかないといけない基本も知らないのでメモ。

#### 微分とは

参考記事：[微分についてわかりやすい記事](https://www.headboost.jp/what-is-derivative/)を発見したので参照する。  

100mを10秒で走ったとき、実際、通常は速さが一定ではない。  
そのため、距離をy軸、x軸を時間としたグラフで速さを表すと、曲線になる。  

この実際の速度の曲線に限りなく近いグラフを、曲線の接線で表現することが微分という概念。  
接線は、時間が大きいよりも瞬間的、つまりx軸上の2点間の時間が0に限りなく近いとき、瞬間速度となり、曲線に対する接線は曲線に近くなる。 

接線つまり瞬間速度を別途のグラフに表すと、ある時点の速度が視覚的に簡単に分かるようになる。このグラフを導関数という。  
微分することとは、導関数を求めること。


### 限界利益とは

限界利益は、売上のお金から変動費を引いたもので、限界利益＝「売上高」ー「変動費」。  

売上高と変動費と固定費という要素で考えたとき、「売上高」ー「変動費」と固定費を比べることで、  
利益のお金が固定費に比べてどうなのかを見る。

限界利益が固定費に比べて大きいなら、利益が出るということを表していて、固定費よりも小さいなら利益が出ないということを  
表している。また、大きさの具合で利益の具合もわかる。

<br />

### 限界利益率とは

売上高に対する限界利益の割合を計算して算出された数値のことを限界利益率という。  

限界利益率＝「限界利益」÷「売上高」

限界利益率が大きいほど、利益が大きいことを意味し、損益分岐点の売上高が小さくなるので、  
収益性が高いことを意味する。

例1). 
売上高：100万円、変動費：30万円

限界利益率＝(100-30)/100 = 70/100 = 0.7

例2)  
売上高：100万円、変動費：60万円

限界利益率＝(100-60)/100 = 40/100 = 0.4

例1、2の例で考えてみても、変動費が小さく限界利益が大きい例1のほうが利益が大きいことがわかる。

<br />

### 条件網羅と判定条件網羅

「条件」は、「個別の条件」と読み替える。条件網羅は個別の条件に着目したもの。個別の条件の真偽を網羅したものが  
条件網羅。

「判定条件」は、分岐路と読み替える。判定条件網羅は、分岐を網羅すること。

判定と条件の違いが混乱しいつもすぐ忘れてわからなくなるので上記のように覚えておく。  

<br />

### 令和2年秋1問めの問題

対数を使った問題で理解に時間がかかったのでメモ。 

10の累乗で整数を表すと指数が桁数を表せ、進数の整数が2桁の10から99を表せる。  
同様にして、2の累乗で整数を表すと指数が2進数の桁数を表している。例えば、指数が2の時は、整数2、3を表せる。これは、2進数で表記すると、10および11となり、2桁の2進数で表すことのできる整数を全部網羅している。

よって、2進数で桁数が2の時の最小値は2、最大値は3となる。

以上から、10の累乗の最小値側か最大値側の近い方のどちらかで2桁のある特定の値をとる10進数を表現でき、2の累乗の最小値側か最大値側の近い方のどちらかで2桁のある特定の値をとる10進数を表現できる。

xが10の時、D=1であり、B=4である。これは共に最小値側となる。x=99のときD=2未満であり、B=7未満である。これは共に最大値となる。よって、

10の累乗の最小値側と2進数の累乗の最小値側、10進数の累乗の最大値側と2進数の累乗の最大値側は同じ値に近いということになる。

そのため、10進数表記の整数10を10のD-1乗した値と、2のB-1乗した値は、「≒」で結ぶことになる。最大値側も同様。

![image](https://user-images.githubusercontent.com/43819429/226172541-6911bee0-10e1-424c-88e3-15eded493ef0.jpeg)

<br />

### ハフマン法とランレングス法(データの圧縮方法)

圧縮方法について、基本のランレングス法と、ハフマン法も記憶から完全に消えていた。

ランレングス法はaaabbbbccdという文字列に対し、連続した同じ文字に対し回数+文字の組み合わせで表現することで  
圧縮する方法。上記の文字列をランレングス法で圧縮すると3a4b2c1dになる。

白と黒の2種類でできていて同じデータが連続しやすいモノクロのデータなどは大きく圧縮できるのでランレングス法が利用される。

<br />

ハフマン法は同じ文字の出現回数に着目している。helloworldという文字列の場合

文字列：helloworld   
合計文字数：10文字
文字種：7種類

2進数1ビットで、0と1を使って2種類の文字に対して種類を表現できる。  
同様に考えて、2ビットでは4種類、3ビットでは8種類の文字に対して文字の種類を表現できる。

helloworldは7種類の文字があるので、1文字あたり3ビットで表現することになる。

1文字3ビットで表現すると、圧縮前は3ビットｘ10文字＝30ビットがデータ量となる。

ハフマン木を使ってhelloworldを表すと、27ビットになり、27/30 = 0.9 となり、10%圧縮される。

![image](https://user-images.githubusercontent.com/43819429/228383428-eac0793c-8378-40ba-adfb-6327ab97f7cc.jpeg)

<br />

[ハフマン符号化のとても参考になった記事](https://note.com/toppakou/n/nbf4128366f1e)を参照する。

<br />

### ガウスの計算法

0+1+2+...99など、連続した自然数を順に足して合計する足し算は、ガウスの計算法で計算できる。

0～99までの100個の自然数の足し算は、0+99=99, 1+98=99, 2+97=99 ...のように、99を50回足したものになる。

そのため、合計は、(0+99) x 50 = 4950となる。 このように、簡単に計算することができる。 

<br />

### 平成30年秋34問目の問題

あるサブネットで、ネットワーク機器にIPアドレスを割り当てる時に、アドレス末尾から降順に使用する。  
サブネットのネットワークアドレスは10.16.32.64/26の時、10番目に割り当てるネットワーク機器のアドレスを
求めよ。

![image](https://user-images.githubusercontent.com/43819429/229406600-e315aab3-d691-4e3b-958c-5205e404d952.jpeg)

<br />

### WPA関連についての整理

wpa関連の内容をすぐ忘れる＝頭が整理されにくい ので整理しておく。

#### WPAは無線LANのセキュリティプロトコル名称

WAPは無線LANのセキュリティプロトコルの名称。

WPAとWPA2、最新のプロトコルとしてWPA3がある。

上記の無線LANのセキュリティプロトコルで利用される暗号化方式として、TKIPやCCMPがある。  

<br />

#### WPAで使われる暗号化方式と暗号化アルゴリズム

TKIP: Temporal Key Integrity Protocol(暗号化方式)  
RC4という暗号化アルゴリズムが利用されている。暗号化に使う鍵を短期間に変更する。共通鍵が使われる。  
RC4はストリーム暗号方式。１ビット単位、1バイト単位という細かなデータを順次暗号化するようなイメージ。

<br />

CCMP: Counter mode with CBC-MAC Protocol(暗号化方式)  
AES: Advanced Encryption Standard という暗号化アルゴリズムが利用されている。
データを一定の長さのブロック単位にして、置換や並び替えを繰り返し暗号化するブロック暗号方式。共通鍵が使われる。RC4よりも暗号化が強固。

AESではブロックの鍵長が選択できる。128, 192, 256bitの3つから選ぶことができる。  
置換や並び替えを繰り返す方法として、SubBytes、ShiftRows、MixColumns、AddRoundKeyという4つの処理が行なわれる。

<br />

ストリーム暗号方式よりもブロック暗号方式の方が一般的に使われている。

ブロック暗号方式として、AESのほかに古いものとしてDES: Data Encryption Standard がある。  
使える鍵長が56bitで短いので簡単に解読されセキュリティが弱い。

<br />

#### WPA-PSKのPSKとは

Pre Shared Keyの略で、事前共有鍵方式のこと。アクセスポイントと端末の間で事前に設定したパスコードで認証し接続や暗号化をすること。

<br />

### システム監査の監査サンプリング

難しく感じたのでメモしておく。平成30年秋午前問58で出題され解説も難しく感じた。

<br />

#### 監査サンプリングの許容逸脱率とは

内部統制のテストで発見したエラー、不備の上限のこと。10％未満とする。  
25件をサンプリングして不備がないか確認し、2件以下なら問題なしということに理論上はなるが、  

25件中1件でも不備が見つかると、追加で17件サンプリングをして、追加サンプル分から不備が無いかを確認。  
不備がなければ問題なしとする。といった手順で許容逸脱率が10%未満であるかを確認する。

監査人の経験、実務上は、許容逸脱率1%、イメージとしては100件中1件の不備の有無が、被監査対象がちゃんとしているかどうかの. 
指標になっているらしい(とはいえ上記のような手順を踏んで評価し10%未満であれば問題なし)。

実務上は、監査対象が90%以上の信頼性を持っているかを確認するため、不備の割合が10%未満ではなく、9%未満であることを確認. 
できるようにサンプリングをしている。

<br />

#### サンプリングリスクとは

監査サンプリングでの監査結果が、母集団の実際持っているデータと異なること。  
つまり、監査サンプリングでの監査結果がおかしいということ。  
実際は母集団200件を全部確認すると不備の件数は2件で問題なしであるのに対し、その2件を少ない件数のサンプリングで拾ってしまい. 
NG判定になり、本当は合格であるのに対し、監査では不合格にされる(本当は不合格なのに監査では合格という逆も同様)といったことをサンプリングリスクという。

#### 固有リスクと統制リスクとは

固有リスクとは：  
内部統制が存在していないという仮定のうえで重大な虚偽表示がされる可能性。  
虚偽が発生しやすい状況など。例えば、やり直しすると工程が遅れるので分析値をちょっと誤魔化さざるを得ない状況になりやすい作業、  
そういったことがないか、監査側が考慮する。

統制リスクとは：  
虚偽の表示が企業の内部統制によって防止、又は適時に発見できない可能性。  
分析値の入力が手作業でダブルチェックがなく誤魔化しやすい作業など。こんな感じに内部統制が不十分なものはないか、監査側が考慮する。

監査リスクとは：  
固有リスクと統制リスク、(発見リスク)を掛け合わせた結果を監査リスクという。

#### 統計的サンプリングと非統計的サンプリングとは

サンプリングでの監査では統計的サンプリングと非統計的サンプリングのどちらかを実施する。

統計的サンプリングは下記のように行う。

1.母集団からサンプルを無作為に抽出する。  
2.抽出したサンプルに対して確率論を利用することで判断結果を導き出す。

非統計的サンプリングは、上記の1と2の一つでも満たさないものは、非統計的サンプリングとなる。

<br />

### 需要値を予測する方法

過去の実績から需要予測をする際に、過去の実績の重みづけをどのように扱うかによって、  
単純移動平均法、加重移動平均法、指数平滑法での需要予測をする方法がある。

過去のデータの重みづけをどのように扱うのが適切なのかは一概には言えないので対象に合わせて適切に判断する。  
といったことが必要になる。

[参考にした記事](https://mirukognosis.com/?p=1020)を参照する。

<br />

#### 単純移動平均法

単純移動平均は過去のデータも直近のデータも同じように扱う需要予測の計算方法。  
需要予測する際は、感覚的には、過去のデータを重要性が小さく、直近のデータを重視するべきだと思いがちだが、  
単純移動平均では過去のデータの重みづけが小さくならず、過去も直近も均等に扱う。

<br />

#### 加重移動平均法

直近から過去にさかのぼるに従って徐々に等間隔で重みを減少させることで、直近のデータを一番  
重要なものとし、過去のデータに遡るほど重要性が小さくなる需要予測の計算方法。

重みづけに係数1～0の係数を使う。例えば、直近のデータの係数を1とし、0.9,0.8.0.7...のように、  
0.1ずつなど一定間隔で係数を減少させることで重みづけをする。

上記のため、過去実績にさかのぼって、重みづけの係数が0になったら、それよりも前の過去実績は  
無視されることになるので、需要予測の根拠からも無視されることになる。

<br />

#### 指数平滑法

指数平滑法が平成30年秋の午前問題の69問目で選択肢として出てきた。

加重移動平均法と同じで、直近のデータほど重要な重みづけとなり、過去のデータほど重要性が小さい重みづけ  
となる。過去に遡るほど指数関数的に重要性が小さくなるので、指数平滑法と呼ばれている。

- 加重移動平均法と指数平滑法の違い：  
加重移動平均法は過去のある時点で係数が0になり、それより前の実績データは無視されるのに対し、  
指数平滑法では過去に遡るほど重要性は小さくなるが、無視はされず需要予測に反映される点が異なる。

<br />

### OC曲線

いつも訳が分からなく感じるので、メモしておく。説明が分かりにくいことが多い。

分かりやすいと感じた[OC曲線の記事](https://qctoranomaki.com/sqc/inspection/oc-curve/)を参考にする。

不良品率をx軸、合格率をy軸にとる。oc曲線はLOT単位の抜き取り検査についてのグラフ。

例えば、1ロット1000個あるうち、100個の抜き取り検査をして不良品の個数が1個の場合は不良品率は1%である。

合格率を検査基準に採用する際に問題となるのが、出荷できない製品が多く出てしまうという  
生産者側にとっての不都合と、不適合品を受け取ってしまうという消費者側にとっての不都合。

上記の折り合いを相談して決めることが多いらしい。

例えば、不良品率1%の合格率が75%を合格基準にすると、100 - 75 = 25%のlotは不合格と判定され、  
生産者側にとってのロスとなる。

不良品率は、実際に試行しなくても1LOTのサンプル個数と不良品の個数だけ分かれば下記のように定まる。

サンプル100個中不良品が1個である場合、不良品率は1 / 100 * 100 = 1%  
サンプル100個中不良品が2個である場合、不良品率は2 / 100 * 100 = 2%  
サンプル100個中不良品が3個である場合、不良品率は3 / 100 * 100 = 3%  
...

のように、不良品率は計算で求まる。

x軸にこの不良品率をとる。

y軸は合格率をとる。  
{lot単位で不良品率1%が実際に発生した回数} / {lot単位での検査回数の合計}  
を計算することで、不良品率が1%となる確率が計算できる。  

例えば、10回検査して不良品率1%の結果が7回あった場合、不良品率1%となるlotが出る確率は、  
7 / 10 * 100 = 70%となる。

この不良品率1%のときの70%をy軸にとる。不良品率1%となるlotが70%の確率なので、感覚的に  
考えてみても不良品率1%を合格とすることになると判断できる。

上記から、話し合い等で生産側と消費者側の双方にとって適切な合格率となるようにOC曲線を利用して調整をして  
サンプルの合格基準値を決める。

<br />

### 山登り法とは

局所探索法という。ある関数が条件として与えられているとき、その関数の極大値、極小値といった極値を探索するために  
利用される最適解の探索アルゴリズム。

例えば極小値を探索するとき、関数にてきとうな値を入力し、そこから近傍の値を計算していき、極小値を探索するイメージ。

[局所探索法についての参考記事](https://mukai-lab.info/pages/classes/artificial_intelligence/chapter8/)

<br />

### 焼きなまし法

山登り法の探索方法にランダム性を加えた最適解の探索アルゴリズム。

ランダム性を時間の経過とともに小さくしていく。

[焼きなまし法についての参考記事](https://gasin.hatenadiary.jp/entry/2019/09/03/162613#:~:text=%E7%84%BC%E3%81%8D%E3%81%AA%E3%81%BE%E3%81%97%E6%B3%95%20%E3%81%AE%E6%A6%82%E8%A6%81%201%20%E5%B1%B1%E7%99%BB%E3%82%8A%E6%B3%95%E3%81%AB%20%E3%83%A9%E3%83%B3%E3%83%80%E3%83%A0%E6%80%A7%20%E3%82%92%E5%85%A5%E3%82%8C%E3%81%A6%E5%B1%80%E6%89%80%E8%A7%A3%E3%81%AB%E9%99%A5%E3%82%8A%E3%81%AB%E3%81%8F%E3%81%8F%E3%81%97%E3%81%9F%E3%82%82%E3%81%AE,2%20%E3%82%B9%E3%82%B3%E3%82%A2%E3%81%8C%E6%94%B9%E5%96%84%E3%81%95%E3%82%8C%E3%81%9F%E3%82%89%E7%84%A1%E6%9D%A1%E4%BB%B6%E9%81%B7%E7%A7%BB%E3%81%A0%E3%81%8C%E3%80%81%E6%82%AA%E5%8C%96%E3%81%AE%E3%81%A8%E3%81%8D%E3%82%82%20%E7%A2%BA%E7%8E%87%E7%9A%84%20%E3%81%AB%E9%81%B7%E7%A7%BB%E3%81%99%E3%82%8B%203%20%E3%83%A9%E3%83%B3%E3%83%80%E3%83%A0%E6%80%A7%E3%82%92%E6%99%82%E9%96%93%E7%B5%8C%E9%81%8E%E3%81%AB%E5%BF%9C%E3%81%98%E3%81%A6%E5%B0%8F%E3%81%95%E3%81%8F%E3%81%97%E3%81%A6%E3%81%84%E3%81%8F%E3%81%93%E3%81%A8%E3%81%A7%E5%8F%8E%E6%9D%9F%E3%81%95%E3%81%9B%E3%81%A6%E3%81%84%E3%81%8F)

<br />

### 線形探索法

線形探索法とは、例えば、数字が並んでいる列があるとして、その列の先頭から探したい数値と比較することで、探したい数値を探す方法。  
線形探索法の平均探索回数をすぐ忘れるのでメモ。

目的の数値を探すとき、探索の最小回数は、目的の数値が列の先頭にあるときは1回で探すことができるので、1回。  
探索の最大回数は、目的の数値が列の最後尾にあるときで、列の要素数がN個とすると、N回。

以上から、平均探索回数は、(探索の最小回数)+(探索の最大回数)/2 = (N+1)/2 回となる。

[線形探索法についての参考記事](https://www.foresight.jp/fe/column/algorithm/)

<br />

### 線形探索の午前問題 | 平成30年春午前問6

手こずったのでメモを貼っておく。

![image](https://user-images.githubusercontent.com/43819429/232505520-7a6d6639-acbc-48aa-9ef9-e04bb4dd7dfb.jpeg)

<br />

### 隣接行列|平成29年秋午前問6

隣接行列の問題が出ることがある。全く知らなかったのでメモ。

グラフ理論の内容として隣接行列がある。

[過去問](https://www.ap-siken.com/kakomon/29_aki/q6.html)がそのまま分かりやすかったので参照する。  
解き方：隣接行列から1～5の5つのノードを準備し、1フラグがあるノードを辺でつなぐ。

<br />

### 2分探索の計算量

2分探索の計算量（平均比較回数）を求めることに対して理解に手こずったのでメモ。

2分探索はまず探索対象のデータをあらかじめ整列しておく。昇順などに。  
例としてデータは数字と想定する。

#### 2分探索の流れ

1回の比較で終了する場合と、終了しない場合がある。  
最小探索回数と平均探索回数と最大探索回数について理解していく。

- 最小探索回数：1回目の比較で終了する場合
たまたま探したい値とデータ列の中央値が同じだった場合、探索回数は1回で済むので、2分探索の最小探索回数は1回。  
1回目：整列データを中央の値で2分割する。整列データに対して探したい数字と、整列したデータの中央の値を比較する。(中央の値＝探したい値) であれば1回で比較は終了。  

- 平均探索回数：1回目の比較で終了しない場合  
平均探索回数が何でlog2Nになるかは[qiitaの記事を参照](https://qiita.com/naokunfootball/items/1c2449169e1ddda73175)  
1回目：(中央の値 > 探したい値) の場合、探したい値は中央の値よりも前半に存在することになるので、中央の値よりも前半のデータ列を探索対象とする。  
2回目：前半のデータ列の中央値の値と探したい値を比較する。1回目と同様、比較し同じ値なら探索終了、異なるならデータ列の2分を実施する。
.  
.  
k回目：上記同様。整列データが1以上2未満になったら探す要素が1つしかなくなるので、探索は終了する。

上記のように、探索回数をk回のときの探索回数が、平均探索回数となる。

- 最大探索回数：要素が奇数個のときに発生  
要素が偶数個のときは、1/2ずつに要素数が減っていくため常に平均探索回数に収まるが、奇数個の時は探索回数が最大で平均探索回数+1となる。  
これが2分探索における最大探索回数となる。

最大探索回数について、bingで検索したときの引用を下記に記す。

>こんにちは、これはBingです。😊

>２分探索の最大探索回数が＋１回となる理由は、データの個数が２のべき乗でない場合に、最後に残ったデータを調べる必要があるからです12。

>例えば、データの個数が８個の場合、２分探索では３回で目的のデータを見つけることができます。しかし、データの個数が９個の場合、３回で残り２個に絞り込むことができま>すが、その中から目的のデータを見つけるためにもう１回探索する必要があります。したがって、最大探索回数は４回となります3。

>２分探索では、データの個数が２倍になって初めて最大探索回数が１回増えます4。そのため、データの個数をnとすると、最大探索回数はlog2n＋１回となります12。

<br />

- 探索回数とデータ列の要素数の関係  
元のデータ数をn個とすると、要素数は探索回数ごとに半分に減っていく。探索回数をkとすると、探索k回目の要素数は、n/2^kと表せる。

たとえばn＝2の時、探索回数k＝1のときの要素数を知りたい場合、探索回数1回時点での要素数は、2/2^1 = 1個となる。  

探索対象のデータ数n＝2で、具体的なデータは[3, 4]で、3を探したいとき

1回目：3を中央値とした場合；3と4に2分割→中央値の3と探索したい値3を比較。3=3で見つかり探索終了。要素は3だけの1個となる（要素数は2/2^1 = 1）。

1回目：4を中央値とした場合；3と4に2分割→4と3を比較、4>3 なので前半のデータ列を探索する。3=3で見つかり探索終了。上記同様、要素は3だけの1個となる。

<br />

### メッセージ認証とデジタル署名の違い

[メッセージ認証とデジタル署名についての参考記事](https://taketake2.com/R8.html)

メッセージ認証・・・平文データに対してハッシュ値を計算し、そのハッシュ値に対して共通鍵で暗号化する。メッセージ認証は送信者が正しいかは検証しない。  
共通鍵暗号を利用するので、公開鍵暗号を利用するデジタル署名よりも処理が速い。

デジタル署名・・・メッセージ認証に加えて、送信者の身元が正しいことも検証することで保証できる。


#### メッセージ認証  
メッセージ認証はデータの送信者が正しいことを検証しない。送信する平文に対してハッシュ値を計算し、そのハッシュ値に対して  
共通鍵で暗号化する。共通鍵で暗号化して生成された値をMACと呼ぶ。そのMACと平文データを受信者に送信する。  
受信者は、送信者と同様に、受信した平文データに対してハッシュ関数でハッシュ値を計算し、そのハッシュ値に対して共通鍵で暗号化処理をし、MACを生成する。  
受信者が平文から生成したMACと送信者から送られてきたMACの値が同じかどうかを比較し、もし同じ値なら送信の途中で平文データが改ざんされていないことになる。

メッセージ認証の例）  
送信者：  
平文：abc、MAC：jfa2　を送信

ある平文に対するハッシュ値、MACは同じアルゴリズムを使ったら常に同じになる。

受信者：上記を受信したところ平文はvbcであった。途中で改ざんされているかは、受信側にとってはわからない。  
平文vbcに対して、送信者と同じハッシュ関数、共通鍵でMACを生成したらfjisajfiとなった。

送信者から送られてきたMACと受信者が平文から生成したMACが違うということは、その平文は改ざんされているということ。

送信者のMACと受信者のMACが同じ値なら、その平文は改ざんされていないということになる。


#### デジタル署名  
平文データのハッシュ値に対して公開鍵暗号方式を使って暗号化する。送信者の秘密鍵で平文のハッシュ値を暗号化し、受信者が公開鍵で復号する。  
受信者は、送信者の秘密鍵で暗号化されたハッシュ値を公開鍵で復号し、そのハッシュ値と、受信者が平文から生成したハッシュ値を比較し、  
ハッシュ値が同じなら平文は改ざんされていないことになる。と同時に、送信者しか持っていない秘密鍵で暗号化したハッシュ値を受信者が公開鍵で復号できた  
ということは、公開鍵の対になる、送信者しか持っていない秘密鍵で暗号化された=送信者本人であることになる。  

公開鍵暗号方式でなんで送信者の身元が正しいことが証明されるのか。それは、受信者が受け取る公開鍵に対して更にCAの発行するデジタル証明書が  
セットとして紐付いていることで、その公開鍵がわけのわからないものではなくきちんと管理され特定されたものであることを証明している。

公開鍵にデジタル証明書が紐づくことで、公開鍵を改ざんしてもデジタル証明書が紐付いていないので、その公開鍵は偽物だと簡単にわかるのかも。

そのきちんと管理された公開鍵で復号できたということは、暗号化に使用された対になる秘密鍵もきちんと保証されたものであることになり、秘密鍵の  
持ち主が特定されることになり、わけのわからない誰かではないことになり、送信者本人であるということになる。

もしその秘密鍵を登録された送信者本人ではないにしても、制度上は本人であるとみなされることになる。その管理された秘密鍵の身元を  
使って変なことしても、管理されているので秘密鍵も公開鍵も無効にされるなど対処されるので被害を拡大させることは防止できる？

<br />

### ターンアラウンドタイムの問題 | 平成27年秋問31

ターンアラウンドタイムの問題に苦戦した末にわからなかったのでメモ。

2つの異なる回線があって、処理するデータ量は同じで、回線速度が異なる。回線速度、ターンアラウンドタイムは問題文で提供されている。  
処理するデータ量、ホストコンピューターの処理時間は提示されていない。問題を解くうえで、データを処理するホストコンピュータの処理速度は  
端末AとBで同じなので無視していたが、それを無視していたせいで解けなかった。

データ量が分かれば解けると思い込んでいた。ターンアラウンドタイムは問題文で提示されている項目の時間をすべて足したものなのであることに  
注意し、丁寧に考えること。

そのため、ターンアラウンドタイムを構成しているホストコンピュータの処理時間を求めることを考える。端末AとBの与えられた条件から方程式を作って  
ホストコンピュータの処理時間を求める。処理するデータ量とホストコンピュータの処理時間は等しいので、異なる回線速度をどちらかの回線速度に合わせると、  
ターンアラウンドタイムからホストコンピュータの処理時間を引いたものは等しくなることに着目して等式を作る。これに気付くことは難しいが、慣れることで  
覚えておく。

今回は端末Aの回線速度が端末Bの回線速度の10倍であることを利用し、端末Aを10倍する。端末Aを10倍することで、速度が遅い端末Bのほうに回線速度を合わせることになり等式が作れる。

ターンアラウンドタイムからホストコンピュータの処理時間を引いたものは、ある回線速度での回線をデータが通過するのにかかる時間である。この時間が異なると、解けるのかもしれないが  
ややこしくなるので、10倍することで、回線部分をデータが通過する時間を同じにできる。そうしてホストコンピュータの処理時間を求めるための等式を作ることができる。




































