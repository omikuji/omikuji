## omikuji

東京の Web エンジニアです。企画・実装・インフラ・運用・SEO まで一人で担当し、**18 の Web サービス**を本番で動かしています。
ソースの大半は private ですが、動いているものはすべて下のリンクから触れます。

<sub>Tokyo-based web engineer. I build and run 18 production web services solo — design, code, infra, ops and search.</sub>

### 運営しているサービス(抜粋)

| サービス | 中身 |
|---|---|
| [games.omikuji.dev](https://games.omikuji.dev) | 登録不要のブラウザゲーム 73 本。日替わり seed で全員が同じ問題を解き、**手順をサーバーで再生・検証してから**ランキングに記録する |
| [calories.omikuji.dev](https://calories.omikuji.dev) | 外食チェーン 50 社・11,995 品の栄養成分。各社が PDF でしか出していない表を集約した完全静的サイト |
| [diary.omikuji.dev](https://diary.omikuji.dev) | 種類ごとに書き味を変えた日記。本文を書くだけで AI がタイトルとあらすじを付け、傾向をグラフにする |
| [maps.omikuji.dev](https://maps.omikuji.dev) | 誰でも匿名で「◯◯マップ」を作れる UGC 地図 |
| [jichitai.omikuji.dev](https://jichitai.omikuji.dev) | 自治体の公式サイトを再構成した非公式ポータル(新着・イベント・施設マップ) |
| [tools.omikuji.dev](https://tools.omikuji.dev) | 多言語のブラウザ完結ツール集 |

ほかに [emoji](https://emoji.omikuji.dev) / [color](https://color.omikuji.dev) / [calendar](https://calendar.omikuji.dev) / [holiday](https://holiday.omikuji.dev) / [manners](https://manners.omikuji.dev) / [recipes](https://recipes.omikuji.dev) など。

### 公開している OSS

- **[waridake](https://github.com/omikuji/waridake)** — Shift+ドラッグで窓をゾーンに吸着させるだけの macOS ウィンドウスナップ。ディスプレイごとのレイアウト、ビジュアルエディタ。26 言語
- **[hakarasenai](https://github.com/omikuji/hakarasenai)** — Google Analytics に測らせないだけの Firefox 拡張(デスクトップ / Android)。[AMO で公開中](https://addons.mozilla.org/firefox/addon/hakarasenai/)。
  公式オプトアウトが CSP の厳しいサイトで黙って失敗する問題を、MAIN world の content script と declarativeNetRequest の 2 層で塞いでいる

### どう運用しているか

- **構成**: Astro + Cloudflare Workers。DNS・キャッシュ設定は Terraform で管理し、本番反映は `main` への push だけ
- **コストを設計で抑える**: 従量課金 DB がクローラーに増幅されて課金事故を起こしたのを機に、全サービスを定額のセルフホスト DB へ移行。
  以後、従量課金のデータストアは採用せず、公開 URL 面には必ずサーバー側の上限を付ける
- **観測**: 自宅の Raspberry Pi 5 で Prometheus / Thanos / Grafana を回し、Cloudflare の日別使用量・死活・バックアップ鮮度を監視。
  値のアラートには「データが来ていない」ことのアラートも必ず添える
- **検索との付き合い方**: 消したページは 404 で放置せず 410 を返す(放置分を数えたら 1 万 URL 超あった)

### 書いているもの

- [omikuji.dev](https://omikuji.dev) — ブログ
- [はてなブログ](https://omikuji-dev.hatenablog.com) — 作ったツールの紹介と、その裏側の技術
