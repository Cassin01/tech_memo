```yaml
layout: post
title: CpawCTF
date: 2022-10-23
categories: [programming]
tags: [rust]
```

# q6

```rs
fn main() {
    let cs =  "fsdz{Fdhvdu_flskhu_lv_fodvvlfdo_flskhu}";
    for c in cs.chars() {
        print!("{}", (c as u8 - 3) as char);
    }
}
```

# q7

```sh
❯ file exec_me
exec_me: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interprete
r /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.24, BuildID[sha1]=663a3e0e5a079fddd0de92474
688cd6812d3b550, not stripped
```

ELF: Executable and Linking Format
    Red Hatを始めとするLinuxディストリビューションの多くでは標準バイナリ形式として採用されている

```sh
docker start ubuntu_1
docker cp ./exec_me ubuntu_1:/root
docker exec -it ubuntu_1 bash -p
cd /root
chmod u+x ./exec_me
./exec_me
```

# q8

finderでクリックしたらwordが開く

# q9

webインスペクタを起動, `{`を検索

# q10

Exif情報  
mac のプレビューでℹ️ マークをクリック

# q15
webインスペクタを開く
ログを保持をチェック.
レスポンスヘッダーのX-Flagにある.

# q16
1. @wireshark
    - file>export opject>http
2. http拡張子を追加してブラウザでひらく

# q18

`%/s/lovelive!//g`

# q19

```sh
$ file misc100.zip
misc100.zip: OpenDocument Drawing
```

```sh
libreoffice ./misc100.zip
```

# q25

```sh
$ ./a.out ruoYced_ehpigniriks_i_llrg_stae 4
```

# q26

```sh
brew install --cask idafree
```

# q27

```mysql
select * from palloc_home;
```

# q28 can u login

```sh
brew install tnftp
```
