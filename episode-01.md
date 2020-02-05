# episode-01~SQL何それ美味しいの？〜美味くはないが血肉になる
- データを自分で抽出する重要性

# テーブル〜データを入れる受け口を作る
``` sql
create table testtable (
  id integer primary key
, name text not null unique 
, age integer
);
```

# データを入れてみる
``` sql
insert into testtable(id, name, age) values (101, 'Alice', 20);
insert into testtable(id, name, age) values (102, 'Bob', 25);
insert into testtable(id, name, age) values (103, 'Cathy', 22);
```

# まとめて入れる方法
``` sql
insert into testtable(id, name, age) 
values (104, 'Jobs', 56)
     , (105, 'Gates' , 64) 
     , (106, 'Bezos', 56);
```

# メイン〜テーブルを検索
- テーブルに挿入した行を検索してみます。そのためには select 文を使います。
``` sql
select *          ← 「*」はすべての列を表示 
from testtable;  ← テーブルの行をすべて表示
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
from testtable;
```

- ある特定の行だけを検索する。
``` sql
select name 
from testtable
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
  - 1.テーブル「members」の行をすべて検索表示してください。
  - 2.名前が「エレン」の行だけを検索表示してください。
  - 3.性別が 女性(F:Female)の行だけを検索表示してください。
  - 4.名前と身長だけを全て検索表示してください。
  
  
# where {表示させたいデータの検索条件};の応用その１
- ある特定の行だけを選ぶ(あるいは除外する)には、where 句で条件を指定します。
- するとその条件に合った行だけが出力されます。

### 例）名前が「ミカサ」である行だけを選ぶ
``` sql
select *
from members
where name = 'ミカサ';
```

- 「＝」を今回使いましたが他にも記号を使えます。
### 「<>」* (等しくない)だけでなく、「>」 「>=」 「<」 「<=」 も使えます。
  
- 身長が「170」cm 以上の行を選ぶ

``` sql
select *
from members
where height >= 170;
```

# whereの応用その２ 複数の条件で検索
- where height >= 170とつけて検索条件をつけましたがこれに「AND」をつけるとさらに条件を絞っての検索が可能です。
- 「~ and ~」は「~ かつ ~」

``` sql
select * from members
where gender = 'M'
and height >= 170;
``` 

- 性別が「M」(Male, 男性) であり
- かつ身長が「170」cm以上の行だけを選ぶ

もちろんOR（〜と〜）で検索も可能です

``` sql
select * from members
where gender = 'M'
or height >= 170;
``` 

- 上記の場合男性か？身長が170cmか？と言う少し緩い検索条件になりました。

# 表示する内容を制限する
- 今はまだ6件ほどデータで操作していますが、これが何千万件〜となったらどうでしょう？
- そんなにデータがいらない場合は、「limit」を使います。（そのまんまです）

``` sql
select * from members limit 3;
```

- 3件のみ表示されるかと思います。
- こうして内容を制限し目的の量にあった検索を行えます。

# order by〜整列
- 小さい順や大きい順に並び替えることを、整列 (Sort) といいます。
- 身長が低い順番、高い順番などに並び替えることができます。

``` sql
select *
from members order by height;
```

- そして名前順（五十音順）にもできます
``` sql
select *
from members order by name;
``` 

- 明示的に大きい順、小さい順などを指定することもできます

``` sql
- 小さい順
select *
from members order by name asc;
``` 

``` sql
- 大きい順
select *
from members order by name desc;
``` 

# ここまでで
- select 文が行うのは「データの加工」
- 自分が検索したい条件を選択し、「加工」と「変形」を行うことをやりました。

# 練習問題
- 問題文章からデータ検索表示してください。
  - 問題 1:
    - 身長の高い順に3名の男子を選び出力（表示項目）は身長と名前だけ
   　のデータを検索表示してください。

# 多くの人がつまづく理由
- この問題のポイントは、「男女別に分かれる」という仕様を「性別で並び替える」という方法に言い換えられるか？という点です。
- 別の言い方をすれば、「業務用件の言葉を実装技術の言葉に置き換えられるか？」です。
 - 「男女別に分かれる」← これは業務の用件の言葉
 - 「性別で並び替える」← これは業務の用件の言葉
- 多くの人がつまづく理由はこれです。
- SQLを知らなくて書けないのはもちろんですが言葉を実装技術の言葉に置き換えられるかが、差になります。

