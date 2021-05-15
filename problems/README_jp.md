# 問題の記述方法

<u>作問者へ： JSON ファイルを書いてください。</u>  

## JSON の様式

問題は、以下のようなJSONファイルで定義する必要があります。

```json
{
  "DDL": [  // List of strings
    "create table Foo (",
    "    xxx varchar(256) primary key,",
    "    yyy varchar(256),",
    "    zzz varchar(256)",
    ");",
    "create table another ..."
  ],
  "description": [  // Optional
    "Hello!",
    "This is message from writer."
  ],
  "tables": [  // List of tables
    {  // Table information
      "name": "Name of Table",
      "columns": ["names", "of", "columns"],
      "records": [
        ["Hi!", "Foo", "Bar"]
      ]
    }
  ],
  "expected": {  // Expected output
    "columns": ["names", "of", "columns"],
    "records": [
        ["Hi!", "Foo", "Bar"]
    ],
    "order_sensitive": false  // ORDER BY など、順序の一致を求めるなら true
  }
}
```

> メモ： JSON ファイル名は問題名としても使用されます。

例： これは、サンプル問題の JSON です。  
(`problem/sample-1.json`)

```json
{
  "DDL": [
    "create table Students (",
    "    id int primary key,",
    "    name varchar(16)",
    ");"
  ],
  "description": [
    "This is the first problem.",
    "Just select all."
  ],
  "tables": [
    {
      "name": "Students",
      "columns": ["id", "name"],
      "records": [
        [1, "Alice"],
        [2, "Bob"],
        [3, "Charlie"],
        [4, "David"]
      ]
    }
  ],
  "expected": {
    "columns": ["id", "name"],
    "records": [
        [1, "Alice"],
        [2, "Bob"],
        [3, "Charlie"],
        [4, "David"]
    ],
    "order_sensitive": false
  }
}
```

この場合、この表が与えられます。

テーブル： Students
| id | name    |
|----|---------|
| 1  | Alice   |
| 2  | Bob     |
| 3  | Charlie |
| 4  | David   |

そして期待される出力はこのようになります。 
（今回は、与えられたテーブルと同じになっています）

| id | name    |
|----|---------|
| 1  | Alice   |
| 2  | Bob     |
| 3  | Charlie |
| 4  | David   |

そして、ユーザは問題を解決するようなSQLコードを書きます。  
> もちろん、答えは "`select id, name from Students;`" です。