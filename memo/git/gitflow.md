```yaml
title: gitflow
date: 2023-03-30
categories: [programming]
tags: [git, cli]
```

# git-flow

[repository](https://github.com/nvie/gitflow)


A collection of Git extensions to provide high-level repository operations for
Vincent Kreeftmeijer's blog post


# A successful Git branching model

https://nvie.com/posts/a-successful-git-branching-model/

Vincent Kreeftmeijerが使っている開発モデルについての説明がされている.



origin/developをHEADにする("integration branch"とも呼ばれている).

origin/developの内容をmasterに反映することは新しいproduction
releaseである. したがって開発者はmasterにコミットが行われるたびに自動でビルドし, ロールアウトするGit hook scriptを使いがちである.

その他のよく使われるブランチ
- Feature branches
- Release branches
- Hotfix branches

それぞれのブランチはどのブランチをオリジナルにするかなどのルールが厳密に決まっている.

## Feature branch
featureブランチは開発者のレポジトリのみ存在する. originには存在しない.

### feature branch の作成

featureブランチはdevelopブランチから分岐される.

```sh
$ git checkout -b myfeature develop
```


### feature をdevelopにマージする

```
$ git checkout develop
Switched to branch 'develop'
$ git marege --no-ff my feature
$ git branch -d myfeature
$ git push origin develop
```

注) git merge --no-ffとは

mergeコマンドを使った際に, mergeコミットを発生させる.

設定に入れる.
`$ git config --global --add merge.ff false`

pullを行った際のmergeにも--no-ffが有効になるため,
pullを行うたびにmergeコミットが発行され, コミットログが荒れる.

pullのときに`--no-ff`オプションを使わないようにする.
`git config --global --add pull.ff only`

## release branch

```
$ git checkout -b release-1.2 develop
$ ./bump-version.sh 1.2
$ git commit -a -m "Bumped version number to 1.2"
```

注) bump up は version upとほぼ同等の意味.
注) git commit -a

```
-a
--all

変更および削除されたファイルを自動的にステージングするようにコマンドに指示しますが、Gitに通知していない新しいファイルは影響を受けません。
```

## finishing a release branch

```
$ git checkout master
$ git merge --no-ff release-1.2
$ git tag -a 1.2
```

masterへの結合を終え, developブランチにもどる.

```
$ git checkout develop
$ git merge --no-ff release-1.2
```

## Hotfix branches

master &rarr; hotfix-* &rarr; develop and master

```
$ git checkout -b hotfix-1.2.1 master

$ ./bump-version.sh 1.2.1

$ git commit -a -m "Bumped version number to 1.2.1"
```

修正内容をコミットする.
`git commit -m "Fixed severe production problem"`

hotfixを終える.

```
$ git checkout master

$ git merge --no-ff hotfix-1.2.1

$ git tag -a 1.2.1
```

