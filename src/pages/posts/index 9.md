---
title: optparse でオプションを指定する
layout: ../../layouts/Layout.astro
---

# optparse でオプションを指定する

## **はじめに**

[Ruby](https://d.hatena.ne.jp/keyword/Ruby)のライブラリである optparse について簡単に解説します。

## **optparse ってなに？**

[_docs.ruby-lang.org_](https://docs.ruby-lang.org/ja/latest/library/optparse.html)

[コマンドライン](https://d.hatena.ne.jp/keyword/%A5%B3%A5%DE%A5%F3%A5%C9%A5%E9%A5%A4%A5%F3)にオプションを指定できるようになります。[コマンドライン](https://d.hatena.ne.jp/keyword/%A5%B3%A5%DE%A5%F3%A5%C9%A5%E9%A5%A4%A5%F3)に、-m や-a などオプションを指定することにより、出力結果を変化させることができます。

## **実際の挙動**

require 'optparse'

opt = OptionParser.new

opt.on('-a') {|v| p v }

opt.on('-b') {|v| p v }

opt.parse!(ARGV)

p ARGV

↓

ruby sample.rb -a foo bar -b baz

\# => true

`     `true

`     `["foo", "bar", "baz"]

on の部分にオプションを定義しています。上のコードだと、-a、-b を定義しています。ARGV にはコマンドに入力したオプションと引数が配列の形で渡されます。その後の parse で引数だけを取り出し、配列として出力しています。

optparse を使った具体例としては、カレンダープログラムなどがあります。optparse を使うと、

ruby calendar.rb -m 5

このようにターミナルで実行時にオプションとして "-5" など任意の数字をつけることによりその数字に対応した月を表示することができます。

## **おわりに**

コードの書き方は少しクセがあると個人的には思いますが、optparse をさらに応用すると[スクレイピング](https://d.hatena.ne.jp/keyword/%A5%B9%A5%AF%A5%EC%A5%A4%A5%D4%A5%F3%A5%B0)などにも組み込まれたりするみたいなのでかなり便利なライブラリだと思います。使う機会があれば積極的に使っていきたいと思います！
