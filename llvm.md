# LLVMを使うためのメモ

windows terminalでc++のコンパイルをするために環境を構築するときのメモ。  
pc: thinkpad yoga windows11home  

wingetでllvmをインストール。cmakeとninjaもインストール。ninjaはビルドが速くできるという特長がある。  

インストールしてpathが通ってなかったらパスを通す。

os側の準備として、c++の開発パッケージを同梱したvisual studioをインストールする。

<br />

## clangでhello world

hello.cppを作成

```
#include <iostream>
using namespace std;

int main() {
     cout << "hello world" << endl;
     return 0;
}
```

clangでコンパイル

```
> clang-cl.exe hello.cpp
//hello.exeが生成される
```

コンパイルされた実行ファイルを実行

```
> ./hello.exe
> hello world //実行結果が出力される
```

