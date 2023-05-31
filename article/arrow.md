```yaml
layout: post
title: hoge
date: 2022-10-15
categories: [programming,]
tags: [plogramming]
```

# Rustでアローマクロを書いてみました

[アローマクロとは](https://clojure.org/guides/threading_macros)

`->`
```rust
macro_rules! rarr {
    ($ret:ident ( $n:ident $(,$e:ident)* ) $( ($n_n:ident $(,$e_n:ident)*) )* ) => {
        {
            let out = $n($ret $(, $e )* );
            rarr![out  $( ($n_n $(,$e_n)*) )*]
        }
    };
    ($ret:ident) => {
        $ret
    };
}
```

`->>`
```rust
macro_rules! rrarr {
    ($ret:ident ( $n:ident $(,$e:ident)* ) $( ($n_n:ident $(,$e_n:ident)*) )* ) => {
        {
            let out = $n($( $e, )* $ret);
            rarr![out  $( ($n_n $(,$e_n)*) )*]
        }
    };
    ($ret:ident) => {
        $ret
    };
}
```

Example

```rust
fn add(a: f64, b:f64) -> f64 {
  a / b
}

fn main() {
  let k = 2.;
  let t = 100.;
  let c = rarr![t (add, k) (add, k) (add, k)];
  println!("{}", c); // 12.5
  let c = rrarr![t (add, k) (add, k) (add, k)];
  println!("{}", c); // 0.005
}
```

`some->>`

```rust
macro_rules! some_rarr {
    ($ret:ident, $n:ident $(,$e:ident)* ) => {
        {
            if let Some(out) = $ret.$n {
                some_rarr![out $(,$e)*]
            } else {
                None
            }
        }
    };
    ($ret:ident) => {
        Some($ret)
    };
}
```

Example

```rust
struct C {
    a: Option::<f64>,
}
struct B {a: Option::<C>}
struct A {a: Option::<B>}

fn main() {
  let r = A{a: Some(B{a: Some(C{a: Some(5.)})})};
  let v = some_rarr![r, a, a, a];
  println!("{:?}", v);
}

```
