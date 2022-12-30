https://note.com/tsuyuri104/n/nf55b77450369?magazine_key=mdb17e3fc1457

# 1回目
```
# Write your MySQL query statement below
select
 u.user_id as buyer_id
,u.join_date as join_date
,count(o.buyer_id) as orders_in_2019
from Users as u
left join Orders as o
    on o.buyer_id = u.user_id
    and order_date >= '2019-01-01'
group by u.user_id
```

* 集約条件をOrders.buyer_idにしていたため、2019年未注文者のレコードが取得できず悩んでしまい時間がかかった。Usersテーブルをfromにしているのだから、Users.user_idで集約すればいいことにもっと早く気づければ。。。笑

# 2回目
```
# Write your MySQL query statement below
select
 u.user_id as buyer_id
,u.join_date as join_date
,count(o.buyer_id) as orders_in_2019
from Users as u
left join Orders as o
    on o.buyer_id = u.user_id
    and YEAR(order_date) = 2019
group by u.user_id
```

* マイベスト。
* 1回目は2272ms、2回目は1074msで早くなった。
* 注文日の型が日付型だったので、YEAR関数を使用した。（業務では日付項目は文字列型を使用することが多いため、ついそのクセで文字列比較してた。。。）
