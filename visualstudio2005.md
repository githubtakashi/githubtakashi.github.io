# Visual Studio 2005を習得するためのメモ

メルカリで入手したvisual studio 2005 standard editionを使って勉強進めるのでノートを書いていきます。  
なぜvisual studio 2005という古いバージョンのvisual studioを使うかというと、c++を使ったアプリを作れるようになりたい  
のもそうだけど、古いthinkpad使いたいという理由も大きいです。

古いthinkpadを使いたいけどネット接続はwindows XPなのでOSが古すぎて危険すぎるためネットにつなげられないです。  
visual studio 2005はwindows2000～xpまでのOSで使えるらしいので、  
windows xpのthinkpad T40pにインストールしました。

<br />

## visual studio 2005を使って勉強進める際の問題点

2000年代前半のvisual studioなのでvisual studio2005の情報がネット上にほとんど存在しないのでは?  
と思っていたけど、いろいろわからないことをググっていると今でも十分に情報が存在することが分かりました。

<br />

## MSDNライブラリを活用する

cd-romからインストールしたMSDNライブラリに充実した内容のコンテンツがいっぱいあるので、  
MSDNライブラリを活用するのがよさそうです。

チュートリアルが多くあるので、まずはチュートリアルを進めて作りつつ勉強していく方針で進めます。

<br />

## 用語など

チュートリアルを進めていくときにメモをとっていく。

### DLL

Dynamic Link Library(動的リンクライブラリ)

DLLとは、Windowsのプログラムファイルの種類のひとつ。いろいろなプログラムから利用される汎用性の高い機能が収録された  
部品化されたプログラム。拡張子は.dll。  
動的リンクライブラリという名前のとおり、プログラムの実行時に、必要なファイルを動的にリンクしてつなげる。

動的リンクは実行ファイルから参照されるライブラリなどを実行時に連結している。  
実行環境側でライブラリを用意する必要があるが実行ファイル本体を軽量にでき、  
他との依存性を低くできる(疎結合)ので部分的な修正や更新がしやすいというメリットがある。

静的リンクの場合は、リンカは参照される関数全部をstatic link libraryから取得して実行コード内に配置する。  
一方、dllの動的リンクは実行時での必要な情報だけ含めることが可能なので、メモリの節約など利点が多い。

#### リンカーとは

ソースコードから実行ファイルにする途中でリンカーが働く。c++はソースファイル単位での分割コンパイルが可能で、  
変更した箇所だけ再コンパイルすることでき、変更していない箇所はコンパイルをしなくていいので効率的。

ソースファイルを分割コンパイルしただけでは、パーツと同じで、ひとつにまとめないと機能をなさないので、  
分割コンパイルしたソースファイル(オブジェクトファイル)を結合する必要がある。  
そこで必要になってくるのがリンカー。

リンカーはオブジェクトファイルのシンボルテーブルを参照し外部で定義された関数やグローバル変数などを結合する。  
リンカーによって、分割コンパイル時には宣言しか存在しなかった関数や変数を実行時に呼び出すことができるようになる。

<br />

### スタティックライブラリ

dllはプログラムをビルド後の実行時に合体させるライブラリなのとは対照的に、  
スタティックライブラリはプログラムをビルドする時点で組み込んで、プログラムと合体させるライブラリのこと。

<br />

### ビルドしたときにメッセージで出てくるマニフェストとは

ビルドしたアプリケーションのランタイム依存について書かれたドキュメントをマニフェストという。  
マニフェストは外部ファイルか、ニーモックで書かれたアセンブリか、アプリ内に埋め込まれる。

<br />

### シンボルとは

プログラムデータベースファイル(.pdb)のことをシンボルファイルと呼ぶ。  
プログラムデータベースファイルとは、デバッグ時に作成されるファイルのことで、  
ソースコードをコンパイルするときに、ソースコードからpdbファイルが生成される。

pdbファイルには、プログラムに関するデバッグ情報とプログラムの状態が保持されていて、デバッグに役立てるためが目的。

<br />

## windows フォームコントロール

windowsのwindowの枠内に表示、機能させることができるアプリケーション。  
windowsフォームアプリケーション(共通言語ランタイム(下記参照)を対象にするGUIアプリケーション)に配置されるコンポーネントのことを  
フォームコントロールという。

<br />

### CLRとは

Common Language Runtime(共通言語ランタイム)の略で、.net applicationを実行するためのバーチャルマシンのこと。  
.net applicationとは、マイクロソフトが開発したアプリ開発/実行環境のこと。

CLRがマネージドコードの取得とコンパイルと実行を行う。

マネージドコードとは、実行がCLRによって管理されているコードのこと。

<br />

### マネージアセンブリとは

CLR(共通言語ランタイム)の環境を前提とした部品プログラムをマネージアセンブリと呼ぶ。

マネージドコードで部品化したプログラムのこと。部品化することで、他で参照して使える。  
作成するプログラムごとにいちいち部品を実装するのではなく、マネージアセンブリを作っておくと他のアプリケーションから  
マネージアセンブリをモジュールとして参照して使うことができる。

<br />

### プリコンパイル済みヘッダーファイルとは

ヘッダーファイルまたはヘッダーファイルに含まれるファイルの内容が変更された場合のみコンパイルされる機能のこと。  
コンパイル時間を短くしてくれるのでビルド時間が短くなる。  
すでにコンパイルが通っていて変更がないコードについては、解析の対象から除外することでコンパイル時間が短縮される。

<br />

### ref修飾子とは

ref修飾することで、参照渡しにできる修飾子。refから参照という機能を持っていることがイメージできる。

```
public ref class MyMathFuncs {//method...}
```

<br />

### gcnewとは

CLR環境で使う。参照渡し、値渡しのデータに対してマネージド型のメモリが割り当てられ、ガベージコレクションによって自動的にメモリが解放される。

```
if (b == 0)
{
  thwow gcnew DivideByZeroException("b cannot be Zero!");
}
```

<br />

***

## COMとは

