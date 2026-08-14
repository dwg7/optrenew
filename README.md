# optrenew

国土地理院最適化ベクトルタイル向けのリニューアル風 MapLibre スタイル。

## Concept

このリポジトリは、国土地理院最適化ベクトルタイルを対象とした、標準地図リニューアル版の**設計思想**を翻訳した MapLibre GL JS 用スタイルを提供します。

> このスタイルは標準地図リニューアル版のピクセル単位の再現ではなく、その設計思想を国土地理院最適化ベクトルタイルおよび spiccato 背景地図の文脈に翻訳したものです。

設計方向性:

> 伝統的な地形図表現から派生した硬い地図から、現代的で再利用可能な、静かで信頼性の高い Web ベースマップへ。

マップはユーザーの情報に主役を譲りながら、国土地理院データに期待される信頼性と地形認識を保持します。

## Why Two Styles

| スタイル | 用途 |
|---|---|
| `optrenew-std` | 汎用標準ベースマップ。リニューアル標準地図に近い設計。 |
| `optrenew-pale` | オーバーレイ向け淡色スタイル。災害情報・統計・センサーデータとの重ね合わせに最適。 |

## optrenew-std

標準地図リニューアル版の設計思想に最も近いスタイルです。

- 温かみのある淡いベージュ・グレーの背景
- 明確な水域表現（青系）
- 道路ヒエラルキーが読みやすい配色
  - 高速道路: くすんだグリーン
  - 国道・主要道路: くすんだオレンジ・レッド系
  - 都道府県道: 柔らかいオーカー・イエロー
  - 市区町村道: オフホワイト・ライトグレー
- 控えめな等高線（褐色・低彩度）
- Mapterhorn 地形陰影対応

## optrenew-pale

オーバーレイとの重ね合わせを優先した淡色スタイルです。

- 彩度・コントラストを低減
- 道路・境界線・等高線・注記を弱く設定
- 災害対応、行政調整、統計可視化、センサーデータ表示に適している
- 単独でも地図として十分に読める

## Design Intent

- 純白の背景を避け、温かみのあるオフホワイト・薄ベージュを使用
- 高彩度の黄色い道路を避け、落ち着いた道路ヒエラルキーを実現
- 等高線の視覚的重さを軽減し、地形陰影との競合を防ぐ
- ラベルはダークグレーで可読性を保ちつつ目立ちすぎない
- 建物は都市密度を伝えるが個々の建物が競争しない表現

## Relationship to the Renewed GSI Standard Map

このスタイルは公式の標準地図リニューアル版ではありません。リニューアル版の設計方向性——温かみのある面色、明確な水域表現、より読みやすい都市コンテキスト、控えめな等高線——を、最適化ベクトルタイルのレイヤー定義の範囲内でスタイルとして翻訳したものです。

## Relationship to GSI Optimal BVMap

ベクトルソースは国土地理院最適化ベクトルタイル（`stars.optgeo.org/bvmap`）を使用します。レイヤー定義は `gsi-cyberjapan/optimal_bvmap` の `style/std.json` を参照基点としています。

## Relationship to Spiccato

このスタイルは [spiccato](https://github.com/dwg7/spiccato) の背景地図置き換え候補として設計されています。

- ソースは spiccato が参照するものに準拠（`bvmap`, `mapterhorn`）
- 地形・陰影は spiccato 背景地図に準拠
- 将来的に spiccato の背景地図を置き換えることを目指す

## Sources and Terrain

| ソース | 種別 | URL |
|---|---|---|
| `bvmap` | vector | `https://stars.optgeo.org/bvmap/{z}/{x}/{y}` |
| `mapterhorn` | raster-dem | `https://tiles.mapterhorn.com/{z}/{x}/{y}.webp` |

- 地形エンコーディング: terrarium
- 地形誇張: std=1.0, pale=0.8
- 属性表記: 国土地理院最適化ベクトルタイル / [Mapterhorn](https://mapterhorn.com/attribution)

## GitHub Pages Demo

デモサイト（GitHub Pages 有効化後）:

```
https://dwg7.github.io/optrenew/
```

スタイル JSON 直接参照:

```
https://dwg7.github.io/optrenew/optrenew-std.json
https://dwg7.github.io/optrenew/optrenew-pale.json
```

## Style Catalog Registration

> The upload method for the Martin instance used by stars.optgeo.org is not implemented in this repository yet. It will be provided later through an interactive Claude Code session.

将来の登録先: [https://stars.optgeo.org/?tab=styles](https://stars.optgeo.org/?tab=styles)

登録予定スタイル:
- `optrenew-std`
- `optrenew-pale`

## What Can Be Reflected by Styling

スタイルレベルで実現できること:

- 背景色・水域・地形の配色変更
- 道路ヒエラルキーの色分け
- 等高線・境界線の視覚的重さの調整
- 地形陰影の設定
- ラベルの濃度・ハロー調整
- ズームレベルごとの表示制御

## What Requires Data Refresh

スタイルのみでは実現できない事項:

- 高品質の一般化された都市域ポリゴン（データ依存）
- 建物密度に基づく都市テクスチャ（データ依存）
- 土地利用・土地被覆の再分類（ソースデータ変更が必要）
- 高度なラベル優先制御（前処理が必要）
- リニューアル標準地図の一部効果（最適化ベクトルタイルに存在しないデータに依存）

## Test Locations

| 地点 | 確認項目 |
|---|---|
| 熊本 | 都市域・水系・道路・丘陵・海岸・地形 |
| 札幌 | 広大な平野・河川・山岳縁・道路ネットワーク |
| 東京 | 高密度道路・鉄道・ラベル密度・建物 |
| 仙台 | 都市と山地の境界 |
| 名古屋 | 平野都市・河川デルタ |
| 大阪 | 港湾・水系・都市密集 |
| 広島 | デルタ地形・海岸 |
| 福岡 | 北部九州の都市 |
| 那覇 | 海岸線・島嶼・水色表現 |
| 松本 | 山岳地形・等高線密度・地形陰影 |

## TODO

- [ ] Test `optrenew-std.json` on GitHub Pages.
- [ ] Test `optrenew-pale.json` on GitHub Pages.
- [ ] Compare both styles against the original GSI optimal_bvmap `std.json`.
- [ ] Compare both styles in spiccato-like use cases.
- [ ] Prepare metadata for the stars.optgeo.org styles catalog.
- [ ] Upload the styles to the Martin instance used by stars.optgeo.org.
- [ ] Register `optrenew-std` in the styles catalog.
- [ ] Register `optrenew-pale` in the styles catalog.
- [ ] Evaluate whether spiccato should switch its background style to `optrenew-std` or `optrenew-pale`.

The upload procedure for the Martin instance used by stars.optgeo.org is intentionally left as a TODO. It will be provided later during an interactive Claude Code session.

## License

CC0-1.0 — パブリックドメイン相当。スタイル JSON、デモ HTML、メタデータを含みます。

データ出典（地図データそのものの著作権は各提供者に帰属）:
- 国土地理院最適化ベクトルタイル
- [Mapterhorn](https://mapterhorn.com/attribution) (地形 DEM)

## Acknowledgements

- [国土地理院 / GSI](https://www.gsi.go.jp/) — 最適化ベクトルタイルデータ
- [gsi-cyberjapan/optimal_bvmap](https://github.com/gsi-cyberjapan/optimal_bvmap) — スタイル参照
- [Mapterhorn](https://mapterhorn.com/) — 地形 DEM
- [MapLibre GL JS](https://maplibre.org/) — レンダリングエンジン
- [dwg7/spiccato](https://github.com/dwg7/spiccato) — ソース・地形設定の参照