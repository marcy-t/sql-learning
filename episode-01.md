# episode-01~SQL何それ美味しいの？〜美味くはないが血肉になる
- データを自分で抽出する重要性

# テーブル〜データを入れる受け口を作る
``` sql
create table testtable1 ( ← テーブルを作成 
  id integer primary key
, name text not null unique 
, age integer
);
```

# データを入れてみる
``` sql
insert into testtable1(id, name, age) values (101, 'Alice', 20);
insert into testtable1(id, name, age) values (102, 'Bob', 25);
insert into testtable1(id, name, age) values (103, 'Cathy', 22);
```

# まとめて入れる方法
``` sql
insert into testtable1(id, name, age) 
values (104, 'Jobs', 56)
     , (105, 'Gates' , 64) 
     , (106, 'Bezos', 56);
```

# メイン〜テーブルを検索
- テーブルに挿入した行を検索してみます。そのためには select 文を使います。
``` sql
select *          ← 「*」はすべての列を表示 
from testtable1;  ← テーブルの行をすべて表示
```
###  行は横、列は縦です。

- 実行結果
``` sql
  id | name  | age 
-----+-------+----- 
  101|Alice| 20 
  102|Bob  | 25 
  103|Cathy| 22
(3 rows)
```
- ある特定の列だけを検索する。
``` sql
select name 
from testtable1;
```

- ある特定の行だけを検索する。
``` sql
select name 
from testtable1
where name = 'Bob';
```

# まとめ
``` sql
select {表示させたい列名} 
from {表示させたいデータの指定}
where {表示させたいデータの検索条件};
```

# 練習問題
- 問題 1:テーブルを作成
  - ID と名前と年齢の列を持つ、次のようなテーブルを作成してください
``` sql
create table testtable1 (
  id   integer primary key
, name text    not null
, age  integer
);
```

- 問題 2:データを挿入
  - テーブル「testtable1」に、次のような行を挿入してください。
    - ID=101、名前=Alpha、年齢=20 
    - ID=102、名前=Blavo、年齢=25
    - ID=103、名前=Charlie、年齢=23  

- 問題 3:検索
  - テーブル「testtable1」の行をすべて検索してください。
  - 名前が「Blavo」の行だけを検索してください。
  - 年齢が 22 歳以上の行だけを検索してください。