Component Object Modelとは、マイクロソフトによる、ソフトウェアの機能を部品化し外部から呼び出して利用する仕組みのこと。  
OSやプログラミング言語に依存しないので、様々な言語やOSで開発されたプログラムを連携できる。

COMにおいて、部品化された（単体では動作しない）ソフトウェアをCOMコンポーネントと呼ぶ。  
COMコンポーネントは、アプリケーションに組み込むことでその機能を呼び出し利用するような使い方をする。

コンポーネントオブジェクトモデル(COM)と分散コンポーネントオブジェクトモデル(DCOM)は、リモートプロシージャコール(RPC)を使用して  
分散コンポーネントオブジェクトが相互に通信する。通信するために、COMインターフェイスまたはDCOMインターフェイスはCOMオブジェクトの  
idと外部特性を定義する必要がある。定義することによって、クライアント側からCOMオブジェクトのメソッドとデータにアクセスできる。  
DCOMではオブジェクトが同じプロセス内に存在するか、同じコンピューター上の異なるプロセスに存在するか、異なるコンピューターに  
存在するかに関係なくアクセスが可能。

<br />

### COMサーバーとは

COMを利用するとき、COMを使う側のアプリケーションソフトウェアは、直接COMコンポーネントとやり取りするのではなく、  
COMインターフェースを介してCOMコンポーネントと通信を行う。COMコンポーネントを提供するものがCOMサーバー。

COMサーバーにCOMコンポーネントが格納されていて、外部からはCOMインターフェースを介してCOMコンポーネントを利用するイメージ。  

<br />

### ATL(Active Template Library)とは

COM開発を簡単にするためのラッパーライブラリ。テンプレート。  
ActiveXコントロールを作成するために使われることが多い。  
ActiveXコントロールはマイクロソフトが開発した機能で、Webサイトでビデオやゲームなどのコンテンツを提供できる小さなアプリ。  
ActiveXコントロールを使って、Webを閲覧するときにツールバーや株価表示などのコンテンツを操作することもできる。

<br /> 

### MFC(Microsoft Foundation Classes)とは

Visual C++でWindows用のアプリ構築するときに利用するクラスライブラリATLと一緒にVisual Studioに同梱されていて、  
一般的にアプリでよく使われるクラスが準備されている。

<br />

### regsvr32

windowsのコマンド。Microsoft Register Serverの略で、  
dllファイルの登録やOLE（Object Linking and Embedding）コントロールの登録や解除の時に使うコマンド。

regsvr32コマンドでDLLファイルを登録すると、dllファイルについての情報がWindowsレジストリ(下記参照)に追加される。  
これによって、他のプログラムからレジストリ内でアクセスできるようになり参照されるようになる。

windowsのレジストリとは:  
様々な設定情報、システム情報が格納されたデータベースのこと。

例)サーバーオブジェクトであるTestServer.cppをdllオプションでコンパイルしサーバー(windowsレジストリ)に登録

```
> cl /LD TestServer.cpp
> regsvr32 TestServer.dll
```

<br />

### HRESULT型

HRESULT型はlong型(大きい桁数の整数を格納できる変数型)の数値で、COMインターフェース関係の関数の返り値に使われることが多い型。  
BOOL型と似ていて、大きな違いはBOOL型は返り値としてtrueかfalse、0か1しかないのに対し、  
HRESULT型は0x00000000～0xFFFFFFFFまでの多くの値が使える。その値に意味を与えられるので、  
true,falseとは対照的に値に応じた意味合いを細かく定義できる。  

BOOL型ではfalseの原因を取得したいときはGetLastError()を使う必要があったが、HRESULT型を利用することで、返り値の値を見るだけで  
falseの原因まで分かるようになっている。

***

<br />

### IDispatch

COMでイベント処理を行うときに使うインターフェース。他のいろんなCOMインターフェースを呼び出すことができる。  
COMサーバーの実装ファイルの中で宣言する。

<br />

### coclass

COMのクラスのことをcoclassと呼ぶ。"COM"+"クラス"でcoclass。

<br />

### threading

threadクラスはスレッド(下記参照)を作成して制御し、優先順位の設定やステータスの取得を行う。  
並列で動くthreadがdeadlockやrace conditionsにならないように制御してくれる機能をCOMが提供している。

race conditionsとは:  
並列動作するプロセスやスレッドが同じリソースにほぼ同時にアクセスしたときに予定外の処理結果が起こってしまうこと。

プロセスの中のCOMオブジェクトはApartmentと呼ぶグループに所属していると考える。  
1つのCOMオブジェクトは1つのApartmentの中に存在する。COMオブジェクトが呼び出すメソッドはApartmentに所属するスレッド  
から呼び出されるということになる。

そのApartmentに属していない他のスレッドからCOMオブジェクトを呼び出すときには、プロキシ(代理)を通じて呼び出すようになっている。

COMにおけるApartmentはSingleThreaded ApartmentとMultiThreaded Apartmentに分類される。

SingleThreaded Apartment:  
SingleThreaded Apartmentのスレッドとの同期をwindowsのメッセージキュー(下記参照)を利用して同期する。  
このメッセージキューはSingleThreadedApartment専用のキューがあり利用される。

MultiThreaded Apartment:  
windowsのメッセージキューは使わず、COMオブジェクト同士が直接通信して同期を行う。

#### スレッドとは

プロセスとは仮想記憶に格納したコードやデータやリソースなどまとまりのことで、プロセスの中で実行されるコードを  
スレッドと呼ぶ。

CPUが実行するのはプロセスではなくて、スレッドを実行する。

上記から、一つのアプリケーションは最低でも1つのプロセスを持っており、プロセスが1つあるということは  
最低でも1つの実行するスレッドを持っているということになる。これをprimary threadと呼ぶ。

プロセスはprimary threadに加えて複数のスレッドを持てる。  

異なるプロセスがお互いに通信するときはRPC(Remote Procedure Call)(下記参照)というメッセージ通信の機能を使う。

