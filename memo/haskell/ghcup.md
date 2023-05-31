ghcupに乗り換えた際の忘録

## 環境
OS X

## 注意点

`brew`はインストールはできたがその後いろいろうまく行かなかった

```sh
brew install ghcup
```

### 以下`ghcup`インストールの前に削除するところ

`stack`と`cabal`が存在するとうまく行かない

#### cabal

`zsh`
```sh
where cabal
/Users/name/.cabal
/usr/local/bin/cabal
```

- `/Users/name/.cabal`の方を削除する

- `zshrc`のパスも削除する

`zshrc`
```zshrc
# idris
# export PATH=~/.cabal/bin:$PATH
```

#### stack

`~/.local/bin/`以下に`stack`が存在するとうまく行かないので削除する

このとき自分は一緒に存在した`hie`も削除した.


## インストール

[こちらのサイト](https://www.haskell.org/ghcup/)のスクリプトを実行してインストールする．

## lsp

`neovim/nvim-lspconfig` でインストールできることを確認した．
