# **Count-Salary-Categories**

- [https://leetcode.com/problems/count-salary-categories/](https://leetcode.com/problems/count-salary-categories/)
- **문제 :** 계좌 테이블에서 각 계좌에 대해 다음의 3가지로 분류하여 출력합니다.
  - 'Low Salary': 월 수입이 $20,000 미만인 계좌.
  - 'Average Salary': 월 수입이 $20,000 이상이고 $50,000 이하인 계좌.
  - 'High Salary': 월 수입이 $50,000 초과인 계좌.

```jsx
[ 문제 조건 ]
CREATE TABLE Accounts (
    account_id INT PRIMARY KEY,
    income INT
);
INSERT INTO Accounts (account_id, income) VALUES
(3, 108939),
(2, 12747),
(8, 87790),
(6, 97196);
```

```jsx
[ 정답 ]
SELECT  'Low Salary' as category
,		count(*) as accounts_count
from Accounts
where income < 20000

UNION

SELECT  'Average Salary' as category
,		count(*) as accounts_count
from Accounts
where income >= 20000
AND income <= 50000

UNION

SELECT  'High Salary' as category
,		count(*) as accounts_count
from Accounts
where income > 50000
```

- **해설 :** 각각의 조회 쿼리를 만들어 마지막에 union으로 합치는 방식을 선택했습니다. 각 조건마다 급여 형태를 하드 코딩하고, where절에 제한을 두어 급여 형태에 맞는 값만 출력 되도록하고 합쳐서 출력되도록했습니다. 이 때, count 집계 함수를 사용했는데 group by절은 생략해도 무방합니다. 집계함수 하나만 쓰일 때는 생략이 가능합니다. ('High Salary' as category 는 하드 코딩이기 때문에 그룹 연산에 영향을 미치지 않기 때문)