スレッドが実行されると、強制的に停止されるか優先度の高いスレッドに割り込みされるまでは実行が継続される。  
ユーザーが実行を止めた時にはスレッドは停止する。  
カーネルのスレッドスケジューラー(下記参照)が優先度を管理して優先度に沿ってスレッドを実行する。  

ソースコードの中で異なるコードセクションにそれぞれ存在するスレッドはそれぞれ並行して走らせることができる。  
また、一つのコードセクション内に存在する複数のスレッドを並行して走らせることができる。  
プロセスで使うグローバル変数やリソースは複数のスレッドで共有して利用する。

複数のスレッドを走らせるマルチスレッドで問題になってくるのがdead lockとrace condition(下記参照)。  
COMはdead lockとrace conditionを避ける機能がある。

シングルスレッドだと同時に1つのスレッドしか走らせられないのでマルチスレッドの方が効率がよいと思いがちだけど、  
内容を把握せずただマルチスレッドを走らせるだけだとパフォーマンスの低下などの問題が発生するので、マルチスレッドで  
しようとしていることの内容と動作を完全に把握しておかないと逆効果となり、マルチスレッドを使いこなせない。

<br />

##### RPCとは  
プログラムから共有ネットワークにある別のコンピュータのアドレス空間にあるサブルーチンや手続きを実行できる技術。  

##### サブルーチンとは  
プログラム中で意味や内容がまとまっている処理を一つの手続きとしてまとめたもの。モジュールと同じ意味。  
メインとなるプログラム(メインルーチン)から呼び出される側なのでサブルーチンと呼ばれる。

##### 手続き(プロシージャ)とは  
複数の処理をまとめたもの。まとめることで再利用しやすくなる。何度も同じ処理を書かなくてもよくなるイメージ。

<br />

##### スレッドスケジューラー

スレッドの実行を管理するスレッドスケジューラーはスレッドをどんなタイミング、どんな頻度で実行するかを  
プロセスの優先クラス属性とスレッドのベース優先度に基づいて決定する。

プロセスの優先クラス属性はSetPriorityClass関数を使うことでユーザーがスレッドの優先度を設定できる。  
また、スレッドのベース優先度はSetThreadPriority関数で設定できる。

上記をまとめると、スレッドスケジューラーでプロセスの優先度とスレッドの優先度を設定できるということ。

<br />

##### race conditionとは

複数のスレッドが共通の1つのコードブロックに到達して実行できる状態。影響としては、どのスレッドが最初にコードに到達するかによって  
結果が変わってしまい、プログラムが不安定になるといったことが起こる。

<br />

### メッセージキューとは

windowsのアプリケーションはイベント駆動型のプログラムなので、メッセージを受け取り  
それに基づいて処理を行う。

イベント駆動のもとになるメッセージがメッセージキューに入っている。昔のOSだとシステム全体で1つしかない  
メッセージキューからメッセージを取り出していた。他の処理にcpuが取られているとメッセージキュー  
からメッセージを送り出すことができないので、メッセージが届かないため処理も行われない。  
それがシステムの停止(フリーズ)につながっていた。

以降、32bitアプリケーションではスレッドごとにメッセージキューを持っている仕組みとなった。  
受信側がメッセージを取り出すまでメッセージはキューに格納されたままで、必要なタイミングで取り出される。

<br />

## no_namespace

no_namespaceインポート属性で、コンパイラに名前空間の生成をしないことを指定するための属性。

書式：#importタイプライブラリno_namespace
  
#importディレクティブはmicrosoft固有のもので、COMで使われていたもの。現在は使われていない?!  
#importディレクティブを宣言することで、タイプライブラリのコンポーネントが持っているインターフェイスや  
CoClassが有効になる。

- タイプライブラリとは、COMコンポーネントの型情報を格納した型ライブラリで、ファイルの拡張子は.tlb

タイプライブラリは独立したファイルとして読み込むことも可能。  
ふつうタイプライブラリは実行可能ファイルの.exeや.dllファイルのリソースに埋め込まれている。

タイプライブラリ(.tlb)はCOMまたはDCOMオブジェクトのプロパティおよびメソッドの情報を実行時に  
他のアプリケーションからアクセスできる形式で格納するバイナリファイル。  
タイプライブラリを使用するとアプリケーションまたはブラウザーからCOMオブジェクトのインターフェイスメソッドを呼び出せる。  

<br />

### CoInitialize()とCoUninitialize()

COMサーバーでのCOMコンポーネントを利用するCOMクライアントプログラムのコンストラクタ　　
とデストラクタにそれぞれ記述する。

CoInitialize()はスレッド毎に呼ばれる。  
スレッドと1対1に対応付けされるApartmentのSingle Thread Apartment(STA)を作成するために初期化を行う関数。

```
struct A {
  A() { CoInitialize(NULL); }
  ~A() { CoUninitialize(); }
}A;
```

<br />

### tmain

mainのようなもの。tmainはc++にはなく、microsoftの拡張機能。  
tmainはコマンドライン引数argcとargvの部分について、コマンドライン引数の種類によって  
適切に条件分岐される仕様となっている。

```
int _tmain(int argc, _TCHAR* argv[])
{
...
}
```

コマンドライン引数に渡される文字列がワイド文字かマルチバイト文字列かによって、tmainによってそれに対応した処理がされるよう  
内部的に切り替わるようになっている(ソースコードをユニコードと非ユニコード両対応にするための型)。

#### argcとargvとは

- argc: argument countの意味で、argvの配列数を示している。

- argv: argument vectorの意味で、コマンドライン引数に渡す配列情報を示している。

argvは文字列へのダブルポインタ変数になっている。

```
int main(int argc, char** argv)
```

例えば、コマンドラインから2つの文字列の引数を渡した場合。

"hello world" "neko"

それぞれの変数は異なるアドレスに格納される。

コマンドライン引数を2個渡したら下記のように3この文字列が格納されるようになっている。

100番地：{C:\c++\nekoProject\Debug\nekoProject.exe}  
200番地：{hello world}  
300番地：{neko}

コマンドライン引数を2個渡したのに3個格納される理由は、アプリケーションプログラムを  
実行したパスとファイル名が渡されるようになっているから。

