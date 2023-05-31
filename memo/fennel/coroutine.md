# コルーチン

- sub-routinne
    - call してからreturnするまで処理を中断できない

- co-routine
    - 途中で処理を中断し、そこから実行を再開することができる。

## 関数

- create: コルーチンの生成
- resume: コルーチンの再開
- yield: 実行するとそこでプログラムの実行を中断して親コルーチンに戻る。


## イテレータ

```lisp
(fn make-array-iter [lst]
return coroutine.create(
    (fn ()
        (each _ v [ipair lst]
            coroutine.yield(v))
    false)))
```

- wrap: create, resume のシンタックス
