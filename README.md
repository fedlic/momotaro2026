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
```

詳しい設計思想とディレクトリ構造は、[story-representation/README.md](story-representation/README.md) を参照してください。

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
