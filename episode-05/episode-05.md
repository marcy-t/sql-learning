# episode-05~

## おさらい
``` sql
select {表示させたい列名} 
from {表示させたいデータの指定}
where {表示させたいデータの検索条件}
order by {表示させたいデータの整列}
limit {表示させたいデータの制限}
;
```

## 下記のテーブルを追加してください(前回の参加者は入れなくていいです)
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
,   (404, 94, 'ムスカ', 'M')
,   (405, 95, 'さつき', 'M')
,   (406, 95, 'メイ', 'F')
,   (407, null, 'クラリス', '')
;

create table comment (
    id integer
,   movie_id integer
,   comment text
)
;

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

# Like 検索
- 曖昧なワードの検索をする際によく使われる

``` sql
select
    *  
from
    characters
where 
    name like '%ナウ%'
;
```

- %%の中で調べたい語句や単語をいれる
- 「%{ワード}%」でやるとこういう風に検索します「○○○ナウ○○○」と含まれているものを調べる
- 「%{ワード}」でやるとこういう風に検索します「○○○ナウ」と含まれているものを調べる
- 「{ワード}%」でやるとこういう風に検索します「ナウ○○○」と含まれているものを調べる
- ワードや単語がいろいろ分からない時に使ったりします。


#case 式
- case 式 (CASE expression) とは、条件分岐を行う式です
- case 式の文法:条件式によって値が変わる

``` text
case
when 条件式1 then 値1 when 条件式2 then 値2 ....
else 値n
end
← もし条件式1が成り立てば値1になり、 ← もし条件式2が成り立てば値2になり、
← どれも成り立たなければ値nになる
```

# Sample
``` sql
select
    case 
      when gender = 'M' then '男性'
      when gender = 'F' then '女性'
      else '--'
    end as gender  
from
    characters
; 
----------------------
女性
男性
女性
男性
男性
女性
--
```

``` sql
select
    name
,   case 
      when gender = 'M' then '男性'
      when gender = 'F' then '女性'
      else '--'
    end as gender  
from
    characters
;ナウシカ	女性
パズー	男性
シータ	女性
ムスカ	男性
さつき	男性
メイ	女性
クラリス	--
```

# カテゴリ分けも任意でできるようになります
``` sql
select
    case 
      when characters.name = 'ナウシカ' then '風の谷のナウシカ'
      when characters.name = 'ムスカ' then 'ラピュタ'
      when characters.name = 'メイ' then 'トトロ'
      else '--'
    end   
,   comment.comment
from
    movies
,   characters
,   comment
where movies.movie_id = characters.movie_id
and characters.id = comment.id
;
```


# 問題1
- 下記のデータセットを作りなさい


| title | name  | カテゴリコメント |
| --- | --- | --- |
| 風の谷のナウシカ | ナウシカ | -- |
| 天空の城ラピュタ | パズー | 僕は海賊にはならないよ |
| 天空の城ラピュタ | シータ | リュシータ・トエル・ウル・ラピュタ |
| 天空の城ラピュタ | ムスカ | ロムスカ・パロ・ウル・ラピュタ |
| となりのトトロ | さつき | 七石山病院 |
| となりのトトロ | メイ | トトロいたもん |


# 問題2
- 上記のデータセットからLIKEを使いコメントを指定してデータの絞り込みをしてください


| title | name  | カテゴリコメント |
| --- | --- | --- |
| 天空の城ラピュタ | シータ | リュシータ・トエル・ウル・ラピュタ |

