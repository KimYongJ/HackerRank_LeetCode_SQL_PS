# **Customer-Who-Visited-but-Did-Not-Make-Any-Transactions**

- [https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)
- **문제 :** 방문은 했지만 어떤 거래도 하지 않은 고객의 ID와 이러한 유형의 방문을 한 횟수를 찾아내 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Visits (
  visit_id INT,
  customer_id INT
);
CREATE TABLE Transactions (
  transaction_id INT,
  visit_id INT,
  amount INT
);
INSERT INTO Visits (visit_id, customer_id) VALUES
(1, 23),
(2, 9),
(4, 30),
(5, 54),
(6, 96),
(7, 54),
(8, 54);
INSERT INTO Transactions (transaction_id, visit_id, amount) VALUES
(2, 5, 310),
(3, 5, 300),
(9, 5, 200),
(12, 1, 910),
(13, 2, 970);
```

```jsx
[ 정답(1) ]
SELECT	CUSTOMER_ID
,		COUNT(CUSTOMER_ID) COUNT_NO_TRANS
FROM VISITS
WHERE VISIT_ID NOT IN(
						SELECT VISIT_ID
						FROM TRANSACTIONS
)
GROUP BY CUSTOMER_ID

[ 정답(2) ]
SELECT	CUSTOMER_ID
,		COUNT(CUSTOMER_ID) COUNT_NO_TRANS
FROM VISITS v
WHERE not exists(
						SELECT 1
						FROM TRANSACTIONS t
						where t.VISIT_ID = v.visit_id
)
GROUP BY CUSTOMER_ID
```

- **해설 :** 두 가지 방법으로 문제를 풀었습니다. 문제의 요구 사항이 작업 테이블에 있는 값을 제거한 visits 테이블을 출력하는 것이기 때문에 정답(1)에서는 not in으로 간단히 풀어보았습니다. 정답(2)에서는 not exists 키워드를 사용해 서브 쿼리에 있지 않을 때 출력되도록 하였습니다.
