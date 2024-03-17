# **Market-Analysis-I**

- [https://leetcode.com/problems/market-analysis-i/](https://leetcode.com/problems/market-analysis-i/)
- **문제 :** 각 사용자에 대해 가입 날짜와 2019년에 구매한 주문의 수를 찾는 SQL 쿼리를 작성해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Users (
    user_id INT,
    join_date DATE,
    favorite_brand VARCHAR(255)
);
CREATE TABLE Orders (
    order_id INT,
    order_date DATE,
    item_id INT,
    buyer_id INT,
    seller_id INT
);
INSERT INTO Users (user_id, join_date, favorite_brand) VALUES
(1, '2018-01-01', 'Lenovo'),
(2, '2018-02-09', 'Samsung'),
(3, '2018-01-19', 'LG'),
(4, '2018-05-21', 'HP');
INSERT INTO Orders (order_id, order_date, item_id, buyer_id, seller_id) VALUES
(1, '2019-08-01', 4,1,2),
(2, '2018-08-02', 2,1,3),
(3, '2019-08-03', 3,2,3),
(4, '2018-08-04', 1,4,2),
(5, '2018-08-04', 1,3,4),
(6, '2019-08-05', 2,2,4);
```

```jsx
[ 정답 ]
SELECT	U.USER_ID AS BUYER_ID
,		U.JOIN_DATE
,		COALESCE(T.ORDERS_IN_2019,0) ORDERS_IN_2019
FROM USERS U
LEFT OUTER JOIN (
		SELECT	BUYER_ID
		,		COUNT(*) ORDERS_IN_2019
		FROM ORDERS
		WHERE DATE_FORMAT(ORDER_DATE,'%Y') = '2019'
		GROUP BY BUYER_ID
)T ON U.USER_ID = T.BUYER_ID
```

- **해설**
  - USERS 테이블의 정보는 모두 출력되어야 하기 때문에 메인은 USERS 테이블로 진행합니다. 그 후 LEFT JOIN을 통해 2019년의 주문수를 가져옵니다.
  - 서브쿼리에서 WHERE 조건에 2019년에 주문한 행을 걸러낸 후 구매자 아이디 기준으로 그룹을 묶었습니다.
