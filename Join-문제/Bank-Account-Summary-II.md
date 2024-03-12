# **Bank-Account-Summary-II**

- [https://leetcode.com/problems/bank-account-summary-ii/](https://leetcode.com/problems/bank-account-summary-ii/)
- **문제 :** 잔액이 10,000보다 큰 사람의 이름과 잔액을 출력하는 문제입니다. 입출금 내역은 Transactions 테이블에 있습니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Users (
    account INT,
    name VARCHAR(100)
);
CREATE TABLE Transactions (
    trans_id INT,
    account INT,
    amount INT,
    transacted_on DATE
);
INSERT INTO Users (account, name) VALUES
(90001, 'Alice'),
(90002, 'Bob'),
(90003, 'Charlie');
INSERT INTO Transactions (trans_id, account, amount, transacted_on) VALUES
(1, 90001, 7000, '2020-08-01'),
(2, 90001, 7000, '2020-09-01'),
(3, 90001, -3000, '2020-09-02'),
(4, 90002, 1000, '2020-09-02'),
(5, 90003, 6000, '2020-08-07'),
(6, 90003, 6000, '2020-08-07'),
(7, 90003, -4000, '2020-09-11');
```

```jsx
[ 정답 ]
SELECT  U.NAME
,       SUM(T.AMOUNT) BALANCE
FROM USERS U
LEFT OUTER JOIN TRANSACTIONS T
    ON T.ACCOUNT = U.ACCOUNT
GROUP BY U.NAME
HAVING BALANCE>10000
```

- **해설 :** 두 테이블은 조인한 후 users의 이름을 기준으로 그룹을 묶어주고, sum 함수로 합계를 구합니다. 그 후 having 키워드로 집계함수에 조건을 걸어 잔액이 만원 초과인 사람을 조회합니다.
