- **Duplicate-Emails**

  - [https://leetcode.com/problems/duplicate-emails/](https://leetcode.com/problems/duplicate-emails/)
  - **문제 :** PERSON 테이블에서 이메일이 중복되어 2개 이상인 경우의 이메일을 출력하시오. 단 이메일은 NULL이 아닌 것들만 출력합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Person (
      id INT PRIMARY KEY,
      email VARCHAR(255) NOT NULL
  );

  INSERT INTO Person (id, email) VALUES
  (1, 'a@b.com'),
  (2, 'c@d.com'),
  (3, 'a@b.com');
  ```

  ```jsx
  [ 정답 ]
  SELECT EMAIL
  FROM PERSON
  GROUP BY EMAIL
  HAVING COUNT(*) > 1
  ```

  - **해설 :** EMAIL을 기준으로 그룹으로 묶어 HAVING절에서 개수를 헤아려 1보다 크면 출력합니다.
