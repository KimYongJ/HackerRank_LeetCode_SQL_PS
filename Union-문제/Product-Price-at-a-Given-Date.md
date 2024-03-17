# **Product-Price-at-a-Given-Date**

- [https://leetcode.com/problems/product-price-at-a-given-date/](https://leetcode.com/problems/product-price-at-a-given-date/)
- **문제 :** '2019-08-16' 날짜에 모든 제품에 대한 가격을 출력해야 합니다. 제품 가격은 10부터 시작합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Products (
    product_id INT,
    new_price INT,
    change_date DATE,
    PRIMARY KEY (product_id, change_date)
);
INSERT INTO Products (product_id, new_price, change_date) VALUES
(1, 20, '2019-08-14'),
(2, 50, '2019-08-14'),
(1, 30, '2019-08-15'),
(1, 35, '2019-08-16'),
(1, 65, '2019-08-17'),
(3, 20, '2019-08-18');
```

```jsx
[ 정답 ]
with temp as(
		select	product_id
		,		price
		from(
			select	product_id
			,		row_number() over(partition by product_id order by change_date desc) rnk
			,		new_price as price
			from products
			where change_date <= '2019-08-16'
		)temp
		where rnk = 1
)
select *
from temp

union all

select	product_id
,		10 as price
from products
where product_id not in (select product_id from temp)
group by product_id

```

- **해설**
  - 2019-08-16 일 이전에 가격이 변경되었고, 2019-08-16에 가장 가까운 날짜의 가격을 출력하는 쿼리 temp를 만듭니다. row_number 함수를 사용해 제품 아이디 별 가격 변동일을 기준으로 내림차순 정렬해 2019-08-16날짜와 가장 가까운 가격을 가져 옵니다.
  - 그 후 가격이 2019-08-17일 이후 부터 변경된 제품에 대해 제품 아이디와 가격(기본값 10)을 가져오기 위해, 위에서 만든 temp 테이블에 없는 제품 아이디만 출력해주도록 구현했습니다.
