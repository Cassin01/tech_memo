# C言語コンパイル
## 実行ファイルに名前を付ける

```c
$ gcc main.c -o main
```

## オブジェクトファイルを作成
オブジェクトファイル: コンパイルは下がリンクが終わっていないファイル

```c
$ gcc -c hello.c
```
## 複数のオブジェクトファイルから実行ファイルを作成

### `a.c b.c c.c`から実行ファイル`main`の作成

```c
$ gcc a.c b.c c.c -o main
```

### オブジェクトファイルを利用

```c
$ gcc a.c b.o c.o -o main
```

## -Wall, -W
ワーニング有効
