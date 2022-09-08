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

