# episode-06

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


``` sql
CREATE TABLE IF NOT EXISTS customer (
  id bigserial primary key,
  name text,
  age text,
  gender char(1),
  created_at timestamptz default current_timestamp not null
);


insert into customer (id, name, age, gender)
values 
    (1, '下川光政', '1973-01-13','M')
,   (2, '諸星康治', '1981-05-10','M')
,   (3, '伴香音', '1991-12-17','F')
,   (4, '大内里奈', '1993-05-03','F')
;
```
