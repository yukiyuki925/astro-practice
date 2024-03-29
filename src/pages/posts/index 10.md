﻿---
title: スッキリわかる SQL 入門を読んで
layout: ../../layouts/Layout.astro
---

# スッキリわかる SQL 入門を読んで

## **はじめに**

すっきりわかる[SQL](https://d.hatena.ne.jp/keyword/SQL)入門を読了したので感想を記載します！

## **良かったところ**

・文章の表現が平易で、難しい書き方がされていないのでとても読みやすかったのと、図やイラストも多く処理の流れをイメージしやすかったです。
・専用サイトにおいてデータベースが用意されていて、手を動かしながら勉強できるのはとても良かったです。初学者にとって環境構築はハードルが高いので、すぐに使えるデータベースとその実行環境が用意されているのは本書における大きな特徴だと思いました。
・[SQL](https://d.hatena.ne.jp/keyword/SQL)の構文だけでなく後半ではデータベース構築にも言及しているので、[SQL](https://d.hatena.ne.jp/keyword/SQL)とデータベースについて網羅的に勉強できるのが良かったです。

## **学んだこと**

**主キーについて**
主キーとなる列が持つべき特性
・必ず何らかのデータが格納される（NULL ではない）。
・ほかの行と値が重複しない。
・一度決めた値は変化しない。

**自然キーと人工キー**
・自然に登場し、主キーの役割を果たすことができるキーを自然キーと呼ぶ（社員番号など）。

・管理目的のためだけに人為的に追加された列を人工キーや代替キーと呼ぶ（入出金 ID など）。

**テーブルの結合について**
・結合に関する２つのテーブルは対等な関係ではなく、あくまでも FROM 句で指定してたテーブルが主役。

・結合とはテーブルを丸ごとつなぐのではなく、結合条件が満たされた行の一つひとつをつなぐ。

・結合相手ない場合や列に NULL がある場合は結合結果が消滅する。 LEFT JOIN を使うことにより左表に結合相手が見つからなくても強制的に結合を行う。

**データベースが持つべき４つの特性**
・原子性　処理が実行されたか、一つも実行されていないかの状態になることが[DBMS](https://d.hatena.ne.jp/keyword/DBMS)によって保証されている。
・一貫性　[トランザクション](https://d.hatena.ne.jp/keyword/%A5%C8%A5%E9%A5%F3%A5%B6%A5%AF%A5%B7%A5%E7%A5%F3)が開始前と終了後でデータの内容は矛盾した状態にならず一貫性を保持している。
・分離性　[SQL](https://d.hatena.ne.jp/keyword/SQL)実行中に他の[SQL](https://d.hatena.ne.jp/keyword/SQL)文から影響を受けないように分離して実行される。
・永続性　変更がデータベースに永続的に保存される。システム障害などが起きても情報は保持される。

## **難しかったところ**

・巻末の演習問題の問題文を[SQL](https://d.hatena.ne.jp/keyword/SQL)の構文に置き換えるのが難しかったです。特に副問合せや結合は[SQL](https://d.hatena.ne.jp/keyword/SQL)の文が長くなるのでエラーが多くなりがちでした。
・データやテーブルが日本語名だったので日本語と英語の切り替えが少し面倒でした。日本語の状態でのスペースはエラーになるので気を付けて書いた文を見るようになりました。

## **おわりに**

手を動かしながら学べるので[SQL](https://d.hatena.ne.jp/keyword/SQL)初学者にはおすすめの参考書だと思いました。巻末のドリルもボリュームがあるので[SQL](https://d.hatena.ne.jp/keyword/SQL)の基礎はしっかり作れると思います。
