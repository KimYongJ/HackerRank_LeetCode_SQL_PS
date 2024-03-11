# **Average-Selling-Price**

- [https://leetcode.com/problems/average-selling-price/](https://leetcode.com/problems/average-selling-price/)
- **문제 :** 날짜에 따른 제품의 총 판매 가격을 판매된 제품 총 수로 나누어 평균 판매가격을 구하는 것입니다. 출력은 소수 3번째 자리에서 반올림하여 소수점 2자리 까지 출력합니다. 이때 값이 NULL이면 0.00 을 출력해주어야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Prices (
  product_id INT,
  start_date DATE,
  end_date DATE,
  price DECIMAL(10, 2)
);
CREATE TABLE UnitsSold (
  product_id INT,
  purchase_date DATE,
  units INT
);

-- //////////////////////////  TYPE 1
INSERT INTO Prices (product_id, start_date, end_date, price) VALUES
(1, '2019-02-17', '2019-02-28', 5),
(1, '2019-03-01', '2019-03-22', 20),
(2, '2019-02-01', '2019-02-20', 15),
(2, '2019-02-21', '2019-03-31', 30),
(3, '2019-02-21', '2019-03-31', 30);
INSERT INTO UnitsSold (product_id, purchase_date, units) VALUES
(1, '2019-02-25', 100),
(1, '2019-03-01', 15),
(2, '2019-02-10', 200),
(2, '2019-03-22', 30);
-- ///////////////////////////// TYPE 2
INSERT INTO Prices (product_id, start_date, end_date, price) VALUES
(1, '2019-01-17', '2019-01-25', 18),
(1, '2019-01-26', '2019-02-12', 5),
(2, '2019-01-23', '2019-01-30', 3),
(2, '2019-01-31', '2019-02-12', 18);
INSERT INTO UnitsSold (product_id, purchase_date, units) VALUES
(1, '2019-01-17', 5),
(1, '2019-01-31', 4),
(2, '2019-01-29', 1),
(2, '2019-01-29', 2);
```

```jsx
[ 정답 ]
SELECT	PR.PRODUCT_ID
,		COALESCE(ROUND(SUM(PR.PRICE * US.UNITS) / SUM(US.UNITS) ,2),0.00) AS AVERAGE_PRICE
FROM PRICES PR
LEFT OUTER JOIN UNITSSOLD US
		ON PR.START_DATE <= US.PURCHASE_DATE
		AND PR.END_DATE	>= US.PURCHASE_DATE
		AND PR.PRODUCT_ID = US.PRODUCT_ID
GROUP BY PR.PRODUCT_ID
```

- **해설 :** PR 테이블 기준으로 US 테이블을 조인합니다. LEFT OUTER JOIN으로 해야 합니다.(ㅣLEFT도 상관없음) INNER JOIN을 하게 되면 PR 테이블이 온전히 출력되지 않기 때문입니다. 조인 조건은 날짜와 제품 아이디를 기준으로 BETWEEN을 사용해도 되고, 부등호를 사용해서 조인해도 됩니다. 그 후 제품 아이디를 기준으로 그룹을 묶어 주며 해당 날짜의 가격과 판매 제품을 곱한 후 판매 제품의 합을 나눠줍니다. 여기 중요한게 NULL인경우 0.00 을 출력해야 하기 때문에 결과에 COALESCE 함수를 사용해 NULL인 경우 0.00을 출력하도록 합니다.
