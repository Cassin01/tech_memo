git push https://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@github.com/Cassin01/lab_memo.git

# GitHub CLI

### エディタの設定
`gh config set editor`

## repo - リポジトリの操作
- [gh repo](https://cli.github.com/manual/gh_repo)

### リポジトリ作成
`gh repo create mlisp --private --push --source ./`

### リポジトリ削除
`gh repo delete`

# GitHub REST API 

### リポジトリ一覧を取得

`https://api.github.com/users/ユーザー名/repos`

### あるリポジトリのイベント履歴を取得

`https://api.github.com/repos/リポジトリの所有ユーザー名/リポジトリ名/events`

### ここ1年間の，あるリポジトリのコミット回数を週ごと取得する

`https://api.github.com/repos/リポジトリの所有ユーザー名/リポジトリ名/stats/participation`

###ここ1年間の，あるリポジトリの曜日別コミット回数を周毎に取得する

`https://api.github.com/repos/リポジトリの所有ユーザー名/リポジトリ名/stats/commit_activity`

### あるユーザのGist情報一覧を取得

`https://api.github.com/users/ユーザー名/gists`

# GitHub Graph API


```sh
gh api graphql -f query='
query {
    user(login: "Cassin01") {
    login
    name
    contributionsCollection(from: "2021-01-01T00:00:00Z") {
        startedAt
        endedAt
        totalCommitContributions
        commitContributions
    }
    }
}'
```
