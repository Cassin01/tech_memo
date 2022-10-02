```yaml
layout: post
title: Rustのイディオム
date: 2022-10-03
categories: [programming]
tags: [rust]
```

# 型変換
`&str` &rarr; `&[u8]`

```rust
let r: &[u8] = l.as_bytes();
```

# 結合

`&str` + `&str`

```rust
l.to_owned() + r
```

# マクロ

## インクリメント

```rust
macro_rules! post_inc {
    ($i:ident) => { // the macro is callable with any identifier (eg. a variable)
        { // the macro evaluates to a block expression
            let old = $i; // save the old value
            $i += 1; // increment the argument
            old // the value of the block is `old`
        }
    };
}
```

## ライフタイムを与える


```rust
macro_rules! give_life {
    ($i:ident) => {
        {
            let old = $i;
            old
        }
    };
}
```
