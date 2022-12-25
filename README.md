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

## 注意事項・留意事項

`layouts/_default/single.html`ファイル内にある`{{ lower . }}`の部分は大文字のファイル名が小文字に変換されてしまうバグ回避のため、小文字に変換しているだけで、この問題が解決されたら`{{ . }}`に変換するのが好ましい。  
別に変換しなくても動作には問題ないが、、、  

※ [参考](https://github.com/gohugoio/hugo/issues/7686)  