なので、コマンドライン引数に何も渡さなくても、1つは必ず自動的に上記のようにパス+ファイル名  
が渡されるようになっている。

つぎに、上記3つの文字列のアドレスをまとめて格納した下記のような配列が作られる。

{100番地, 200番地, 300番地}

この配列がポインタになっていて、それぞれのアドレス(100, 200, 300番地)を参照している。->１つめのポインタ。

さらにこの配列を参照しているのが、argv変数のポインタ。  
argvの番地を1000番地とすると、1000番地のargvから{100,200,300番地}をポンタで参照している。->2つめのポインタ。

以上のように、argvは文字列配列へのダブルポインタとなっている。

argcのほうは文字列配列の個数を管理している。

<br />

### CComPtr

COMのインターフェースポインターを管理するためのスマートポインタークラス。

下記のように宣言して使う。

```
CComPtr<IUnknown> spUnknown;
```

<br />

### IUnknown

IUnknownインターフェースはCOMの基盤的な抽象型。  
COMの仕様ではすべてのCOMオブジェクトはIUnknownインターフェイスを実装しなきゃいけないとされてて必須のもの。  
IUnknownはCOMのルートクラスで、すべてのCOMインターフェースはIUnknownから派生したもの。

<br />

### CoCreateInstance()

COMインスタンスを生成するためのメソッド。  
サンプルコード

```
CComPtr<IUnknown> spUnknown;
spUnknown.CoCreateInstance(__uuidof(COobject1));
...
```

#### __uuidof

式にはその型の型名やポインターや参照や配列やこれらの型に特化したテンプレートや、これらの型の変数を指定できる。  
引数は、アタッチされたGUIDを見つけるためにコンパイラが使用できる限り有効。  
GUIDとはglobally unique identifierの略で、uuidの別名。グローバル一意識別子。  
UUIDとはuniversally unique identifierの略。ソフトフェア上でオブジェクトを一意に識別するための識別子。

<br />

### インプロセスサーバーとアウトプロセスサーバー

インプロセスサーバーはdllファイルに実装されるサーバーのこと。  
dllファイルを使ったCOMサーバーをインプロセスサーバーとよぶ。  
アウトプロセスサーバーはexeファイルに実装されるサーバーのこと。  

<br />

### HANDLE

Windowsの持っているリソースを表すための型。ウィンドウならHWND、デバイスコンテキストならHDCというように  
それぞれ専用の型があり、それの総称をHANDLEと呼ぶ。  

デバイスコンテキストとは、ディスプレイやプリンターなどのデバイスの描画属性に関する情報を含んだ、Windowsのデータ構造体。

<br />

***

## COMサーバーのヘッダーファイル

comサーバーのヘッダーファイルに書かれている内容を下記に書いていく。

### define STRICT

STRICT を <Windows.h> をインクルードする前に定義しておくとHANDLEの扱いが厳密になる。新しいvisual studioでは  
宣言しなくてもデフォルトで有効になっている。昔は宣言する必要があった。

<br />

### ifndef _WIN32_WINNT

_WIN32_WINNTは、コードがサポートするオペレーティングシステムの最小バージョンを指定する。 

例

```
#ifndef _WIN32_WINNT
#define _WIN32_WINNT 0x0400
#endif
```

ウィンドウズのバージョンは下記のような定数が存在する。

```
// _WIN32_WINNT version constants  
//  
#define _WIN32_WINNT_NT4                    0x0400 // Windows NT 4.0  
#define _WIN32_WINNT_WIN2K                  0x0500 // Windows 2000  
#define _WIN32_WINNT_WINXP                  0x0501 // Windows XP  
#define _WIN32_WINNT_WS03                   0x0502 // Windows Server 2003  
#define _WIN32_WINNT_WIN6                   0x0600 // Windows Vista  
#define _WIN32_WINNT_VISTA                  0x0600 // Windows Vista  
#define _WIN32_WINNT_WS08                   0x0600 // Windows Server 2008  
#define _WIN32_WINNT_LONGHORN               0x0600 // Windows Vista  
#define _WIN32_WINNT_WIN7                   0x0601 // Windows 7
#define _WIN32_WINNT_WIN8                   0x0602 // Windows 8
#define _WIN32_WINNT_WINBLUE                0x0603 // Windows 8.1
#define _WIN32_WINNT_WINTHRESHOLD           0x0A00 // Windows 10
#define _WIN32_WINNT_WIN10                  0x0A00 // Windows 10
// . . .
```

<br />

### define _ATL_ATTRIBUTES

ATLプログラミングに役立つ属性を使えるようにするための宣言。

<br />

### define _ATL_APARTMENT_THREADED

マクロによるコンパイラオプションの設定で、特定のコンパイラ機能を制御するための  
マクロの宣言。1つ以上のオブジェクトでアパートメントスレッド処理を使用する場合に宣言。  

<br />

### define __AUTOMATIC_NAMESPACE

マクロによるコンパイラオプションの設定で、特定のコンパイラ機能を制御するための  
マクロの宣言。ATLを既定の名前空間として使用しないためのシンボル。  
このシンボルが定義されていない場合はatlbase.hを含め既定で名前空間ATLを使用して実行され、名前付けの競合が発生する可能性がある。  
これを防ぐためにこのシンボルを定義する。

<br />

### include <atlbase.h>

ATLをインクルードするためのヘッダーファイル。
以下、"atl"の付くヘッダーファイル名はアプリケーションにATLのサポートを加えるためのもの。

<br />
 
### include <atlcom.h>

ATLをインクルードするためのヘッダーファイル。

<br />

### include <atlwin.h>

ATLをインクルードするためのヘッダーファイル。

<br />

### include <atltypes.h>

ATLをインクルードするためのヘッダーファイル。

<br />

### include <atlctl.h>

ATLをインクルードするためのヘッダーファイル。

<br />

### include <atlhost.h>

ATLをインクルードするためのヘッダーファイル。

<br />

***

### idlファイル(COM)

