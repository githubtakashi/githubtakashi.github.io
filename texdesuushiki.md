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


# github pagesとnote.muで数式を書く方法

github pagesのmarkdownのmdファイルやnote.muでのブログに数式を表記できるように
したい。方法を調べたのでメモ(2021年10月15日現在での方法)。

<br />

## github pages

下記のコードをmdファイルの上部にペーストする。

<br />

```
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
```

texの記法で数式を書くと、github pagesのmdファイルのプレビュー時には適用されないけど、
htmlの公開ページにはちゃんと数式が表示されるようになる。

<br />

- inlineMathとdisplayMath

文中に数式を表示する場合はinlineMathの表記方法を使う。

⇒数式を$ $で囲む。

文中に数式を表示せず、新しい段落に数式を表示するときはdisplayMathを使う。

⇒数式を$$ $$で囲む。

2^3を表記すると下記のようになる。

2の3乗 $2^3$

$$
D = P^{-1} A P
$$

<br />

## note.mu

noteに数式を埋め込む場合は少し手順を踏む必要がある。

<br />

### texの数式をurlに埋め込むツールにtexの数式を埋め込みリンクを作成する

tex image link generatorというツールを利用する。

[リンク作成ツールのurl](https://tex-image-link-generator.herokuapp.com/)

texの書き方で数式を記入したら自動的にurlが生成されるようになっているので、
コピーしておく。

<br />

### githubでgistを作成する

'+'をクリックし"new gist"をクリック

コピーした数式のurlをペーストし。ファイル名を適当に付ける。
ファイル名は"filename.md"のようにmd拡張子にする。

右下の"create secret gist"をクリック。

"Embed"をクリックし、"share"をクリック。

urlが生成されるので。そのurlのコピーアイコンをクリックしてコピーしておく。
これがnoteのブログ記事内に貼り付けるurl。

<br />

### gistのurlをnoteにペーストする

gistで生成したurlをnoteの記事の中にペーストすると数式が
表示される。

<br />

### 数式のメモ

実際に使う数式の書き方をメモしていく。

#### 論理演算子

| 名称 | 演算子 | TEX記法 |
| ---- | ---- |  ----|
| 論理積 | $\cdot$ | \cdot |
| 論理和 | + | + |
| 排他的論理和 | $\oplus$ | \oplus |
| 論理否定 | $\lnot$ | \neg,\lnot |

<br />

#### 集合の演算子

| 名称 | 演算子 | TEX記法 |
| ---- | ---- |  ----|
| 和集合 | $X \cup Y$ | X \cup Y |
| 積集合 | $X \cap Y$ | A \cap B |
| 補集合 | $\overline{A}$ | \overline{A} |
| 空集合 | $\emptyset$ | \emptyset |
| 集合の要素 | $\in$ | \in |
| 集合の要素 | $\ni$ | \ni |
| 集合の要素でない | $\notin$ | \notin |
| 部分集合 | $\subset$ | \subset |
| 部分集合 | $\supset$ | \supset |
| 補集合 | $A^c$ | A^c |
| 差集合 | $\setminus$ | \setminus |



ド・モルガンの法則の書き方

\overline{A \cup B}=\overline{A}\cap\overline{B}

$\overline{A \cup B}=\overline{A}\cap\overline{B}$






