# episode-04~SQL WorkOut


## おさらい
``` sql
select {表示させたい列名} 
from {表示させたいデータの指定}
where {表示させたいデータの検索条件}
order by {表示させたいデータの整列}
limit {表示させたいデータの制限}
;
```

## 下記のテーブルを追加してください
- 前回やった人は三番目だけ追加してください

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

-- コメント 前回やった人はこれだけやればいいです
create table comment (
    id integer
,   movie_id integer
,   comment text
)
;

前回やった人はこれだけやればいいです
insert into comment (id, movie_id, comment)
values 
    (401, 93, '多すぎる火は何も生みはせん')
,   (402, 94, '僕は海賊にはならないよ')
,   (403, 94, 'リュシータ・トエル・ウル・ラピュタ')
,   (404, 94, 'ロムスカ・パロ・ウル・ラピュタ')
,   (405, 95, '夢だけど、夢じゃなかった！')
,   (406, 95, 'とうもころし')
;
```

# 問題

## 1.「movies」テーブルのデータを全て出力してください

## 2.「characters」テーブルのデータを全て出力してください

## 3.「comment」テーブルのデータを全て出力してください

## 4.「characters」から、名前(name)と性別(gender)を出力してください

## ５.「characters」から「ナウシカ」を選択し、出力表示は、名前(name)と性別(gender)を出力してください









