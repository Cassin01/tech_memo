# DockerでMySQRを使う
Ref [Qiita](https://qiita.com/TAMIYAN/items/ed9ec892d91e5af962c6)

## Docker Composeを使わない場合

```sh
 Docker-hubからMySQLのイメージをインストールする
$ docker pull mysql

# インストールしたイメージから、コンテナを起動･作成する
# MYSQL_ROOT_PASSWORDにログインする際のパスワードを設定する
$ docker run -it --name my-mysql -e MYSQL_ROOT_PASSWORD=mysql -d mysql:latest

$ docker exec -it test-wolrd-mysql bash -p

# MySQLのコンテナにログインする
$ mysql -u root -p -h 127.0.0.1

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.16 MySQL Community Server - GPL

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

## Docker Compose使用

docker-compose.ymlがあるフォルダに移動後, 以下コマンドを実行

```sh
# イメージのビルド
$ Docker-Compose build

# コンテナの作成
$ Docker-Compose up -d

# 起動したコンテナにログイン
$ docker exec -it Docker-mysql_mysql_1 bash -p

# MySQLを起動
$ mysql -u root -p -h 127.0.0.1

# この後パスワードを入力して完了
```
## mysql

### データベースの一覧

```mysql
show databases;
```

### データベースの作成

```mysql
create database [データベース名 (my_info)];
```

### データベースの選択

```mysql
use [データベース名 (my_info)];
```

### テーブルの一覧

```mysql
show tables;
```

### テーブルの作成

```mysql
create table [テーブル名 (passwords)];
```

### テーブルへの基本操作

`select` `delete` `inisert`