IDLはinterface definition languageの略で、インターフェイスとタイプライブラリの定義を含むファイルはIDLファイルとよび、.idlファイル名拡張子が付いている。  
IDLファイルは、ネットワーク上のアプリケーションのインターフェイス特性(クライアントとサーバー間のデータの送信方法、またはCOMオブジェクト間のデータの送信方法)を指定する。

あるプログラム言語のソースファイルの中に、IDL仕様の書き方でインターフェースの情報を記述することで定義する形式で書く。  
"[]"の中に記述することが特徴。

## サーバーオブジェクトを実装したソースファイルを作成する

ファイル名をMyServer.cppとする

```
//MyServer.cpp fileの中身
#include "MyIncludes.h"

[ module(dll, name = "MyServer", helpstring = "MyServer 1.0 Type Library") ];
[ emitdl ];

//IObject1
[
  object,
  uuid("103FF...."),
  dual,
  helpstring("IObject1 Interface"),
  pointer_default(unique)
]
__interface IObject1 : IDispatch
{
  HRESULT GetANum([out, retval]int* pInt);
};
//CObject1
[
  coclass,
  threading(apartment),
  vi_progid("MyServer.Object1.1"),
  version(1.0),
  uuid("15615...."),
  helpstring("Object1 Class")
]
class ATL_NO_VTABLE CObject1 :
  public IObject1
{
public:
  CObject1()
  {
  }
  HRESULT GetANum(int* pInt){
    *pInt = 101;
    return S_OK;
  }
  DECLARE_PROTECT_FINAL_CONSTRUCT()
  HRESULT FinalConstruct()
  {
    return S_OK;
  }
  
  void FinalRelease()
  {
  }
};
```

上記コードによって、メソッドを1つ持つカスタムインターフェース(IObject1)を実装したCOMオブジェクト(CObject1)が作成される。  
GetANumメソッドは、データメンバの値(int型)を返す。

"[]"の中の項目はIDL属性という。

### IDL属性の説明

object属性:  
インターフェイス定義の前にobject属性を指定すると、インターフェイスはカスタムインターフェイスとして.idlファイルに配置される。

uuid属性:  
uuidは、定義するインターフェイス、タイプライブラリ、coclassを一意に識別するためのIDで、  
SDKツールのuuidgenというコマンドで作成できる。

dual属性:  
idlファイル内のインターフェイスをデュアルインターフェイスとして設定。  
デュアルインターフェースとは、c++と、c++以外のスクリプト言語のどちらからもCOMサーバーを利用できるよう対応した  
インターフェースのことで、IDispatchから派生したもの。

