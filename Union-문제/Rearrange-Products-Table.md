# **Rearrange Products Table**

- [https://leetcode.com/problems/rearrange-products-table/](https://leetcode.com/problems/rearrange-products-table/)
- **문제 :** 한 제품에 대해 상점마다 가격이 한행으로 들어가있습니다. 이런 테이블 구조를 제품과 상점마다의 가격을 출력하도록 바꾸는 것입니다. 특정 상점에서 제품을 판매하지 않는 경우는 가격이 null로 되어있는데 null은 결과에 포함되지 않도록합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Products (
    product_id INT,
    store1 INT,
    store2 INT,
    store3 INT
);
INSERT INTO Products (product_id, store1, store2, store3) VALUES
(0, 95, 100, 105),
(1, 70, NULL, 80);
```

```jsx
[ 정답 ]
select *
from (
	select	product_id
	,		'store1' as store
	,		store1 as price
	from products
	union
	select	product_id
	,		'store2' as store
	,		store2 as price
	from products
	union
	select	product_id
	,		'store3' as store
	,		store3 as price
	from products
)temp
where price is not null
```

- **해설 :** store1부터 3까지 하드코딩으로 들어가야 하기 때문에 union을 사용해 한줄 한줄 붙여주었습니다. 그리고 가격이 NULL인것을 제외하기 위해 본 쿼리를 서브쿼리로 만들어 WHERE price is not null 코드로 제약을 주었습니다.
