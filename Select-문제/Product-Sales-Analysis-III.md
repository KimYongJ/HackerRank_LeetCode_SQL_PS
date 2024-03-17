# **Product-Sales-Analysis-III**

- [https://leetcode.com/problems/product-sales-analysis-iii/](https://leetcode.com/problems/product-sales-analysis-iii/)
- **문제 :** 각 제품의 첫 해 판매에 대한 정보를 추출하는 것입니다. 여기에는 제품 ID, 첫 해, 판매된 수량, 가격이 포함됩니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Sales (
    sale_id INT,
    product_id INT,
    year INT,
    quantity INT,
    price INT
);
CREATE TABLE Product (
    product_id INT,
    product_name VARCHAR(255)
);
INSERT INTO Sales (sale_id, product_id, year, quantity, price) VALUES
(1, 100, 2008, 10, 5000),
(2, 100, 2009, 12, 5000),
(7, 200, 2011, 15, 9000);
INSERT INTO Product (product_id, product_name) VALUES
(100, 'Nokia'),
(200, 'Apple'),
(300, 'Samsung');
```

```jsx
[ 정답 ]
SELECT	product_id
,		YEAR first_year
,		quantity
,		price
FROM SALES
WHERE (product_id, YEAR) IN(
		SELECT	product_id
		,		MIN(YEAR) AS YEAR
		FROM SALES
		GROUP BY product_id
)
```

- **해설**
  - IN절 서브 쿼리에서 제품ID 기준으로 그룹을 묶고 가장 빠른 YEAR를 찾습니다. 그 후 SALES의 전체 행에서 서브 쿼리에서 추출한 정보랑 같은 행만 출력해주면 됩니다.
