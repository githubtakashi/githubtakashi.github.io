# android studioでandroidアプリを作成するためのメモ

android studioというIDEをdell precision m6500 ubuntuにインストールしandroidアプリを  
作成してみようと思い立った。

android studioはどのosにも対応している。windows,macOS,Linux

android studio自体はubuntuのソフトウェアでGUIでアプリ化されているのでインストールは簡単。

言語はjavaがメインで使われている。c言語に対するc++のような位置づけでkotlinという言語も使える。

javaとkotlinのどっちがいいのか調べたらjavaのほうがまだ良さげな気がしたのでjavaでとりあえず  
勉強を開始してみることにした。

## システム要件が重要

新しめのpcでメモリを多めに積んでないとシミュレータが固まってまともに動かない。  
とくに重要なのがcpu。第二世代以上のcpuが要件となっているけど、第二世代付近だと重い。

<br />

## android studioでhello world

[helloworldするチュートリアル](https://developer.android.com/training/basics/firstapp/creating-project?hl=ja)通り進める。

<br />

### マニフェストとは  

マニフェストという言葉自体の意味は、個人や団体が方針や意図を、広く多数のひとに向かって知らせるための文書や演説のこと。  
AndroidManifest.xmlはアプリ作成で必要なファイルで、アプリケーションについての情報が記載されている。  
マニフェストに記載された情報はAndroidシステムに提供される。なので、システムに知らせるための文書。

### エントリーポイントとは:

すぐ忘れるので再度メモ。エントリーポイントとは、プログラムを実行するとき、プログラムやサブルーチンの実行を開始する場所のこと。  
AndroidManifest.xml中のxx.category.LAUNCHER"の部分がエントリーポイント。

```
<category android:name="android.intent.category.LAUNCHER">
```

グーグダウンロードしたアプリを使い始めるときにアイコンをタップする。  
タップが引き金になり、上記タグ内のプログラムが呼ばれてアプリが動き出す。  

app > java > com.example.myfirstapp > MainActivity.javaがエントリポイント。

アプリをビルドして実行するとこのActivity(class)のインスタンスが起動してレイアウトが読み込まれる。

### Gradleとは

オープンソースビルド自動化システムのこと。

### 主要なファイル

app > res > layout > activity_main.xml　　
アクティビティのUIのレイアウトを定義しているXMLファイル。  
デフォルトでHello, World!というテキストを表示するTextView要素が含まれている。

app > manifests > AndroidManifest.xml　　
マニフェストファイルには、アプリの基本的な特徴やアプリの各コンポーネントが定義されている。

Gradle Scripts > build.gradle  
この名前を持つファイルは2 種類ある。1 つはプロジェクト用(Project: My_First_App)で、  
もう1 つはアプリモジュール用（Module: My_First_App.app）。  
モジュールごとにそれぞれ個別のbuild.gradleファイルが用意される。  
現在のところ、このプロジェクトに含まれるモジュールは1つだけで、各モジュールのbuild.gradleファイルを使用して、  
Gradleプラグインでアプリを作成する方法を制御する。

