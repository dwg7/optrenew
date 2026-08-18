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

## Related GSI Initiatives (2026)

このプロジェクトの設計判断は、以下の国土地理院の最新発表を参考にしています。

### 地理院地図（中・小縮尺タイル）のリニューアル

[地理院地図（中・小縮尺タイル）のリニューアル（予告）](https://www.gsi.go.jp/chizuhensyu/chizuhensyu41047.html)（令和8年度第2四半期予定）

このリニューアルは電子地形図50000／20万をベースとした中・小縮尺のラスタタイルが対象で、optrenew が対象とする最適化ベクトルタイル（bvmap）とは系統が異なります。ただし国土地理院自身の地図デザインの方向性を示す一次情報として、以下の変更点は optrenew のスタイル設計における参考材料になります。

- ZL14: 電子地形図50000表現を適用し、等高線等の情報を充実
- ZL12〜13: 電子地形図20万描画を適用し、市街地エリア等の情報を充実
- ZL9〜11: 記号形状・文字色の変更により、ZL12〜14との描画連続性・切り替えを改善
  - 飛行場・港湾記号をそれぞれ1種類に統一
  - 湿地表現をベタ塗りからハッチング（斜線）表現に変更
  - 山系／河川・湖沼系／陸域自然地名の文字色を変更
  - 市区町村界をZL10〜11に追加表示
  - 採鉱地・火山記号の表示を廃止（火山は気象庁の活火山分布を重ね合わせ情報として別途提供）

火山記号を主題図から外し、重ね合わせ情報（オーバーレイ）として提供する方針は、`optrenew-pale` がオーバーレイ用途を主目的とする設計思想と方向性が一致しています。

### 令和8年（2026年）熊本地震への対応

[令和8年熊本地震に関する国土地理院の対応](https://www.gsi.go.jp/BOUSAI/20260728_kumamoto_earthquake.html)

2026年7月28日発生の熊本地震に対し、国土地理院は地理院地図を通じて以下の災害情報を公開しています。

- 空中写真（垂直写真・斜め写真・正射画像、7/29〜8/12撮影）
- 地殻変動データ（電子基準点観測: 北東方向に約87cm、沈降約33cm）
- 活断層図（八代・熊本・日奈久地区）
- 地形分類データ（土地の成り立ちと自然災害リスク）
- 斜面崩壊・堆積分布データ
- 衛星SAR干渉解析による地殻変動
- 震源断層モデル

こうした災害対応レイヤーとの重ね合わせは、まさに `optrenew-pale` が想定する利用シーンです。[Test Locations](#test-locations) の熊本は、通常の地形確認に加えて、災害オーバーレイとの重ね合わせテストの観点でも重要な地点として位置づけます。

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
| 熊本 | 都市域・水系・道路・丘陵・海岸・地形／2026年熊本地震の災害オーバーレイ（地殻変動・活断層・地形分類・斜面崩壊）との重ね合わせ |
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
- [ ] 地理院地図（中・小縮尺タイル）リニューアルの記号変更（湿地ハッチング、飛行場・港湾記号統一、火山のオーバーレイ化）を optrenew のシンボル設計に反映するか検討する。
- [ ] `optrenew-pale` を2026年熊本地震関連の災害オーバーレイ（地殻変動・活断層図・地形分類・斜面崩壊分布）と重ね合わせ、可読性を確認する。

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