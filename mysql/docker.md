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
# mysql

## データベースの一覧

```mysql
show databases;
```

## データベースの作成

```mysql
create database [データベース名];
```

## データベースの選択

```mysql
use [データベース名];
```

## テーブルの一覧

```mysql
show tables;
```

## テーブルの作成

```mysql
create table [テーブル名] (id INT AUTO_INCREMENT, name TEXT,mail TEXT ,pass TEXT, PRIMARY KEY (id));
```

## テーブルのcolumn一覧

```mysql
describe [テーブル名]
```

## テーブルへの基本操作

`select` `delete` `inisert` 

# データベースへのアクセス

[How to insert data into a MySQL database with Golang?](https://www.practical-go-lessons.com/post/how-to-insert-data-into-a-mysql-database-with-golang-ccbmu7s6qcuc70nnaia0)
## Rust sqlx

```rust
use sqlx::mysql::MySqlPoolOptions;


#[async_std::main]
async fn main() -> Result<(), sqlx::Error> {
    let pool = MySqlPoolOptions::new()
        .max_connections(5)
        .connect("mysql://root:mysql@127.0.0.1/my_info").await?;

    let row: (i64, ) = sqlx::query_as("SELECT id from passwords")
        .bind(150_i64)
        .fetch_one(&pool).await?;
    println!("{:?}",row.0);
    // assert_eq!(raw.0, 150);
    Ok(())
}
```
```sh
❯ sudo cargo run
Error: Database(MySqlDatabaseError { code: Some("28000"), number: 1045, message: "
 password: YES)" })

```

[MySQL ERROR 1045 (28000): Access denied for user 'bill'@'localhost' (using password: YES)](https://stackoverflow.com/questions/10299148/mysql-error-1045-28000-access-denied-for-user-billlocalhost-using-passw)
# ユーザの管理

## ユーザの作成

host`%`は外部から接続できる。

```mysql
 grant all privileges on your_schema.* to 'hie'@'%' identified by 'password' with grant option;
```

## ユーザの削除
```mysql
drop user 'user'@'localhost';
```

# localhostとは

[Code for Dajango](https://codor.co.jp/django/localhost)

localhostとは自分のパソコンのこと

