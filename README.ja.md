[한국어](README.md) · [English](README.en.md) · **日本語**

# tripo-model-reference-pack

Tripo(画像 → 3D)に入力するリファレンス画像を、毎回同じ規格で作るためのエージェントスキルです。
モデル1つにつき、画像4枚と仕様書1枚ができます。

| ファイル | 内容 |
| --- | --- |
| `front.png` `right.png` `back.png` | グレーのクレイ表現の正面・右側面・背面。ビューごとに個別に生成します |
| `textured_front.png` | 正面と同じ形状に、色と表面だけを加えた画像 |
| `spec.md` | ゲーム内のサイズ(cm)、頂点・Quad・三角形の予算、形状とテクスチャのメモ、チェック結果 |

## インストール

エージェントの skills フォルダーに、このリポジトリをそのままクローンします。

```
# Claude Code
git clone https://github.com/RevStudio/tripo-model-reference-pack ~/.claude/skills/tripo-model-reference-pack

# Codex
git clone https://github.com/RevStudio/tripo-model-reference-pack ~/.codex/skills/tripo-model-reference-pack
```

エージェント側に、画像を新規生成でき、既存の画像を参照して編集できるツールが必要です。
ツールがない場合、スキルはドキュメントとプロンプトの準備までを行い、画像は生成しません。

## 使い方

```
tripo-model-reference-pack スキルで、このモデルのグレーの三面図3枚と、同じ形状のテクスチャ付き正面1枚を作って、
ゲーム内サイズと推奨の頂点予算をドキュメントにまとめて。
モデル:古い貯水タンク、153×172×215cm、ローポリ、錆びた鉄板の質感
```

## 入っているもの

- `SKILL.md` — 成果物のルール、作業順序(正面 → 側面・背面 → テクスチャ付き正面)、最終チェック項目、フォルダー構成
- `references/prompt-recipes.md` — ビューごとのプロンプト、軸と視点の規約、不具合ごとの修正プロンプト
- `references/scale-budget-and-art.md` — サイズとポリゴン予算の書き方と、プリセットの**例**。自分のプロジェクトの値に置き換えて使ってください
- `assets/model-spec-template.md`、`assets/vertex_budgets.csv` — 仕様書のテンプレートと予算表のヘッダー

## 言語について

スキルのファイルは韓国語で書かれています。中に含まれる画像生成用のプロンプトは英語です。
`SKILL.md` には「仕様とチェック結果は韓国語で伝える」という指示があるので、別の言語にしたい場合はその行を書き換えてください。

## 知っておくこと

- 3つのビューは同じ3Dモデルを投影したものではなく、個別に生成した近似です。寸法が食い違う場合は、ドキュメントの数値を優先します。
- 頂点・Quad・三角形の数は制作上の目標です。Tripoがその数に合わせてくれるわけではありません。
- Tripoでの生成とアップロード、Blenderでのメッシュ整理、エンジンへのインポートは、このスキルの範囲外です。
