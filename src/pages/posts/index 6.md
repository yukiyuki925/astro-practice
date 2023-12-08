﻿---
title: Linuxコマンドについて
---

## Linuxコマンドについて

##### **はじめに**
今回はLinuxのコマンドについて簡単に説明したいと思います。この記事でLinuxコマンドを簡単に理解し、実際に使ってみましょう！ 
##### **ターミナル**
windowsだったらスタートメニュー、macだったらLaunchpadを開き、ターミナルと検索します。開くと黒い画面が出てきます。（もしかしたら白い画面の方もいるかも）基本的にはこの画面にコマンドを入力していきます。コマンドを入力することで、PCの中のファイルやディレクトリを操作していきます。 
##### **ファイルとディレクトリ**
コマンドを説明するにあたり、ファイルとディレクトリについて簡単に説明します。ファイルとは文書や画像などのデータのことで、ディレクトリはファイルを入れる箱のことです。PCの中には無数のファイルがあり、それが無秩序に並べられていると探すのが大変なので写真のディレクトリ、音楽のディレクトリという風にファイルをディレクトリにまとめて管理することで、PC内部の検索を効率化しています。 

基本的にPCのディレクトリの構造は階層構造をなしています。ルートディレクトリ→ホームディレクトリ→デスクトップディレクトリ→写真ディレクトリ→2023年memoryディレクトリのように、上から下へとアクセスしていきます。 


#### **基本コマンド**
##### **cd**
change directryの略称です。ディレクトリを移動します。

例えば、cd desktopとするとデスクトップディレクトリに移動します。cd /とすると一番上のディレクトリのルートディレクトリに移動します。 
##### **pwd**
print working directoryの略称です。現在のディレクトリの位置を確認できます。例えば、2023年memoryディレクトリにいたとすると、 

desktop/picture/2023memory　と表示されます。本当はもっと長く表示されますが、説明のために省略しています。 
##### **ls**
listの略称です。ディレクトリの中身を確認できます。まず中身確認してから次のコマンドを入力という流れが多いです。以下がオプションコマンドです。 

ls -l　中身の詳細情報を確認できます。ファイルかディレクトリか判別できるので便利です。 

ls -a　隠しファイルを確認できます。誤って削除したりしないように、PCの設定などの重要なファイルは隠してあります。 
##### **mkdir**
make directoryの略称です。ディレクトリを作成します。
##### **rmdir**
remove directoryの略称です。空のディレクトリを削除します。「空の」というのが肝で、削除したいディレクトリにファイルなどが入っている場合は削除ができません。 
##### **cat**
concatenateの略称です。ファイルの中身を確認できます。
##### **less**
テキストファイルの中身を閲覧できます。catコマンドはそのままターミナルに出力するので中身の文章が長い場合、今ままでの操作履歴が上に流れて若干不便です。lessは別画面で出力されるのでファイルの中身長くても閲覧しやすいです。 
##### **tail**
ファイルの末尾を確認することができます。追記されたログを確認する時に使います。 
##### **touch**
ファイルのアクセス日時や更新日時を変更します。ファイル名が存在しない場合、新しくファイルを作成します。最初の方はファイルを新しく作るコマンドという認識で大丈夫かなと思います。 
##### **rm**
removeの略称です。ファイルを削除できます。rm -rとすることでディレクトリも削除できます。ディレクトリにファイルが存在する場合、ファイルも一緒に削除するので、注意が必要です。 
##### **mv**
ファイルやディレクトリを移動する時に使います。

mv 移動元 移動先　という使い方になります。

移動元がファイル、移動先がファイルの場合は移動元のファイルの名前を変更します。 

移動元がディレクトリX、移動先がディレクトリYの場合はディレクトリXをディレクトリYに移動します。 

移動元がファイル、移動先がディレクトリの場合あファイルをディレクトリに移動します。 
##### **cp**
copyの略称です。指定したファイルをコピーすることができます。

copy -r　でディレクトリもコピーできます。ディレクトリにファイルが存在する場合、ファイルもコピーします。 

使い方は　cp コピー元 コピー先です。
##### **ls**
ファイルのリンクを作成するコマンドです。

ln -s ファイル名 リンク名　という使い方になります。いわば、ファイルに別名をつけるというコマンドです。長いファイル名に別の名前をつける時に使います。 
##### **find**
ファイルやディレクトリを検索します。

find ファイル名　のように使います。
##### **chomod**
change modeの略称です。ファイルやディレクトリの権限を変更することができます。権限は　ls -l　で確認することができます。権限はアルファベットで表現されます。 

r ファイルの読み込み　w ファイルの編集　x ファイルの実行

u ユーザー　g グループ　o その他　という意味です。

例えば　chmod u+x　とすればユーザーにファイル実行の権限が付与されます。
##### **chown**
ファイルやディレクトリの所有者を変更するコマンドです。

chown 所有者名 ファイル名またはディレクトリ名　のように使います。
##### **ps**
os内部で現在実行されているプロセスを確認するコマンドです。CPUの使用率などが確認できます。 

単に　ps　と入力するだけで大丈夫です。
##### **kill**
プロセスを終了するコマンドです。

kill プロセスID（PID）　のように使います。

上記のpsコマンドでプロセスIDを確認し使用します。

また、kill -9 プロセスID　とすることでプロセスを強制終了することができます。 
##### **おわりに**
コマンドをたくさん紹介しましたが、暗記する必要はないと思います。これらは実際に手を動かすことで覚えていくと思うので、紹介したコマンドをターミナルに入力して挙動を確認していただければと思います。 