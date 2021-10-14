# ウェブブラウザで数式を書く方法

github pagesのmarkdownのmdファイルやnote.muでのブログに数式を表記できるように
したい。方法を調べたのでメモ(2021年10月15日現在での方法)。

## github pages

下記のコードをmdファイルの上部にペーストする。

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

あとはtexの記法で数式を書くと、github pagesのmdファイルのプレビュー時には適用され無いけど、
htmlの公開ページにはちゃんと数式が表示されるようになる。

<br />

## note.mu

noteに数式を埋め込む場合は少し手順を踏む必要がある。

-[x]texの数式をurlに埋め込むツールにtexの数式を埋め込みリンクを作成する

-[x]githubでgistを作成する

-[x]gistのurlをnoteに挿入する







