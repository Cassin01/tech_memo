```yaml
title:wifi
date: 2023-03-28
categories: [network]
tags: [光回線, network]
```

# 通信速度

## 上り

端末からファイルを転送する際の通信

- git push とか

## 下り

端末でファイルを受け取る際の通信

- 動画とかダウンロードとか
こっちのほうが重要そう

# 光回線について

- [ICT Digital Column](https://www.nttpc.co.jp/column/network/pppoe_ipoe.html)
- [フレッツ網の使い方完全に理解した qiita](https://qiita.com/7GHz/items/2eeb5d5644fc9df6bc10)


## フレッツ網とは
NTTの高速なLANネットワーク


## PPPoE, IPoE

oE: 「over Ethernet」の略,
LANの規格であるイーサネット(Ethernet)を使用して通信を行うという意味。

### PPPoE

電話網でプロバイダとの通信に使われたPPP(Point to Point Protocol)をイーサネットにさせたもの。
電話回線網とインターネットサービス・プロバイダを接続する「ネットワーク終端装置」を必ず通過する。

- IPv4のみ
- 通信速度: 1Gbps
- 時間により混雑の影響あり

### IPoE

- IPv6のみ
- 津神速度10Gbps
- 輻輳しづらく安定する

## IPoEの規格

### MAP-E
- MapはMapping of Address and Portの, EはEncapsulation(カプセル化)の略
- 最大勢力
- So-netが使用
    * v6プラス (最大勢力)
    * OCNバーチャルコネクト (第2勢力)
- 対応ルータおおい
- ポート開放限定的に可能

### DS-Lite

- ぷららが使用
    * v6オプション (ビックローブのみ採用)
    * transix
- 対応ルータおおい(下火)
- ポート開放できない


### IPIPトンネル

- ソフトバンク光が使用
- 対応ルータほぼなし
- ポート開放可能

# プロバイダ (2023-03-28)

チェックリスト

- [ ] NTTのフレッツ光回線
- [ ] IPoE
- [ ] v6プラス
- [ ] マンションタイプ
- [ ] 1Gbps?(実家は1Gbps) &rarr; 100Mbpsで十分そう?前のアパートは下り200mps上り100mpsで共有だった.

以下 マンションタイプ, IPoE, NTTフレッツ光回線


## So-net

- 初期工事費: 26,400円
- 事務手数料: 3500円
- 月額料金: 3,400円/月
- 一年間1,000円/月割引
- v6プラス無料

### プラス    5 万円のキャッシュバック
工事費26800 途中解約しなければキャッシュバック
土日3500


## おてがる光

- IPv6オプション
- 月額料金: 4,400円/月
- 事務手数料: 3300円
- 解約金: 4,180円
- v6プラス無料
- wifiルータ無料

So-net minicoにしました。
