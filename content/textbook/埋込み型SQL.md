---
title: "埋込み型SQL"
date: 2022-12-25T23:41:01+09:00
draft: false
description: "プログラミング言語から直接使用するSQLについてです。最近はカーソルとか意識しなくてもよくなっているので、忘れがちですね、、、"
categories: ["DB2023", "教科書"]
tags: ["SQL"]
---

## 埋込み型SQL・会話型SQL

SSMSなどで直接ユーザが実行するSQLを会話型SQLと呼びます。  
それに対してプログラミング言語から直接実行するSQLを埋込み型SQLと呼びます。  

最近はデータベース操作に関するラッパーライブラリが充実しているため、プログラムから簡単にSQLを実行、結果を取得できますが、試験では詳細に問われることがあるため、簡単に説明します。  

## カーソル

SELECT文の結果が複数行になる場合には、プログラミング言語では複数行を操作することができないため、カーソルを操作することで複数行の結果を扱います。  

下のコード(PHP)では`while ($row = $stmt->fetch())`の部分で結果がある限り、カーソルをひとつずつ下に下げることで複数行を処理しています。  

```php
$pdo = new PDO(
  'mysql:dbname=testdb;host=localhost;charset=utf8mb4',
  'root',
  'password',
);
$stmt = $pdo->prepare('SELECT number, name FROM pokemon;');
$stmt->execute();
// カーソルをひとつずつ下げていく。
while ($row = $stmt->fetch()) {
  printf("%s - %s\n", $row['number'], $row['name']);
}
```

## カーソル操作

今更、cobolなんて、、、  
って思いますが、考古学として一応紹介します。  

### EXEC SQL - END-EXEC

`EXEC SQL`でSQL文の開始を、`END-EXEC`でSQL文の終わりを表します。  

### DECLARE カーソル名 CURSOR FOR

`DECLARE カーソル名 CURSOR FOR`でカーソル変数を定義します。  

```cobol
EXEC SQL
DECLARE C1 CURSOR FOR
SELECT number, name
  FROM pokemon
END-EXEC
```

### OPEN - FETCH - CLOSE

`OPEN`でカーソル処理を開始し、`FETCH`でカーソルからデータを取り出し、`CLOSE`でカーソル操作を終了します。  
また、SQLSTATE変数を使用してSQLの実行の成功・失敗を判断します。  

### WHERE CURRENT OF カーソル名

UPDATE文とDELETE文に関しては対象のカーソル位置に関して行う処理であるため、実行に関してはカーソル位置を伝える必要があります。  

```cobol
EXEC SQL
UPDATE
  ...
  WHERE CURRENT OF カーソル名
END-EXEC
```

```cobol
EXEC SQL
DELETE
  ...
  WHERE CURRENT OF カーソル名
END-EXEC
```

### COMMIT

トランザクションを使用する場合には、`COMMIT (WORK)`、`ROLLBACK (WORK)`を使用します。  

```cobol
EXEC SQL
COMMIT (WORK)
END-EXEC
```

```cobol
EXEC SQL
ROLLBACK (WORK)
END-EXEC
```

SQL92では`COMMIT (WORK)`、`ROLLBACK (WORK)`の`WORK`を省略して、`COMMIT ()`、`ROLLBACK ()`と書くことができます。  