デュアルインターフェース自体の意味がなかなかググっても見つからなかったけど[こちらの記事](https://ichigopack.net/win32com/com_dual_1.html)で説明されている。

helpstring属性:   
helpstringにインターフェースの名称を設定しておくと、IDEのGUIで名称が表示される。ツールチップやカーソルホバーで表示されたりする。

pointer_default属性:  
インターフェイスの引数で使用するポインタのデフォルトの属性(機能、挙動)を定義する。  
pointer_default(属性)という使い方。どの属性を定義するかによってポインターの機能が違ってくる。  
引数に渡す属性は3種類ほどある。ref,ptr,unique。  
refは参照ポインタ属性、prtはフルポインタ属性、uniqueはユニーク属性

refは間接参照の機能を持ったポインタ。  
uniqueは、あるメモリに対する所有権を持つポインタが、ただ一つであることを保証するようなポインタ。<-多分。  
ptrは、C言語のポインタ機能を備えたポインタのこと。  

__interface属性:  
下記のように使う。

```
modifier __interface interface-name {interface-definition};
```

サンプルコードではIObject1という名前のインターフェースを定義している。  
{}の中にインターフェースの定義を書く。

```
__interface IObject1 : IDispatch
{
  HRESULT GetANum([out, retval]int* pInt);
};
```

:IDispatchと書くことによって、IDispatchを継承することを意味する。

\[out, retval]は、引数の属性を表している。outは方向属性といい、outは出力のこと。  
inなら入力のこと。retvalは戻り値のこと。

マネージドコードとアンマネージドコードの間でメソッドの引数データをやり取りするときに、型の変換をする  
必要があり、それをマーシャリングとよぶ。inまたはoutはマーシャリングの方向性(タイミング)の違い。

inは呼び出す時に（前）に引数データをマーシャリングする。  
outは呼び出し先から戻る時に引数データをマーシャリングする。

<br />

coclass属性:  
生成されたidlファイルにcoclassコンストラクトを配置する。  
coclassを定義するときにuuid,version,threading,vi_progid属性をセットで指定する。

ATL_NO_VTABLE属性:  
ATL(Active Template Library)はCOMオブジェクトを簡単に作成できる  
Visua C++用のテンプレートライブラリ。  
COMインターフェースなのでvtableへのアクセスが不要なので、ATL_NO_VTABLE属性をつける。  

module属性:  
.idlファイルのライブラリブロックを定義するための属性。  
module属性を使うと、COMインプロセスサーバーに必要な機能を実装する手間が省ける。  
また、idlファイルまたはdefファイル(サーバーの関数をエクスポートするファイル)を記述する必要がない。

module属性の例：

```
[ module (type=dll, name=string, version=1.0, uuid=uuid, lcid=integer, control=boolean, helpstring=string, helpstringdll=string, helpfile=string, helpcontext=integer, helpstringcontext=integer, hidden=boolean, restricted=boolean, custom=string, resource_name=string,) ];
```

module属性で使えるパラメータの説明：

type=dll: DLLをインプロセスCOM サーバーとして機能できるように関数とクラスを追加する。 これ(dll)が既定値。  

name: ライブラリブロックの名称。"Myserver"など、機能に合った分かりやすい名前にする。  

helpstring: タイプライブラリの名称。

<br />

### emitidl属性

emitdl属性によって、後続のすべてのIDL属性を処理し、生成されたidlファイルに配置するかどうかを指定する。  
ソースコードファイルでemitidl属性が検出されると、生成されたidlファイルにIDLカテゴリ属性が配置。  
emitidl属性がない場合は、ソースコードファイル内のIDL属性が生成されたidlファイルに出力される。

### VTable

呼ばれたらどの関数を返すかについての情報を持ったテーブルみたいなイメージ。  
ポインタでメソッドを使うときに、ポインタが参照する仮想関数が2種類以上とかあって、どれを使えば分からなくなるのを  
VTableを利用することで防ぎ、適切な仮想関数を参照してくれる仕組み。

[分かりやすい記事](https://qiita.com/4_mio_11/items/aa71f18b24ab55e4cb3d)を参照。

<br />


### DECLARE_PROTECT_FINAL_CONSTRUCT

FinalConstructで内部の集計されるオブジェクトによって参照カウントが増やされ、カウントが0に減らされても、  
オブジェクトが削除されないように保護するための集計マクロ。

```
DECLARE_PROTECT_FINAL_CONSTRUCT()
  HRESULT FinalConstruct()
  {
    return S_OK;
  }
```
HRESULT FinalConstruct()：  
派生クラスでこのメソッドをオーバーライドして、オブジェクトに必要な初期化を実行できる。  
正常に実行できたらS_OKをリターンする(return 0;よりも意味合いが分かりやすいのでS_OKを使っている)。  
エラーだとHRESULT型のエラー値がリターンされる。

<br />


### void FinalRelease()

オブジェクトのメモリ解放をする。

```
 void FinalRelease()
  {
  }
```

<br />

## COMサーバーアプリケーションをビルド

ヘッダーファイルのMyIncludes.hとCOMサーバーオブジェクトのMyServer.cppを作成したら、ビルドをして
COMサーバーオブジェクトをwindowsに登録する。

```
> cl /LD MyServer.cpp
> regsvr32 MyServer.dll
```

## テスト用のクライアントアプリケーションを作成

作成したCOMサーバーがちゃんと使えるかを確認するため、作成したCOMサーバーを利用するクライアントアプリケーションを  
作成する。

ファイル名：  
クライアントアプリケーションのファイル名はComtest.cppとする。

```
//Comtest.cpp
#include <iostream>
#include "atlbase.h"
#import "vc80.tlb" no_namespace
using namespace std;
int main()
{
    CoInitialize(NULL);
    {
        CComPtr<IUnknown> spUnknown;
            spUnknown.CoCreateInstance(__uuidof(CObject1));
        CComPtr<IOblect1> pI;
        spUnknown.QueryInterface(&pI);
        int res = 0;
        res = pI->GetANum();
        cout << res << endl;
    }
    CoUninitialize();
}
```

クライアント側でCOMサーバーの正しい動作を認識するために、#importキーワードを使って、作成したCOMサーバーのタイプライブラリを  
インポートする。インポートすることで、作成したCOMサーバーの機能を使えるようになる。

COMサーバーを作成するときにコンパイラによって生成されたタイプライブラリの名前は、"vc80.tlb"なのでこのファイルをインポートする。

```
#import "vc80.tlb" no_namespace
```

no_namespace属性を付けることで、コンパイラがインポートしたvc80.tlbタイプライブラリの名前空間を生成しないことを指定できる。

インポートしたCOMサーバーのインスタンスを使うときは、CoInitialize()とCoUninitialize()をセットで宣言する必要がある。
(コンストラクタとデストラクタ)


### ストレージクラス

変数や定数のデータを格納したメモリ領域をオブジェクトと呼ぶ。  
オブジェクトが格納されたメモリ空間の種類をストレージクラスと呼ぶ。

オブジェクトはライフタイムとかデータのアクセス保護情報の違いによって分類され、異なる種類のメモリ空間に格納される。  
同じメモリ空間に属す場合でも、初期値によってその初期化方法が異なる場合がある。  
それらのメモリ空間はそれぞれ異なるアクセス保護がされる。  
ストレージクラスとは、オブジェクトがそれらどのメモリ空間に属するかを指すためのもの。  

メモリ空間の種類は言語処理系に依存する。代表的なメモリ空間は下記。

- スタック領域  
言語処理系が必要に応じてメモリを確保したり解放したりするメモリ空間

- ヒープ領域  
プログラムを組む人が自由に確保したり解放の操作をしてよいメモリ空間

- データ領域  
言語処理系が使用する固定サイズのメモリ空間で、プログラムの開始時にメモリが確保され、終了時に解放される。

- テキスト領域  
命令列が格納されるメモリ空間。

- 各メモリ領域の配置のされ方  
テキスト領域とデータ領域とヒープ領域はそれぞれ順番にアドレス番号の小さい方に配置される。  
スタック領域はアドレス番号の大きい方に配置される。  
領域の拡大については、スタック領域はアドレス番号の大きいものから小さい方へと、ヒープ領域はアドレス番号の小さいものから大きい方へと領域を拡大させる。  

ストレージクラスは、オブジェクトがヒープ領域、スタック領域、データ領域のどの領域に属すかで分類する。

- 自動ストレージ  
関数内で定義されたローカルスコープの変数はstatic宣言される場合を除いて  
自動ストレージ(スタック領域)に格納される。自動ストレージに配置されたデータは関数が呼ばれた時に呼び出し元に割り当てられ、  
呼び出した元に制御が戻るときに割り当てが開放される。  
再帰的に関数が呼び出されたら、ある関数のあるデータはスタック領域に複数存在することになる。

- 静的ストレージ  
グローバルスコープや名前空間スコープで宣言される変数および関数やクラス内でstatic宣言される変数は  
静的ストレージ(データ領域)に格納される。リンカはプログラムが実行を開始する前に静的ストレージに変数を格納する。

- フリーストア  
newで作成されたオブジェクトはフリーストア(ヒープ領域)に格納される。格納されたデータはdeleteでヒープ領域から削除される。

どのストレージクラスにインスタンスを格納させるかを指定できるのが、microsoft固有の仕様の_declspec。  
この機能を利用することで、指定された型のインスタンスがMicrosoftに固有のストレージクラス属性を使用して格納されることを指定できる。

ストレージクラス属性にはいろいろな種類がある。staticやexternはmicrosoft固有じゃなくc++に存在する標準の仕様なので、これら以外の  
ストレージクラス属性をmicrosoftが準備している。

<br />

## __declspec(dllexport)

dll作成の時にメソッド宣言に付ける。
dllをエクスポートして他のアプリケーションで使えるようにするために付加する修飾子。

<br />

## visual C++ /EHsc

/EHscはコンパイラに対して例外処理を有効化するためのオプション。

<br />

## visual c++ /LD

/LDオプションはDLLを作成するために必要なオプション。

visual studioのメニューでdllになるようにビルド設定してビルドすると自動的に/LDオプションでdllが作成される。

コマンドラインからビルドするときは/LDコンパイラオプションを使用し出力ファイルがdllになるようにする。

<br />

## clコマンドとは

clとはvisual C++のコンパイラのことで、visual c++に付属しているコマンドラインで

clコマンドを実行するとソースファイルを手動でコンパイルできる。

例)コンパイルする例

/LDオプションでコンパイルすることでdllを作成

```
> cl /LD test.cpp
```

<br />


## <stdexcept>ヘッダーファイル

stdexceptヘッダをインクルードすると標準的な例外処理のクラスが使えるようになる。
  
```
#include <stdexcept>
using namespace std;
```
  
std名前空間で使えるのでusing namespace stdを宣言する必要がある。
  
<br />
  
## stdafx.hヘッダーファイルとは

プリコンパイル済みヘッダーファイルのこと。
visual c++のプロジェクトのcppファイルにデフォルトで書かれている。
  
<br />

## VTableとは

クラスのポインターが与えられ、そのポインターから仮想関数を呼び出すとき、  
継承関係を考慮した上で適切なクラスのメンバ関数を呼び出せる仕組み。
  
<br />
  
## OLEとは
  
Object Linking and Embeddingの略で、windowsの機能。複数のソフトウェアが連携したり、  
データを共有するしくみ。のちにActiveXに名称が変更された。

<br />
  
## ActiveXとは
  
ActiveX コントロールはCOM:Component Object Modelに基づく再利用可能なソフトウェアコンポーネント。  
多岐にわたるOLEの機能をサポートしていて、いろんなソフトウェアの要件に合わせてカスタマイズができる。  
※しかしレガシーな技術なので、現在は非推奨の技術となっている。
  
<br />
  
## ActiveXコントロールの作成(ウィザードを利用)

ActiveXコントロールを作成する手順を書いていく。  
プロジェクト名は"MyAxCtrl"とする。  
  
### Visual C++のIDEでATLプロジェクトウィザードを使用してプロジェクトを作成

"ファイル"メニューの"新規作成"→"プロジェクト"をクリック。  
"visual c++プロジェクト"をクリック、テンプレートペインの"ATLプロジェクト"をクリック。  
"プロジェクト名"を入力しokをクリック。すると、ATLプロジェクトウィザードが表示される。  
"属性"のチェックボックスと"DLL"をオンにして完了をクリックするとプロジェクトが生成され、    
ActiveXコントロールのコンテナとなるvisual c++のDLLプロジェクトが生成される。

### ATLコントロールコンポーネントをプロジェクトに追加

"クラスの追加"ダイアログボックスでは、visual c++のIDEプロジェクトに追加するいろんなコンポーネントが  
フレームワークとして提供されている。
  
ATLコントロールコンポーネントもそのひとつで、"クラスの追加"で利用できる。

ソリューションエクスプローラでプロジェクト名の"MyAxCrtl"を右クリックし、"追加"→"クラスの追加"をクリック。  
クラスの追加ダイアログボックスが表示される。  
カテゴリーで"ATL"をクリックし、"ATLコントロール"をダブルクリックすると、"ATLコントロールウィザード"が表示される。  
"短い名前"に"MyCtl"と入力し、"完了"をクリックすると、MyAxCtrlプロジェクトにATLコントロールが追加される。  
追加によって、ヘッダーファイルとcppファイルが生成される。
  
//MyCtl.h  
  
```
//MyCtl.h : CMyCtlの宣言
#pragma once
#include "resource.h" //メインシンボル
#include <atlctl.h>

#if defined(_WIN32_WCE) && !defined(_CE_DCOM) && !defined(_CE_ALLOW_SINGLE_THREADED_OBJECTS_IN_MTA)
#error "DCOMの完全サポートを含んでいないWindows MobileプラットフォームのようなWindows CEプラットフォームでは、単一スレッドCOMオブジェクトは正しくサポートされていません。ATLが単一スレッドCOMオブジェクトの作成をサポートすること、およびその単一スレッドCOMオブジェクトの実装の仕様を許可することを強制するには、_CE_ALLOW_SINGLE_THREADED_OBJECTS_IN_MTAを定義してください。ご使用のresファイルのスレッドモデルは'free'に設定されており、DCOM Windows CE以外のプラットフォームでサポートされる唯一のスレッドモデルと設定されていました。"
#endif

//CMyCtl
[
  coclass,
  control,
  default(IMyCtl),
  threading(apartment),
  vi_progid("MyAxCtrl.MyCtl"),
  progid("MyAxCtrl.MyCtl.1"),
  version(1.0),
  uuid("804A28DB-6768-42B0-AD2A-0C326CB489F7"),
  helpstring("MyCtl Class"),
  support_error_info(IMyCtl),
  registration_script("control.rgs")
]
class ATL_NO_VTABLE CMyCtl :
  public IMyCtl,
  public IPersistStreamInitImpl<CMyCtl>,
  public IOleControlImpl<CMyCtl>,
  public IOleObjectImpl<CMyCtl>,
  public IOleInPlaceActiveObjectImpl<CMyCtl>,
  public IViewObjectExImpl<CMyCtl>,
  public IOleInPlaceObjectWindowlessImpl<CMyCtl>,
  public IPersistStorageImpl<CMyCtl>,
  public ISpecifyPropertyPagesImpl<CMyCtl>,
  public IQuickActivateImpl<CMyCtl>,
#ifndef _WIN32_WCE
  public IDataObjectImpl<CMyCtl>,
#endif
  public IProvideClassInfo2Impl<&__uuidof(CMyCtl), NULL>,
#ifdef _WIN32_WCE // コントロールを正常に読み込むのにWindows CE上にIObjectSaftyが必要
  public IObjectSaftyImpl<CMyCtl, INTERFACESAFE_FOR_UNTRUSTED_CALLER>,
#endif
  public CComControl<>CMyCtl>
{
public:
  
  CMyCtl()
  {
  }

DECLARE_OLEMISC_STATUS(OLEMISC_RECOMPOSEONRESIZE |
  OLEMISC_CANTLINKINSIDE |
  OLEMISC_INSIDEOUT |
  OLEMISC_ACTIVATEWHENVISIBLE |
  OLEMISC_SETCLIENTSITEFIRST  
)
  
BEGIN_PROP_MAP(CMyCtl)
  PROP_DATA_ENTRY("_cx", m_sizeExtent.cx, VT_UI4)
  PROP_DATA_ENTRY("_cy", m_sizeExtent.cy, VT_UI4)
  //エントリの例
  //PROP_ENTRY("プロパティの説明", dispid, clsid)
  //PROP_PAGE(CLSID_StockColorPage)
END_PROP_MAP()
  
BEGIN_MSG_MAP(CMyCtl)
  CHAIN_MSG_MAP(CComControl<CMyCtl>)
  DEFAULT_REFLECTION_HANDLER()
END_MSG_MAP()
//ハンドラプロパティ：
// LRESULT MessageHandler(UINT uMsg, WPARAM wParam, LPARAM lParam, BOOL& bHandled);
// 
 コードまだ入力途中なので入力も進めていく。
```

### resource.hファイル
  
visual studioによって開発環境で生成されるヘッダーファイル。シンボル定義が含まれる。

シンボルとは、例えば定数などは、数字だと意味不明で何を意味しているか分からない。  
それを意味あるワードに定義すること(今年をThisYearに割り付ける:const unsigned int ThisYear = 2022のように)。  
  
シンボルは2つの部分で構成されるリソース識別子(ID)。シンボル名は次の例のようにシンボル値にマップされる。  
IDC_EDITNAME = 5100
  
シンボルはソースコード内およびエディターで作業している間にリソースおよびユーザーインターフェースオブジェクトを  
参照するためのわかりやすい手段を提供する。シンボルは"リソース シンボル"ダイアログボックスを使用して、  
都合の良い1箇所に表示して操作することができる。

アプリケーションのサイズが大きくなり複雑になるにつれリソースとシンボルの数も増える。  
いくつかのファイルに散在する大量のシンボルを追跡することは大変になってくる。 　　
"リソース シンボル"ダイアログボックスを使用すると、シンボルを簡単に管理することができる。
  
作成したシンボルがresource.hに保存され管理できる。
  
resource.hファイルは.rc(リソーススクリプトファイル)から参照され使われる。  

#### rcファイルとは
  
rcファイルは、現在のプロジェクト内のリソース用のスクリプトを格納するリソーススクリプトファイル。  
Microsoft Windowsプログラムで使われる"リソース"というデータを記述するための言語ファイル。  
rcファイルには数値定数、文字列定数、メニュー階層、各種アイコンデータなど記述し、それぞれにリソースIDという通し番号を割り振りふる。  
rcファイルをリソースコンパイラでコンパイルするとRESファイルというバイナリファイルができる（リソースファイル）。  

例えばメインプログラム側で文字列を表示したい場合は、文字列の内容をそのままコーディングするのではなく、  
該当文字列のリソースIDを参照するようにコーディングする。  
これをコンパイルしてobjファイルを作成しリソースファイルとリンクしてexeファイルを作成するとexeファイルにはobjファイルの中身  
（プログラム実行部分)とRESファイルの中身（すなわちリソース）が含まれる事になる。

