---
title: 既存のプロジェクトを Docker 化する手順について
layout: ../../layouts/Layout.astro
---

# 既存のプロジェクトを Docker 化する手順について

## **はじめに**

今回は[Rails](https://d.hatena.ne.jp/keyword/Rails)のプロジェクトを Docker 化を紹介します。よろしくお願いします。

## **Docker 化することの意味**

Docker 化することで開発環境を共有でき、さらに Dockerfile を共有することで複数人で共通の環境を構築できます。OS ごとに挙動が変わることがなく、また、コンテナという仮想環境で作業するので自分の PC にあれこれインストールしなくて済みます。

## **Docker 化の手順**

1\. [github](https://d.hatena.ne.jp/keyword/github)から Web アプリの[ソースコード](https://d.hatena.ne.jp/keyword/%A5%BD%A1%BC%A5%B9%A5%B3%A1%BC%A5%C9)を引っ張ってきます。（今回は[Rails](https://d.hatena.ne.jp/keyword/Rails)アプリ）
2\. Dockerfile、docker-compose.yml というものを作ります。
3\. database.yml というファイルを編集します。
4\. Docker のイメージ・コンテナ・データベースを作成し、プロジェクト起動

## **1. [github](https://d.hatena.ne.jp/keyword/github)から Web アプリの[ソースコード](https://d.hatena.ne.jp/keyword/%A5%BD%A1%BC%A5%B9%A5%B3%A1%BC%A5%C9)を引っ張ってくる**

git clone というコマンドで[github](https://d.hatena.ne.jp/keyword/github)に上がっているプロジェクトの[ソースコード](https://d.hatena.ne.jp/keyword/%A5%BD%A1%BC%A5%B9%A5%B3%A1%BC%A5%C9)をローカル環境（自分のパソコン）に持ってきます。

git clone （リポジトリの SSH key）

[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)の[SSH](https://d.hatena.ne.jp/keyword/SSH) key は（git@[github](https://d.hatena.ne.jp/keyword/github).com）から始まるやつです。

## **2. Dockerfile、docker-compose.yml を作成**

Docker コンテナという仮想環境を作りたいのですが、その前に準備が必要です。

Dockerfile 作成

↓

Dockerimage 作成

↓

Docker コンテナ 作成

コンテナ作成は上記の流れになります。
今回のアプリは[Rails](https://d.hatena.ne.jp/keyword/Rails) + [postgresql](https://d.hatena.ne.jp/keyword/postgresql)（データベース）を使用します。[Rails](https://d.hatena.ne.jp/keyword/Rails)で一つのコンテナ、[postgresql](https://d.hatena.ne.jp/keyword/postgresql)で一つのコンテナ、計２つのコンテナを使用するので、複数のコンテナを定義・実行・管理できる Docker compose というものを使います。

**Dockerfile を作成**
Dockerfile は Dockerimage の設計図のようなものです。パッケージのインストールや作業[ディレクト](https://d.hatena.ne.jp/keyword/%A5%C7%A5%A3%A5%EC%A5%AF%A5%C8)リなど様々な設定を行います。touch コマンドで Dockerfile を作成し以下のように記述します。

## ruby のバージョン指定

```
FROM ruby:3.2.2

# パッケージをインストール

  RUN apt-get update && apt-get install -y \
  build-essential \

  libpq-dev \

  nodejs\

  postgresql-client \

  yarn

# 作業ディレクトリを rails-docke に指定

  WORKDIR /rails-docker

# Gemfile Gemfile.lock を rails-docker に追加

  COPY Gemfile Gemfile.lock /rails-docker/

# bundle install を実行

  RUN bundle install
```

### **docker-compose.yml を作成**

docker-compose.yml とは、Docker Compose を使うための設定を定義するファイルです。docker-compose.yml でそれぞれのコンテナについて条件を定義します。touch コマンドで docker-compose.yml を作成し以下のように記述します。

### コンテナのバージョンを指定

```
  version: "3"
```

### データを保存する場所を設定

```
volumes:
  db-data:
```

### 各コンテナの設定

```
  services:
```

### web コンテナの設定

```
  web:
```

### 現在のディレクトリで Dockerfile のイメージをビルド

```
  build: .
```

### コンテナ起動時にコマンドを実行

```
  command: bundle exec rails s -p 3000 -b '0.0.0.0'
```

### ポート番号を 3000 に設定

```
ports:
  - "3000:3000"
```

### ローカル側とコンテナ側で同期したいディレクトリを設定

```
volumes:
  - .:/rails-docker
```

### db コンテナから起動するように設定

```
depends_on:
  - db
```

### 環境変数を設定

```
environment:
  - "DATABASE_PASSWORD=postgres"
```

### db コンテナの設定

```
  db:
```

### postgresql のバージョンを設定

```
  image: postgres:12
```

### 環境変数を設定

```
environment:

  - POSTGRES_USER=postgres

  - POSTGRES_PASSWORD=postgres

  - POSTGRES_HOST_AUTH_METHOD=trust

```

### ホストの db データをコンテナに共有

```

volumes:

  - db-data:/var/lib/postgresql/data
```

### **3. database.yml ファイルの編集**

database.yml は[Rails](https://d.hatena.ne.jp/keyword/Rails)がデータベースに接続する時に必要になる情報を保管しています。host、username、password を設定します。

```
default: &default

  adapter: postgresql

  encoding: unicode

  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

  host: db

  username: postgres

  password: postgres

development:

  <<: \*default

  database: myapp_development

test:

  <<: \*default

  database: myapp_test

production:

  <<: \*default

  database: myapp_production

  username: myapp

  password: <%= ENV["MYAPP\_DATABASE\_PASSWORD"] %>
```

ファイルに以下の記述を追加しました。

```
  host: db

  username: postgres

  password: postgres
```

## **4. Docker のイメージ・コンテナ・データベース作成しプロジェクト起動**

下記コマンドでイメージを作成します。

```
docker-compose build
```

下記コマンドでコンテナを作成します。

```
  docker-compose up -d
```

そして、コンテナの中に下記コマンドで入ります

```
  docker-compose exec web bash
```

コンテナの中に入ったら下記コマンドで[Rails](https://d.hatena.ne.jp/keyword/Rails)のデータベースを作成します。

```
  rails db:create

  ↓

  rails db:migrate
```

この後 exit でコンテナを抜け、

```
  docker-compose up
```

をコマンドで実行し、ブラウザのアドレスバーに<http://localhost:3000>と入力します。プロジェクトの画面が出力されていれば成功です。
プロジェクトは ctrl + C で終了できます。

## **おわりに**

今回はプロジェクトを Docker 化する方法を紹介しました。私も含め初学者にとっては難しい内容ではありますが、使いこなせば大きな恩恵を受けられるので、これからも Docker の学習を継続したいと思います。
