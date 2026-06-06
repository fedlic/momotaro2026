# momotaro2026

桃太郎を、AI創作用の構造データとして管理するためのリポジトリです。

物語を文章の要約としてではなく、世界、人物、勢力、アイテム、宝物、出来事、主張、語り、スキーマに分解し、YAMLで扱える形にしています。

## 目的

- AIが物語要素を参照しやすい形にする
- 二次創作、別視点生成、再構成、ゲーム化に使える素材にする
- 桃太郎側と鬼側の主張を両方保持する
- アイテムや宝物を、所有権・象徴・効果・リスクまで含めて管理する

## メインデータ

```txt
story-representation/
├── README.md
├── schemas/
└── worlds/
    └── momotaro/
        ├── texts/
        │   └── original_ja.md
        ├── story.yml
        ├── world.yml
        └── ...
```

詳しい設計思想とディレクトリ構造は、[story-representation/README.md](story-representation/README.md) を参照してください。

## 桃太郎 標準テキスト

構造化データの基準本文として、[story-representation/worlds/momotaro/texts/original_ja.md](story-representation/worlds/momotaro/texts/original_ja.md) に普通の桃太郎の再話を置いています。

この本文は特定の刊本からの引用ではなく、このリポジトリ用に新しく書いた標準テキストです。AIがYAMLデータだけを見て話の全体像を見失わないように、出来事の順番、登場人物、主要アイテム、宝物の登場箇所を確認するための参照元として使います。

構造データを編集するときは、まず標準テキストで物語の流れを確認し、対応する `events/`、`characters/`、`items/`、`claims/` を更新します。逆に、鬼側視点や別展開を生成するときは、標準テキストを「人間側の基本語り」として扱い、`claims/oni_side.yml` や `factions/oni_clan.yml` で視点をずらします。

## 含まれる要素

- `world`: 桃太郎世界の土地、ルール、中心対立
- `characters`: 桃太郎、老夫婦、犬、猿、雉、鬼、子鬼
- `factions`: 鬼一族、鬼ヶ島の社会と経済
- `items`: 桃、きびだんご、船、刀、金棒など
- `treasures`: 打ち出の小槌、珊瑚の枝、隠れ蓑、金貨、銀貨、絹の反物、宝箱
- `events`: 桃の発見、誕生、旅立ち、仲間集め、鬼ヶ島到着、戦闘、帰還
- `claims`: 桃太郎側と鬼側の言い分
- `narratives`: 原典寄りの語りと別視点生成の入口
- `texts`: 構造化の基準になる普通の桃太郎本文
- `schemas`: 他作品にも転用できるYAML項目定義

## 検証

YAMLとして壊れていないかは、以下で確認できます。

```bash
ruby -e 'require "yaml"; files = Dir["story-representation/**/*.yml"].sort; files.each { |f| YAML.load_file(f) }; puts "ok: #{files.size} yaml files"'
```
