# Contents

このページにいろいろコンテンツ。
コンテンツのまとめページにする。
noteみたいに記事の一覧があってクリックしたら記事に飛べるようにする。

---

## Linuxやプログラミングのエラー｜普通に分からないことにメモを活用する


Linuxでvimをビルドしようとしてエラーになったときにエラーを解決する
方法としていつも同じように何一つ解決に向けて進まない。

- ターミナルに表示されるエラーメッセージをコピーしようとしてもできない
- エラーと対応をメモしてないのでエラー-> ネットで検索など、また同じことを繰り返す
- 分からないことをメモしたいなと思ってもめんどくさくてなかなかできてない


**今回考えたのが、github pagesをそのままメモがわりに使っていくということ**


//github pagesをメモのかわりに使うことのメリット


- github pagesはマークダウンが使えるので情報を見やすく整理しやすい
- メモがそのままコンテンツになる
- ウェブブラウザで使えるのでどのpc使っていても使える


ということで、メモのかわりにgithub pagesを使うことにします。


## github pagesの導入

//公開するgithub pagesは1GB以内という制限がある

1GBってデータ量的にめっちゃ少なく感じたので、調べてみたら
ウェブページ1ページあたりの容量はだいたい1から2MBらしいので、500〜1000ページは
公開できることになるので、1GBでも充分すぎるので容量に対する制限は気にせず使えます。

**github pagesの作成**

- [github](https://github.com/)の自分のページにいく。
- Repositorysの"New"をクリックし新しいリポジトリを作成
- "Repository name"に<アカウント名>.github.ioと入力し"Create repository"をクリック
- 上記で作ったリポジトリのページで"Create new file"をクリックしindex.htmlなど作成したいファイル名を入力
- helloなど適当に内容を入力し"commit new file"をクリック

**サイトのテンプレートを設定する**

github pagesにはjekyllというテンプレートのテーマが準備されているので便利。
これを利用します。

- "settings"をクリックし"github pages"をクリック
- "choose a theme"をクリックし好きなテーマを選ぶ

" _config.yml " と " index.md " が生成される

jekyllによって生成されたindex.mdをもとにして実際にはindex.htmlが作られてサイトが描画される。

リポジトリ上にindex.htmlとindex.mdの2つが存在する状態だと、index.htmlの方が優先されてテーマが
あたらないので、index.htmlの方は削除しておく。

config.ymlファイルに直接jekyllのテーマ名を書くこと（テーマ名変更すること）でテーマを変更することが
できる。

```
theme: xxx
title: foo 
description: hello
```


また、titleとdescriptionを変えることで、サイト名やサイトがどんなサイトなのかを表示する
サイトのヘッダー部分を変更することができる。



![configyml](https://user-images.githubusercontent.com/43819429/131515949-c6f26247-245d-4feb-b211-06b862789f35.png "config.ymlで表示される文章変更")
















