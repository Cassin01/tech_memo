```yaml
title: server
date: 2023-06-08
categories: [programming]
tags: [server, linux, rokcy-linux]
```

# Shell commands

## switch user

`su -l USER_NAME`

## sudoの実行権限を付与

`usermod -aG sudo USER_NAME`

## Display disc assignment with Gigabyte

`df -h`

# firewalld

## 起動

`sudo systemctl start firewalld`

## 確認

`sudo systemctl status firewalld`

## 自動起動有効化

`sudo systemctl enable --now firewalld`

## 自動起動確認

`sudo systemctl is-enabled firewalld`

## 設定の確認

`sudo firewall-cmd --list-all`

## ポートを加える

```sh
sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
sudo firewall-cmd --permanent --zone=public --add-port=443/tcp
sudo firewall-cmd --permanent --zone=public --add-port=22/tcp

# reload firewall after making changes
sudo firewall-cmd --reload
```

## VPNのコントロールパネルでもポートを加える

IPアドレス`0.0.0.0`はどこからでも受け付けるの意

*問題*: dnfが使えなくなる

# ssh

## 作成したユーザに鍵を付与

Reference: https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04

# dnf

## 期限切れのパッケージを削除する

`dnf autoremove`