こうして作ったソフトウェアを他国語に移植する時は他国語版のrcファイルだけを作ってコンパイルしRESファイルをobjファイルとリンクし、  
新しいexeファイルを作る。そうすることで、メインプログラムに手を加える必要がなくなるので、保守しやすい。
  
### ATLコントロールコンポーネントで使われる属性

ウィザードでATLコントロールオブジェクトを挿入したことによって自動的にMyCtl.hに新しく属性が追加される(IDLのカッコの中身が属性)。  
これらの属性はコントロールオブジェクトと既定のコントロールインターフェースを実装している。  
属性をシンプルな形で書き、この属性セットによってコントロールのフレームワークが裏で実装されるようになっている。

```
[
  coclass,
  control,
  default(IMyCtl),
  threading(apartment),
  vi_progid("MyAxCtrl.MyCtl"),
  progid("MyAxCtrl.MyCtl.1"),
  version(1.0),
  uuid("804A28DB-6768-42B0-AD2A-0C326CB489F7"),
  helpstring("MyCtl Class"),
  support_error_info(IMyCtl),
  registration_script("control.rgs")
]
```

#### ATLコントロールオブジェクトの挿入で追加された属性
  
coclass: オブジェクトがCOMオブジェクトであることを指定し、クラスファクトリ、自動登録、IUnKnownインターフェースの実装を自動的に提供する。

クラスファクトリとは、COMオブジェクトを生成するためのクラス。  
COMオブジェクトを生成するときは、CoCreateInstanceというCOMが提供するAPIを利用する。C++のオブジェクトをnewで生成するのとは違って、  
CoCreateInstanceというAPIを途中に挟んでインスタンスを生成することで、COMのシステムがそのインスタンスを生成する場所を変えることができるという利点がある。  
CoCreateInstanceでCOMオブジェクトを生成したとき、その実体が同じプロセス内にある場合もあれば、他のプロセスにある場合もある。
  
control: control属性を使用すると、coclassやライブラリをCOMコントロールとして識別し、必要なコンポーネント等を追加してくれる。
  
