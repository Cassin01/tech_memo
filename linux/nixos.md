```yaml
title: nixis
date: 2022-10-25
categories: [linux]
tags: [nixos, nix]
```

## ストレージがなくなる問題

ストレージ`32GB`でやっていた。
xmonadというWMをインストール
`nixos-rebuild switch`をやった際にストレージがないと言われる。
rebootしたところ起動しなくなった.

## 解決方法?

[How much storage does NixOs need?](https://discourse.nixos.org/t/how-much-storage-does-nixos-need/8805/3)
にあった内容を書き出す

### 方法?1
```bash
## hope you're using bash
##
zGenerationsInDaysToBeDeleted=22 ## my individual preference of having the 22 days available; adjust to your personal needs
#
nix-collect-garbage -d --delete-older-than ${zGenerationsInDaysToBeDeleted}
```

### 方法?2
> Do you use home manager? Be sure to delete it’s generations as well. Same goes for lorri, direnv persistent shell, or anything else that creates gc roots.

home-managerにhaskellのためのこれこれを色々書いていた。これが原因かもしれない
