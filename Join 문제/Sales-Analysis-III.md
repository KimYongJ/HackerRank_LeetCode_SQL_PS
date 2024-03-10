# **Sales-Analysis-III**

- [https://leetcode.com/problems/sales-analysis-iii/](https://leetcode.com/problems/sales-analysis-iii/)
- **문제 :** 2019년 1분기(1월 1일부터 3월 31일까지)에만 판매된 제품들을 찾는 것입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Product (
  product_id INT,
  product_name VARCHAR(255),
  unit_price INT
);
CREATE TABLE Sales (
  seller_id INT,
  product_id INT,
  buyer_id INT,
  sale_date DATE,
  quantity INT,
  price INT
);
INSERT INTO Product (product_id, product_name, unit_price) VALUES
(1, 'S8', 1000),
(2, 'G4', 800),
(3, 'iPhone', 1400);
INSERT INTO Sales (seller_id, product_id, buyer_id, sale_date, quantity, price) VALUES
(1, 1, 2, '2019-01-21', 1, 800),
(1, 2, 2, '2019-02-17', 2, 2000),
(2, 2, 3, '2019-06-02', 1, 800),
(3, 3, 4, '2019-05-13', 2, 2800);
```

```jsx
[ 정답 ]
SELECT	PD.PRODUCT_ID
,		PD.PRODUCT_NAME
FROM PRODUCT PD
INNER JOIN SALES SL ON SL.PRODUCT_ID	=	PD.product_id
GROUP BY PD.PRODUCT_ID, PD.product_name
HAVING MIN(SL.SALE_DATE) >= '2019-01-01'
AND MAX(SL.SALE_DATE) <= '2019-03-31'
```

- **해설 :** 여러개의 PRODUCT_ID가 있을 수 있는데 중복을 제거해야 하기 때문에 PRODUCT_ID와 PRODUCT_NAME을 기준으로 그룹을 묶은 후 그룹에 대한 조건(WHERE)을 주기위해 HAVING 키워드를 사용했습니다. 이 때 날짜 컬럼(SL.SALES_DATE)에 대해 HAVING절에 들어갈 수 있게 하려면 집계함수(MIN, MAX)를 사용해야 합니다.
