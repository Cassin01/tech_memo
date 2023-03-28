```yaml
title:wifi
date: 2023-03-28
categories: [network]
tags: [光回線, network]
```

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
- 最大勢力
- So-netが使用
    * v6プラス
- 対応ルータおおい
- ポート開放限定的に可能

### DS-Lite

- ぷららが使用
    * v6オプション
- 対応ルータおおい
- ポート開放できない


### IPIPトンネル

- ソフトバンク光が使用
- 対応ルータほぼなし
- ポート開放可能
