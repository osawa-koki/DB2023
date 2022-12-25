# DB2023

データベーススペシャリスト試験対策用のサイト。  
Hugoで開発。  

## イロイロ

```shell
# 新規記事の作成
hugo new textbook/<名前>.md
# ついでにconfig.tomlファイルにもページを追加しておく。
```

## 実行方法

```shell
# デバグ実行
hugo server -D

# デプロイ用ビルド
hugo -d docs
```

## 開発環境

| モジュール | バージョン |
| ---- | ---- |
| Windows | 11 Home |
| Hugo | v0.109.0 |
