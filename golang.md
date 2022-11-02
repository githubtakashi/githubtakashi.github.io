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

example/helloのexampleの部分は、第３者にも使ってもらうことを想定する場合は、通常はgoが探すことができるパス名となり、  
普通はgithub.com/<プロジェクト名>となる。

<br />

#### hello.go作成

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

#### 外部のモジュールを使う

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

<br />

------

### 外部から使えるモジュール作成

外部から使えるモジュールを作成

モジュールとなるディレクトリを作成

```
mkdir greetings
cd greetings
```

go mod initコマンドでモジュールを初期化

```
go mod init example.com/greetings
go: creating new go.mod: module example.com/greetings
```

greetings.goファイルを作成し処理を記述する。

```
package greetings

import "fmt"

// Hello returns a greeting for the named person.
func Hello(name string) string {
    // Return a greeting that embeds the name in a message.
    message := fmt.Sprintf("Hi, %v. Welcome!", name)
    return message
}
```

func Hello(name string) string {} Helloのように大文字で始めると外部のモジュールから関数を呼び出せる。  
また、変数名nameの右側のstringは変数の型名を表している。{}の前のstringは戻り値の型を表している。

:=オペレーターは変数の宣言と初期化をするためのショートカット。

以上でgreetingsモジュールができたので、次は外部からこのモジュールを呼び出す。

greetingsモジュールと同じ階層にhelloモジュールを作りそこからgreetingsモジュールを呼び出す。

最初に作ったhelloモジュールのhello.goを以下に内容を変更する。

```
package main

import (
    "fmt"

    "example.com/greetings"
)

func main() {
    // Get a greeting message and print it.
    message := greetings.Hello("Gladys")
    fmt.Println(message)
}
```

- package main  
goのソースコードをアプリケーションとして実行するには、main packageを宣言する必要がある。

- import  
input/outputpの基本的な関数を利用するためにfmtモジュールをインポート、さっき作ったgreetingsモジュールをインポート。

外部からモジュールを呼び出して使うには、本当はモジュールを所定のパスに登録しそこからGo toolsがダウンロードして使うという処理になるけど、  
今回はモジュールを登録はしないので、ローカルのディレクトリ内のモジュールを結びつけるという感じの操作をする。

そのために下記のコマンドをhelloディレクトリ内で実行する。

```
 go mod edit -replace example.com/greetings=../greetings
```

するとhelloディレクトリのgo.modファイルの内容が下記のようにreplaceディレクティブによって変更される。

```
module example.com/hello

go 1.19

replace example.com/greetings => ../greetings
```

"example.com/hello" とgreetingsモジュールを結びつけるためにhelloディレクトリでgo mod tidyコマンドを実行する。

```
go mod tidy
go: found example.com/greetings in example.com/greetings v0.0.0-00010101000000-000000000000
```

helloディレクトリのgo.modファイルが下記のように変更される。

```
module example.com/hello

go 1.19

replace example.com/greetings => ../greetings

require example.com/greetings v0.0.0-00010101000000-000000000000
```

requireディレクティブによって、"example.com/hello" モジュールが"example.com/greetings" モジュールを使っていることが分かる。

v0.0.0-00010101000000-000000000000は疑似的なもので、疑似的なバージョンナンバーが生成されるようになっている。

番号の意味については、[モジュールのバージョン番号の定義についてのドキュメント](https://go.dev/doc/modules/version-numbers)を参照。

<br />

### errorハンドリングの追加

挨拶をするgreetingsモジュールを作り、helloモジュールからgreetingsモジュールを呼び出して  
使うということをできるようにしたが、そこにエラーハンドリングのコードを追加する。

名前を埋め込む部分がもし空白だったらエラーを返す。名前が有る場合は成功として通常のメソッドの実行結果と一緒に  
成功したことを示すnilも返す。

greetings/greetings.goのソースコードを下記のように変更する。

```
package greetings

import (
    "errors"
    "fmt"
)

// Hello returns a greeting for the named person.
func Hello(name string) (string, error) {
    // If no name was given, return an error with a message.
    if name == "" {
        return "", errors.New("empty name")
    }

    // If a name was received, return a value that embeds the name
    // in a greeting message.
    message := fmt.Sprintf("Hi, %v. Welcome!", name)
    return message, nil
}
```

コードの変更点：  
- Helloの返り値を2個に変更。文字列とerrorの2個を返す。自動的に、Helloを呼ぶ側モジュールがerrorがないかをチェックしてくれる。  
- errors.Newメソッドを使うために標準パッケージのerrorsをインポートする。  
- 名前が空のときはif文でエラー処理に分岐し、errors.Newメソッドによってエラーメッセージとerrorオブジェクトを返す。  
- エラーに分岐せず正常に処理ができたら、正常に処理できたオブジェクトとともに、エラーがないことを意味するnilオブジェクトも追加で返す。

次に、hello/hello.goを下記のように変更する。

```
package main

import (
    "fmt"
    "log"

    "example.com/greetings"
)

func main() {
    // Set properties of the predefined Logger, including
    // the log entry prefix and a flag to disable printing
    // the time, source file, and line number.
    log.SetPrefix("greetings: ")
    log.SetFlags(0)

    // Request a greeting message.
    message, err := greetings.Hello("")
    // If an error was returned, print it to the console and
    // exit the program.
    if err != nil {
        log.Fatal(err)
    }

    // If no error was returned, print the returned message
    // to the console.
    fmt.Println(message)
}

コードの変更点：  
- logパッケージを設定：log.SetPrefix("greetings: ")とすることでエラーのときにgreetingパッケージのログとわかるようにする。  
- log.SetFlags(0)とすることで、デフォルトで設定されている時刻、ファイル名、行番号の情報出力を無効にする。  
- Helloメソッドの実行結果として返ってくる正常処理、エラーの返り値を格納できるようmessage変数とerr変数を定義する。  
- エラーハンドリングを試すために、Helloメソッドの引数を空にする。  
- errにnilじゃなく値が入っていないかを確認する。greetings.Helloの第二引数に設定したerrorに値が入っている場合は、  
errにerrorの値が返ってくるので、その値をlog.Fatal(err)とすることで出力する。そして、log.Fatalメソッドはos.Exitメソッドを  
内部で実行し、プロセスを終了してくれる。以上のように、log.Fatalメソッドはエラーメッセージの出力とプロセス終了をする。  

<br />

helloディレクトリでソースコードを実行すると、エラーハンドリングされ、プロセスが終了することでプログラムを停止してくれる。

```
go run .
greetings: empty name
exit status 1
```



```
