## 自作キーボードのメモ

meishi2という自作キーボードを買って作ってみた。  
はんだつけ自体ははじめてでもできた。ハードウェア的なことは意外とかんたんだけど、  
Pro Microにキーボードのファームウェアを書き込むというソフト的なことが難しいのでメモをとっていく。

### はんだつけのメモ

はんだは320℃くらいで使う。パーツは背の低い順にはんだつけしていく。  
はんだのこてさきは酸化しやすく、黒くなるとちゃんとはんだつけできなくなるので、  
こまめにはんだをこてさきに塗っておく。作業が終わったらはんだを塗っておく。

はんだのヤニを洗浄するものがあったほうがよい。基盤の上にヤニの飛沫とかが固まっている。

### ファームウェアの書き込み

Pro Microに書き込むためのキーボード用のファームウェアがある。qmk firmware。

Pro Microについても調べておく。

ファームウェアの書き込みはGoogle Chromeのウェブ上で書き込む方法と、CUIで書き込む方法がある。  

web上で書き込む方法は、REMAPというサイトを利用する。

meishi2の場合は[こちらのサイト](https://remap-keys.app/catalog/756NcK1aaYMm9CuJhcTA)。

qmk firmwareをCUIで書き込む場合は、githubからソースをビルドして、実行環境を作る。  
NEC Express5800のubuntuでやってみたけど、pythonのpipの問題でエラーが出てできなかったので、  
また別途時間をとって解決する。

2022/07/07の時点では上記のためできなかったので、ウェブ上から書き込みをした。  
windowsでもCUI１でできる。dell precision5810のwidnows11でqmk firmwareのビルド環境作れたので、windowsの方が簡単かも。

[qmk firmwareについてのドキュメント](https://docs.qmk.fm/#/newbs_getting_started)を読む。  
まだまともに読んでいないため。

[meishi2のビルドガイド](https://biacco42.hatenablog.com/entry/2019/08/10/185624#Mac--Linux-%E3%81%AE%E5%A0%B4%E5%90%88)を読んだら各種リンクも記載されている。


