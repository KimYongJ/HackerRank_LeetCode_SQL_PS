# **Monthly-Transactions-I**

- [https://leetcode.com/problems/monthly-transactions-i/](https://leetcode.com/problems/monthly-transactions-i/)
- **문제 :** 각 국가별, 월별로 거래 건수와 총액, 승인된 거래 건수와 그 총액을 찾는 SQL 쿼리를 작성해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Transactions (
    id int,
    country varchar(2),
    state enum('approved', 'declined'),
    amount int,
    trans_date date
);
INSERT INTO Transactions (id, country, state, amount, trans_date) VALUES
(121, 'US', 'approved', 1000, '2018-12-18'),
(122, 'US', 'declined', 2000, '2018-12-19'),
(123, 'US', 'approved', 2000, '2019-01-01'),
(124, 'DE', 'approved', 2000, '2019-01-07');
```

```jsx
[ 정답 ]
SELECT	DATE_FORMAT(TRANS_DATE, '%Y-%m') MONTH
,		COUNTRY
,		COUNT(*) AS TRANS_COUNT
,		COUNT(CASE WHEN STATE='approved'THEN 1 ELSE NULL END) AS APPROVED_COUNT
,		SUM(AMOUNT) AS TRANS_TOTAL_AMOUNT
,		SUM(CASE WHEN STATE='approved' THEN AMOUNT ELSE 0 END) AS APPROVED_TOTAL_AMOUNT
FROM transactions
GROUP BY COUNTRY, DATE_FORMAT(TRANS_DATE, '%Y-%m')
```

- **해설 :** 이 문제는 나라별, 월별로 그룹을 지어준 후 집계함수를 이용해 출력만 해주면됩니다.
  - **APPROVED_COUNT 컬럼 :** 이 컬럼을 구할 때 집계함수 안에 CASE WHEN 구문을 적었습니다. COUNT 집계 함수는 값이 NULL이 아닌 경우 카운팅 합니다. 그렇기 때문에 STATE 컬럼이 ‘approved’일 때만 숫자를 반환하고, 아닌 경우 null을 반환하였습니다.
  - **APPROVED_TOTAL_AMOUNT 컬럼 :** 이 컬럼을 구할 때도 집계함수 안에 CASE WHEN 구문을 넣었습니다. STATE 값이 ‘approved’일 때는 amount 값을, 아닌 경우 0을 더하도록 하여 값을 구했습니다.
