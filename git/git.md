```yaml
title: gitについて
date: 2022-10-14
categories: [programming]
tags: [git]
```
# upstream

## ossにpull request

[oss](https://qiita.com/y-vectorfield/items/b955617712f3b66359f2#fn5)

## 上流ブランチの確認

`$ git banch -vv`

## ブランチ作成からcommitまでの流れ

### ブランチ作成

```sh
$ git branch [Branch name]
* main
  [Branch name]
$ git branch # 作成確認
$ git checktout [Branch name] # ブランチ切り替え
$ git branch # 切替確認
  main
* practice
```

- If you want to make new local branch and move there at once: `git checkout -b [Branch name]`

### コミット

```sh
git add some
git commit -m "some"
```

### push

```sh
# upstream branch がない場合
git push --set-upstream origin [Branch name]
# -u is syntax sugar for --set-upstream

# upstream branchがすでに存在している場合
git push origin [Branch name]
```


# [Conventional Commits](https://www.conventionalcommits.org/)

# trics

## Add and commit at same time

```sh
git commit -am "chore: add new feature"
```

## Add alias

```sh
git config --global alias.ac "commit -am"
git ac "noice"
```

## git log more readable

```sh
git log --graph --oneline --decorete
```
