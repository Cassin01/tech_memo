```yaml
title: 謎ブラウザ
date: 2022-10-24
categories: [app]
tags: [browser, app, linux]
```

参照: DistroTube

# Light Minimal browsers

## surf
- minimal but not light(slow)

## Qutebrowser
- Keyboard driven
- `Ctrl-g`: Open the history
- faster than surf
- The Web-kit-engine

## vimb
- Alt-Ctrl
- The Web-kit-engine
- There is the configuration file at `.config/vimb`

`gtk/gtk.h`が見つからないと言われビルドできなかった.(OS X)

## Min browser

- Min is not as minimal as others, but this is still minimal.
- Min is using older version of Cromium engine.
- Min's speed is good.

## Badwolf
参照: [badwolf is A Minimal, Privacy-Oriented Web Browser](https://youtu.be/EBWy1d-JE6A)

## Midori browser

- WebKitGTK
- Mac, Windowsで使える.

- [https://hacktivis.me/projects/badwolf](https://hacktivis.me/projects/badwolf)
- WebKit2GTK

## 自分で調べたやつ

## Pale Moon

[for Mac OSX](https://forum.palemoon.org/viewforum.php?f=41&sid=499e432e17c668f78621b91ec4bc80b2)

# 使ってみた感想

## qutebrowser

- vimぽいキーバインドではあるけれど、完全にそれではないのでなれるのに大変そう
- windowのフォーカスが他のアプリにある場合に、上のバーを押さないとフォーカスがされない.
- 2回目の起動時に23:38:30 `ERROR: Error while loading config.py`とエラーを吐いて起動しなかった.(OS X)
- githubのクローンのコピーボタンを押しても上手くコピーされなかった.
- コマンドが`:`で検索できるのでわざわざtutorialのサイトを読み込む必要がなかった

## Midori browser

- ビルトインアドブロッカーの性能よいとかんじた.
- このなかで一番安定していると感じた.
- 設定がちょうどよいくらいシンプルですぐに使える.
- 普通にはやい
- ダークモードが反映されなかった
- ダウンロード画面が謎言語
