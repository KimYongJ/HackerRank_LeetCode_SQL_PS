- **Find-Customer-Referee**

  - [https://leetcode.com/problems/find-customer-referee/](https://leetcode.com/problems/find-customer-referee/)
  - **문제 :** 고객 테이블(Customer table)에서 특정 고객(id = 2)에 의해 추천되지 않은(refereed) 모든 고객의 이름을 찾는 것입니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Customer (
      id int,
      name varchar(100),
      referee_id int
  );

  INSERT INTO Customer (id, name, referee_id) VALUES
  (1, 'Will', NULL),
  (2, 'Jane', NULL),
  (3, 'Alex', 2),
  (4, 'Bill', NULL),
  (5, 'Zack', 1),
  (6, 'Mark', 2);
  ```

  ```jsx
  [ 정답 ]
  SELECT NAME
  FROM CUSTOMER C1
  WHERE C1.referee_id != 2
  OR C1.referee_id IS NULL
  ```
