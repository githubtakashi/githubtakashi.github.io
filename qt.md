# Qtを使うためのメモ

NEC express5800 ubuntu22.04でQtを使ってアプリ作成を進めるためのメモを作成していく。


## HelloWorldをQtWidgetで作成

Cmakeだとビルド以前のエラーが発生しうまくいかないのでqmakeに変更しビルドすると、下記のエラーメッセージが出た。

```
Qt 6: cannot find -lGL
```

-lに続く文字列がパッケージを意味していて、GLパッケージが無いよと言っている。  
下記のようにubuntuにパッケージをインストールするとビルドできるようになる。

```
sudo apt-get install mesa-common-dev libgl1-mesa-dev libglu1-mesa-dev
```



