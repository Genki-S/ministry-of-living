---
date: '2025-01-07T00:31:45+09:00'
title: 'OpenWrtでv6プラス接続(2025年1月最新版)'
---

私は[こちらの記事(OpenWrtとフレッツ光ネクスト/クロス v6プラス(MAP-E/固定IPIP6)で繋ぐには)](https://qiita.com/kouhei-ioroi/items/cf0c6228c5c1faef415a)に従うだけでv6プラス接続ができるようになりました(2025年1月現在)。ググって出てくる記事のいくつかは情報が古いのか、私には動かずかなりハマったので書き置きです。

{{< details summary="筆者の環境" >}}
- 回線: GMO光アクセス クロスファミリー接続サービス
- OpenWrt 23.05.5, r24106-10cc5fcd00
  - on Proxmox 8.3.0
    - on [iKOOLCORE R2 Max](https://jp.ikoolcore.com/products/ikoolcore-r2-max)
{{< /details >}}

## Tips

この記事を読むといいよ、だけで終わるのもアレなので便利かも情報を書いておきます。

- [こちらの記事(OpenWRT V6プラス (MAP-E) 接続設定)](https://forum.ficusonline.com/t/topic/498)でv6プラスの仕組みの概要を説明してくれているので頭に入れておくと捗ります。(※この記事のv6プラス接続設定は私の環境では動きませんでした)
- VMでやってる場合はこまめにsnapshotをとると吉です。私は3回くらいOpenWrtのVMを作り直しました。
- OpenWrtで`opkg update && opkg install curl`をして、こまめに`curl -v -6 google.com`と`curl -v -4 google.com`でIPv6/IPv4インターネット接続を確認すると便利です。LAN内のデバイスからも同様に。
- Arch LinuxでOpenWrtからIPアドレスをもらうときは、`sudo ip link set enpXXX down && sudo ip link set enpXXX up`が安定して成功しました。`sudo systemctl restart systemd-networkd`でもできるらしいですが私には動かず...
