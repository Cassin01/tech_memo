```yaml
layout: post
title: mysql
date: 2020-04-02 00:00:00 +0900
categories: [database]
tags: [mysql]
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

