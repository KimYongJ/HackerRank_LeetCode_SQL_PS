# **Customers-Who-Bought-All-Products**

- [https://leetcode.com/problems/customers-who-bought-all-products/](https://leetcode.com/problems/customers-who-bought-all-products/)
- **문제 :** Product 테이블에 있는 모든 제품을 구매한 CUSTOMER_ID를 찾는 것입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Product (
  product_key INT PRIMARY KEY
);
CREATE TABLE Customer (
  customer_id INT,
  product_key INT,
  FOREIGN KEY (product_key) REFERENCES Product(product_key)
);
INSERT INTO Product (product_key) VALUES (5), (6);
INSERT INTO Customer (customer_id, product_key) VALUES
(1, 5), (2, 6),(3, 5),(3, 6),(1, 6);
```

```jsx
[ 정답 ]
SELECT	CUSTOMER_ID
FROM CUSTOMER
GROUP BY CUSTOMER_ID
HAVING COUNT(DISTINCT PRODUCT_KEY) = (SELECT COUNT(*) FROM PRODUCT)
```

- **해설 :** 이 문제는 고객 별로 그룹을 나눠 고객이 PRODUCT 테이블에 있는 모든 RODUCT_KEY를 주문했을 때 CUSTOMER_ID를 출력해야 합니다. 이를 위해 PRODUCT 테이블의 PRODUCT_KEY 개수와 CUSTOMER 테이블에 고객별로 갖고있는 PRODUCT_KEY를 카운팅하여 문제를 해결합니다. 한 고객이 같은 제품을 여러번 구매했을 수도 있기 때문에 CUSTOMER 테이블의 PRODUCT_KEY를 카운팅 할 때는 DISTINCT 키워드를 사용해 카운팅합니다. 집계 함수 안에 DISTINCT 키워드가 들어갈 경우 그룹에서 같은 값은 삭제되어 하나의 값만 카운팅 됩니다.
