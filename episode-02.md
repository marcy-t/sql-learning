# episode-02~グループ化と集約〜ぼっちを集めてリア充に

## 前回のおさらい

``` sql
select {表示させたい列名} 
from {表示させたいデータの指定}
where {表示させたいデータの検索条件}
order by {表示させたいデータの整列}
limit {表示させたいデータの制限}
;
```

# group by テーブルの内容をグループに分けて集計ができます。
- 合計する (sum())
- 平均する (avg())
- 最大値を調べる (max()) • 最小値を調べる (min()) 
- 行数を数える (count())

## 前回のテーブル「members」で見てみます
- 次の SQL を実行すると、男女別の平均身長が出せます

``` sql 
select 
    gender
,   avg(height) --  グループごとに平均値を計算 
from 
    members
group by gender -- 性別ごとにグループ化
;
```

- 上記のSQL値が正しいか、確かめてみましょう。
- そのために次の SQL を実行し、男 女別に身長の低い順で整列します。

## 男女別に身長の低い順で整列

``` sql
select 
    *
from 
    members
order by gender desc, height
;
```

- 男女別の平均身長は次のように計算できます。
  - 男子の平均身長: (158+163+170+175) / 4 = 166.5
  - 女子の平均身長: (168+170) / 2 = 169.0
  
# グループ化
- グループ化 (Grouping) とは、何らかのキーを使って行をいくつかのグループ にまとめることです。
- 「行」をグループにするのがポイント
- 前回のクエリを見てみましょう

``` sql
select 
    gender
,   avg(height) --  グループごとに平均値を計算 
from 
    members
group by gender -- 性別ごとにグループ化
;
```
- 「avg()」のように、グループから複数の値を受け取って何らかの値を計算する関数を集約関数 (Aggregate function) と言います


# 集約関数
- sum() ... 合計する
- avg() ... 平均する
- max() ... 最大値を調べる
- min() ... 最小値を調べる
- count() ... 行数を数える

## 男女別に、身長の最大値と最小値と合計値と行数と平均値を計算する

``` sql
select 
    gender
,   max(height)
,   min(height)
,   sum(height)
,   count(*)
,   to_char(avg(height), '999.99') -- 小数点100の位まで出す
from 
    members
group by gender --性別でグループ化 
order by gender desc
;
```

## count(*)だけなんで*?
- この「*」は「行そのもの」を表しています。なので
- 「count(*)」は「行の数を数える」という意味になります。
- count(height)にかくと値が入っていないものに関してはカウントしません

