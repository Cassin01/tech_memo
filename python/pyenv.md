# pyenv
## インストール
```
$ brew install pyenv
```

```
$ brew info pyenv
```

で表示されたものを`.zprofile`と`.zshrc`へ


## バージョン切り替え
```
$ pyenv global systtem
$ pyenv versions
* system
  3.10.1 (set by /Users/cassin/.pyenv/version)
```
```
$ pyenv global 3.10.1
$ pyenv versions
  system
* 3.10.1 (set by /Users/cassin/.pyenv/version)
```

## 確認
```
❯ which python
/Users/cassin/.pyenv/shims/python
```

### 注意点
``python3`` が``python``になる
``pip3`` が``pip``になる

## pip install
```
❯ sudo sudo /Users/cassin/.pyenv/shims/python3 -m  pip install pynvim
```


## pipのバックアップ

```
$ pip freeze > requirement.txt
```

## pipの回復
```
$ pip install -r requirement.txt
```

