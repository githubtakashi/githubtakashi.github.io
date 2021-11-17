# xcode swiftの勉強メモ

xcodeとswiftの勉強を進めていてメモを取っておきたいことなど

<br />

## xcodeの操作方法など

- 定義ジャンプ

  - command + click

- story boardのパーツをソースコードに追加

  - control + ドラッグ

<br />

## 文法など

- delegateとprotocol

  appleが準備している機能のこと。
  
  delegateとは、委譲という意味。
  
  iphoneでキーボードを閉じる機能の動作をdelegateとprotocolを使って機能を作れる。
  
  delegateで依頼してprotocolに沿ったデータを渡すことでappleの準備している機能を利用できるイメージ。
  
<br />
  
- optional型
  
  型の後ろに?や!マークを付ける意味
  
```
var hako : String?
...
timelabel.text = hako
```

String?のように型の後ろに?を付けると、デフォルトがnilになり、何もない状態になる。

Stringの後ろに?を付けずに他のところに変数のhakoを渡すと、値が設定されていない変数を渡すことになるので、エラーとなる。

この状態で値として他のところに渡すとエラーとならない。
  
String?のように型の後ろに?を付けると、デフォルトがnilになり、エラーとならない。

<br />

?を付けることで変数hakoがラッピングされた状態になる。

```
var hako : String? = "ねこ"
print(hako)
//出力結果：optional(ねこ)

print(hako!)
//出力結果：ねこ
```

強制的アンラップをするために必要なのが!記号。

!を付与することで、optional宣言した変数を、とにかく強制的にアンラップできる。

<br />

optional型にしてnilで変数に何も値がない状態だと、予期しないままプログラムが終了してしまう挙動に

つながることがある。

これを防止するために、optional bindingを行う。

条件分岐して、変数に値が入っている時はOO、入っていない時はxxみたいに処理を分けることで、

値が入っていない状態での予期せぬ挙動をしないようにできる。

optional bindingはif文で条件分岐する。

```
let hako : String?
if let hako2 = hako {
  print(hako2)
}
else {
  print("hako: nil")
}
//hakoの中身はnilなのでelseの中身が実行される
```

<br />

optional chaining

optional型の変数のうしろに?を付与してプロパティやメソッドにアクセスする。

optional型の変数の値が存在するかどうかを検証してくれる。

もし値が入っていれば変数をアンラップし中身が取り出されるという処理が自動的にされる。

変数がnilだったらアンラップせず,値が入っていたらアンラップするみたいに処理してくれる。

optional型の変数?.method()

optional型の変数?.property
  
<br />

## Jump to Difinitionできる理由

ライブラリをインポートしているので定義ジャンプができる。

```
import UIKit
import WebKit 
```

## 目的から機能を覚えていくとよい

実装したい機能という目的が初めにあって、目的でググってそこから書き方を調べる。




