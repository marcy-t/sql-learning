# episode-01~SQL何それ美味しいの？〜美味くはないが血肉になる
- データを自分で抽出する重要性

# テーブル〜データを入れる受け口を作る
``` sql
create table User ( ← テーブルを作成 
  id integer primary key
, name text not null unique 
, age integer
);
```

# データを入れてみる
``` sql
insert into User(id, name, age) values (101, 'Alice', 20);
insert into User(id, name, age) values (102, 'Bob', 25);
insert into User(id, name, age) values (103, 'Cathy', 22);
```

# まとめて入れる方法
``` sql
insert into User(id, name, age) 
values (104, 'Jobs', 56)
     , (105, 'Gates' , 64) 
     , (106, 'Bezos', 56);
```

# メイン〜テーブルを検索
- テーブルに挿入した行を検索してみます。そのためには select 文を使います。
``` sql
select *          ← 「*」はすべての列を表示 
from User;  ← テーブルの行をすべて表示
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
from User;
```

- ある特定の行だけを検索する。
``` sql
select name 
from User
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
  - ID と名前と身長と性別の列を持つ、次のようなテーブルとデータ作成してください
``` sql
- テーブル「members」を作成 primary key

create table members (
  id integer not null
, name text not null
, height integer , gender char(1) not null 
);


insert into members(id, name, height, gender)
values 
  (101, 'エレン', 170, 'M')
, (102, 'ミカサ', 170, 'F') 
, (103, 'アルミン', 163, 'M')
, (104, 'ジャン',175, 'M')
, (105, 'サシャ',168, 'F')
, (106, 'コニー',158, 'M')
;
```

- 問題 2:検索
  - 1.テーブル「members」の行をすべて検索してください。
  - 2.名前が「えれん」の行だけを検索してください。
  - 3.性別が 女性(F:Female)の行だけを検索してください。
  
  
  
