```yaml
title: subprocess
date: 2023-05-01
categories: [programming]
tags: [shell]
```

# comand > dev/null 2>&1の意味

- 0: 標準入力
- 1: 標準出力
- 2: 標準エラー出力

## 出力結果を捨てる

```
command > /dev/null
```

## 結果をマージする

標準出力を標準エラー出力にマージする

```
1>&2
```

標準エラー出力を標準出力にマージする

```
1>&2
```


`comand > dev/null 2>&1`の意味

*標準エラー出力の結果を標準出力にマージして、/dev/nullにすてる*
