## goでファイル操作をする

goを使って何かできることをしたいと思ったとき、思いついたのがファイルを開くなど、ファイル操作をgoで. 
やってみたいと思ったのでやり方をみていく。

ファイル操作の中でも基本のような気がするし、やってみたいし、できそうだと思う操作が、ファイルを開くという操作。

今回作成したソースコードが下のもの。

```
package main

import (
  "os"
  "fmt"
)

func main() {
  // 読み取り専用でtodo.txtを開く
  f, err := os.Open("/Users/katsuo/todo.txt")
  if err != nil {
    // fileopenに失敗した場合の例外処理
    fmt.Println(err)
    fmt.Println("fail to open file")
  }

  // deferでクローズ処理を記述
  defer f.Close()

  data := make([]byte, 1024)
  count, err := f.Read(data)
  if err != nil {
    fmt.Println(err)
    fmt.Println("fail to read file")
  }

// 挙動の確認

  fsize := fmt.Srintf("read %d bytes:\n", count)
  fmt.Println(fsize)
  fmt.Println(string(data[:count]))
```

読み取り専用でファイルを開いて、開いたファイルの内容を変数の箱に格納し、格納した内容を読み込んでターミナルの画面に出力するという流れとなる。

読み取り専用で開いて、開いたファイルの内容を読み取りできる関数で読み取って変数の記憶域に格納しその内容を出力する。



