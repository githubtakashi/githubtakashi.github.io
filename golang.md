## go言語を使うためのメモ

goに興味が出たので使っていく。

goの[公式サイトのチュートリアル](https://go.dev/doc/tutorial/getting-started)を進めていく。

### helloモジュールを作成

ホームディレクトリにhelloディレクトリを作成しgoのモジュールを作成。  

```
cd
mkdir hello
cd hello
go mod init example/hello
```

go mod init <モジュール名>  
を実行することで、go.modというファイルが生成される。

モジュール名を指定する際はモジュールのパスも指定する。

例では、モジュール名はhello,パスはexample/hello

上記によって、モジュール化されるので、自分で名付けたモジュール名を指定することでモジュールとして使うことができる。

<br />

### hello.go作成

hello.goを作成しhello worldを表示するソースコード書く。

```
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

作成したファイルを実行する。go runコマンドで実行できる。  
ビルドして実行が自動的にされる。

```
go run .
//Hello, World!がターミナルに出力される
```

### 外部のモジュールを使う

goの公式サイト上のpkg.go.devという場所に、いろいろgoのモジュールが登録されていて使うことができる。

今回は、pkg.go.devに登録されているquoteというモジュールを、自分のソースコードの中で呼び出して利用する。

検索窓で"quote"を検索してヒットする "rsc.io/quote" を利用する。

hello.goのソースコードを下記のようにする。importでquoteモジュールを呼び出すことができる。

```
package main

import "fmt"

import "rsc.io/quote"

func main() {
    fmt.Println(quote.Go())
}
```

pkg.go.devに登録されている外部のモジュールであるquoteをつかうためには、下記のようにgo mod tidyという  
コマンドを実行する。

```
go mod tidy
go: finding module for package rsc.io/quote
go: found rsc.io/quote in rsc.io/quote v1.5.2
```

go mod tidyをすると、go.sumを生成し、既存のgo.modファイルに外部モジュールを使うためのrequireなどの  
記述を自動的にしてくれる。

```
go run .
//quoteモジュールを使った結果がターミナルに出力される
Don't communicate by sharing memory, share memory by communicating.
```

<br />

#### go.modとgo.sumファイル

go.modはモジュールのパスやバージョン情報を記載するファイル。どんな依存関係を持っているかも記載する。  
基本的には自動生成に任せ、自分で編集しないファイル。

go.sumはgo mod tidyコマンドを実行すると生成されるファイル。go mod tidyするとgo.sumを元に依存先を取得する。  
go.sumは依存先のモジュールのハッシュを記録していて、もしウィルス仕込みなどで依存先のファイルが改ざんされていたら、  
go.sumのハッシュ値と依存先のハッシュ値が異なるので、改ざんを検知できる。




