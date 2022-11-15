```yaml
title: algorithm2e
date: 2022-11-12
categories: [tex]
tags: [tex]
```

# algorithm2e 備忘録

## \usepackageのオプション[$\ldots$]について

- 行番号をつける: `linesnumbered`
- `end`を消す: `noend`
- captionをつける: `ruled`
- インデント線を$\lfloor$にする: `vlined` (`\SetAlgoLined`が設定されていると反映されないので注意)

## コマンド
- 入力, 出力をInput, Outputに変更: `\SetKwInOut{Input}{Input}\SetKwInOut{Output}{Output}`
- 行末のセミコロン表示しない: `\DontPrintSemicolon`
- インデント線をつける: `\SetAlgoLined`

- endをつけない`\If`: `\uIf`
