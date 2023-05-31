# tmux

# tmux コマンド
## reload

```sh
❯ tmux source ~/.tmux.conf
```

## セッション一覧

```sh
tmux ls
```

## Discard all sessions

```sh
tmux kill-server
```


# キーバインド
## セッション(tab)

- c: new セッション
- w: セッションの一覧
- n: 次のセッション
- p: 前のセッション

## ペイン(window)
- x: ペインの破棄
- |: 縦分割
- -: 横分割
- h: 左のペインへ
- j: 下のペインへ
- k: 上のペインへ
- l: 右のペインへ
- H: ペインへ
- J: ペインへ
- K: ペインへ
- L: ペインへ
- スペース: ペインのレイアウト変更
- Ctrl+o: ペインの入れ替え
- {: ペインの入れ替え(上方向)
- }: ペインの入れ替え(下方向)
- [: コピーモードの開始(カーソルキーで移動)
- v: コピー開始位置決定(viモード)
- y: コピー終了位置決定(viモード)
- Crtl+p: コピー内容の貼り付け


[参考](https://qiita.com/shin-ch13/items/9d207a70ccc8467f7bab)
