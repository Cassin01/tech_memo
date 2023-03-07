# Haskell

# `$`

`$`から行末までを括弧で囲む

# クラスメソッド

純粋仮想関数みたいな関数の抽象的な特徴

# 型クラス

クラスメソッドをまとめたもの

# fmap

`map`は配列に対してしか関数を適用できない．

一方で，`fmap` は Maybe型やタプルにも適用できる.

```haskell
fn n = n * 2
main = do
    print $ fmap fn [1, 2, 3] -- [2, 4, 6]
    print $ fmap fn Notiong   -- Notiong
    print $ fmap fn (Just 5)  -- Just 10
    print $ fmap fn (2 ,3)    -- (4, 6)
```

`fmap fn x` は `fn <$> x`と書ける

```haskell
fn n = n * 2
main = do
    print $ fn <$> [1, 2, 3] -- [2, 4, 6]
    print $ fn <$> Notiong   -- Notiong
    print $ fn <$> (Just 5)  -- Just 10
    print $ fn <$> (2 ,3)    -- (4, 6)
```

`Functor`型クラスは，`fmap`クラスメソッドを持つ.


# `pure`メソッド, `<*>`演算子

- `pure`は関数をラッピングする.
- `<*>`はラッピングした関数を，ラッピングした値に対して適用する.

```haskell
main = do
    print $ pure (* 2) <*> Just 5    -- Just 10
    print $ pure (* 2) <*> [1, 2, 3] -- [2, 4, 6]
```


- 複数の関数を複数のリストに対して適用する事もできる

```haskell
main = do
    print $ [(* 2), (* 3)] <*> [1, 2, 3] -- [2, 4, 6, 3, 6, 9]

```

`Applicative`型クラスは`pure`メソッドと`<*>`演算子を持つ


# `return` メソッド, `>>=`演算子

- `return` は通常の値をラッピングされた値に変換する.
- `>>=` はラッピングされた値をラッピングされた値を返す関数に渡す.

```haskell
fn x = return (2 * x)

main = do
    print $ [1, 2, 3] >>= fn	-- [2, 4, 6]
    print $ Just 5 >>= fn	-- Just 10
    print $ Nothing >>= fn	-- Nothing
```


`Monad`型クラスは, `return` メソッド, `>>=`演算子を持つ．

# `<>` 演算子

## Semigroup 半群

- 結合則 `(a <> b) <> c = a <> (b <> c)`

## Monoid モノイド
+empty

- 結合則 `(a <> b) <> c = a <> (b <> c)`
- 単位元 `e <> a = a <> e = a`

## Group 群
+inverse

- 結合則 `(a <> b) <> c = a <> (b <> c)`
- 単位元 `e <> a = a <> e = a`
- 逆元   `a <> inv a = e`

## `<|>`

Alternative

## MonadPlus



# 参考

[とほほのHaskell入門](https://www.tohoho-web.com/ex/haskell.html#functor)
[あなたの知らないSemigroupの世界](https://kazu-yamamoto.hatenablog.jp/entry/20180306/1520314185)
