# **Product-Sales-Analysis-I**

- [https://leetcode.com/problems/product-sales-analysis-i/](https://leetcode.com/problems/product-sales-analysis-i/)
- **문제 :** 두 테이블을 조인하여 제품명과, Year, Price를 출력하는 문제입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Product (
  product_id INT,
  product_name VARCHAR(255)
);
CREATE TABLE Sales (
  sale_id INT,
  product_id INT,
  year INT,
  quantity INT,
  price INT
);
INSERT INTO Product (product_id, product_name) VALUES
(100, 'Nokia'),
(200, 'Apple'),
(300, 'Samsung');
INSERT INTO Sales (sale_id, product_id, year, quantity, price) VALUES
(1, 100, 2008, 10, 5000),
(2, 100, 2009, 12, 5000),
(7, 200, 2011, 15, 9000);
```

```jsx
[ 정답 ]
SELECT  PD.PRODUCT_NAME
,       SL.YEAR
,       SL.PRICE
FROM SALES SL
LEFT OUTER JOIN PRODUCT PD
    ON PD.PRODUCT_ID = SL.PRODUCT_ID
```
