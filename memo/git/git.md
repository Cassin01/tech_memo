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

### ブランチ削除

```sh
$ git branch -d [Branch name]
$ git branch -D [Branch name] # with force
```

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

## Add a description to a branch

```
git branch --edit-description
```

## Git branch command behaves like 'less'

```
git --no-pager branch
```

## Add a comment to a branch

```
git branch --edit-description
```

# Branch naming conventions

[stack overflow](https://stackoverflow.com/questions/273695/what-are-some-examples-of-commonly-used-practices-for-naming-git-brancheshttps://stackoverflow.com/questions/273695/what-are-some-examples-of-commonly-used-practices-for-naming-git-branches)

- 連番や長い名前を使わない

## Group tokens

```
{lead token}/{short well-defined token}
```

## Short well-defined tokens

```
wip     Works in progress; stuff I know won't be finished soon
feat    Feature I'm adding or expanding
bug     Buf fix or experiment
junk    Throwaway branbnch created to experiment
```

## Cycle token(lead token)

```
new     new
testing testing
ver     verified
```

# Show network graph

## git log

今までのコミットのログが見れる

```zsh
git log
```


### --graph

コミットツリーが表示される

```
git log --graph
```

- `--oneline`: 一行表示
- `--decorate=(short|full|no)`: ブランチ名の表示形式
- `--date=(relative|local|default|iso|rfc|shot|raw)`: 日付表示

## alias

@ `.gitconfig`

```
[alias]
  tree = log --graph -decorate --pretty=oneline --abbrev-commit
```

`$ git tree`

## tig
