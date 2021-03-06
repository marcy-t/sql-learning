# episode-06〜時間操作

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
,   (5, '南部鉄夫', '1984-04-06','M')
;

CREATE TABLE IF NOT EXISTS used_history (
  id integer references customer(id),
  payment_id text,
  amount integer,
  created_at timestamptz
);

insert into used_history (id, payment_id, amount, created_at)
values 
    (1, 'hjgvcmhj576uyd', 6787,'2020-03-01 7:34:22')
,   (1, 'isuhepo878w673', 876,'2020-03-04 16:44:23')
,   (1, '8276394hahr289', 3459,'2020-03-06 12:00:00')
,   (2, 'hjklajh8234nbe', 456,'2020-02-01 09:10:00')
,   (2, 'ujntgvedy7u923', 9873,'2020-02-05 08:43:40')
,   (2, 'yhgwerdsfx9828', 2974,'2020-02-10 11:33:54')
,   (2, 'nyhgce8744qwj3', 9353,'2020-02-21 16:23:45')
,   (3, 'siugf9823fkahw', 763,'2020-02-21 16:23:45')
,   (3, 'nu827uahr093rr', 1000,'2020-02-22 10:00:10')
,   (3, '2wsxfrt6yhgkjh', 540,'2020-03-02 12:02:40')
,   (3, '09oilklhe72eud', 780,'2020-03-05 20:12:30')
,   (4, '8ujn3wsxtgbrss', 320,'2020-02-01 20:12:30')
,   (4, 'pp;;[;,mashxyy', 643,'2020-02-10 13:11:20')
,   (4, '345g2hdyuiwehd', 2381,'2020-02-11 16:12:20')
,   (4, '56123hgfsd67df', 5600,'2020-02-19 07:45:15')
,   (5, 'ertynbvcxxcvbe', 9876,'2020-02-04 09:55:00')
,   (5, '98234kfuyhwssw', 761,'2020-02-07 12:55:00')
,   (5, '1qase4juc9idkj', 120,'2020-02-09 16:32:00')
,   (5, 'oked82wjnedfi9', 230,'2020-02-12 14:31:00')
;


select * from customer;

select * from used_history;

```


# データを結合して見ましょう

``` sql
select 
    * 
from 
    customer
,   used_history
;
```

- 共通するデータを結合して見ましょう

``` sql
select 
   * 
from 
    customer
,   used_history
where 
customer.id = used_history.id
;
```

# 日付から年齢を出す

- 年齢の求め方「現在日 - 生誕日」
- 現在は `select current_date;`

``` sql
select current_date;

select 
    customer.name as 名前
,   customer.age  as 生年月日
,   age(current_date, customer.age::timestamp) as 年齢
,   EXTRACT(YEAR FROM age(current_date, customer.age::timestamp)) as 歳
from 
    customer
,   used_history
where 
customer.id = used_history.id
;

```
- これでデータが結合されたデータと年齢が出るかと思います。
- customer.age::timestampと指定している内容はこのcustomer.ageは日付ですと指定する宣言文のようなものになります。

# 問題
- 1.年齢が30歳以下のデータを出力してください

- 出力結果
``` sql
大内里奈	1993-05-03	26 years 10 mons 29 days	26
伴香音	   1991-12-17	 28 years 3 mons 15 days	28
```

- 2.2020-03-01より前の使用ユーザを出力してください。
- 出力結果
``` sql
2	諸星康治	456	2020-02-01 09:10:00
4	大内里奈	320	2020-02-01 20:12:30
5	南部鉄夫	9876	2020-02-04 09:55:00
2	諸星康治	9873	2020-02-05 08:43:40
5	南部鉄夫	761	2020-02-07 12:55:00
5	南部鉄夫	120	2020-02-09 16:32:00
2	諸星康治	2974	2020-02-10 11:33:54
4	大内里奈	643	2020-02-10 13:11:20
4	大内里奈	2381	2020-02-11 16:12:20
5	南部鉄夫	230	2020-02-12 14:31:00
4	大内里奈	5600	2020-02-19 07:45:15
3	伴香音	763	2020-02-21 16:23:45
2	諸星康治	9353	2020-02-21 16:23:45
3	伴香音	1000	2020-02-22 10:00:10
```


- 3.'2020-02-01' から '2020-02-10'の間のユーザを出力してください  
日付の間を出すにはbetweenを使います。

``` sql
where 
used_history.created_at between '2020-02-01' and '2020-02-10'
```

- 出力結果
``` sql
2	諸星康治	9873	2020-02-05 08:43:40
2	諸星康治	456	  2020-02-01 09:10:00
4	大内里奈	320	  2020-02-01 20:12:30
5	南部鉄夫	120	  2020-02-09 16:32:00
5	南部鉄夫	761	  2020-02-07 12:55:00
5	南部鉄夫	9876	2020-02-04 09:55:00
```


