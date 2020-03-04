# episode-03~便利な機能

## おさらい

``` sql
select {表示させたい列名} 
from {表示させたいデータの指定}
where {表示させたいデータの検索条件}
order by {表示させたいデータの整列}
limit {表示させたいデータの制限}
;
```

# 作成
``` sql
-- 映画
create table movies (
  movie_id integer primary key
, title text not null unique );


insert into movies (movie_id, title) 
values 
    (93, '風の谷のナウシカ')
,   (94, '天空の城ラピュタ') 
,   (95, 'となりのトトロ')
,   (96, '崖の上のポニョ')
;

-- キャラクター
create table characters (
    id integer
,   movie_id integer
,   name text
,   gender char(1) )
;


insert into characters (id, movie_id, name, gender)
values 
    (401, 93, 'ナウシカ', 'F')
,   (402, 94, 'パズー', 'M')
,   (403, 94, 'シータ', 'F')
,   (404, 94, 'ムスカ', 'F')
,   (405, 95, 'さつき', 'M')
,   (406, 95, 'メイ', 'F')
,   (407, null, 'クラリス', 'F')
;
```

# group by テーブルの内容をグループに分けて集計


# 列の別名
- SQL では、列や式に別名 (Alias) をつけられます

``` sql
select 
    id as ID
,   name as 名前
,   height as 身長 
from members
where gender = 'F'
;
```

# テーブルの別名
- テーブルにも別名 (Alias) がつけられます。

``` sql
select 
    m.id
,   m.name
,   m.height
from 
members m 
where m.gender = 'F'
order by m.id
;
```


