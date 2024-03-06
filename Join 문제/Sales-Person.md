- **Sales Person**
  - [https://leetcode.com/problems/sales-person/](https://leetcode.com/problems/sales-person/)
  - **문제 :** "RED"라는 이름의 회사와 관련된 주문이 없는 모든 판매자의 이름을 찾아 출력하는 문제 입니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Salesperson (
      sales_id INT,
      name VARCHAR(255),
      salary INT,
      commission_rate INT,
      hire_date DATE
  );

  CREATE TABLE Company (
      com_id INT,
      name VARCHAR(255),
      city VARCHAR(255)
  );

  CREATE TABLE Orders (
      order_id INT,
      order_date DATE,
      com_id INT,
      sales_id INT,
      amount DECIMAL(10, 2)
  );

  INSERT INTO SalesPerson (sales_id, name, salary, commission_rate, hire_date) VALUES
  (1, 'John', 100000, 6, '2006-04-01'),
  (2, 'Amy', 12000, 5, '2010-05-01'),
  (3, 'Mark', 65000, 12, '2008-12-25'),
  (4, 'Pam', 25000, 25, '2005-01-01'),
  (5, 'Alex', 5000, 10, '2007-02-03');

  INSERT INTO Company (com_id, name, city) VALUES
  (1, 'RED', 'Boston'),
  (2, 'ORANGE', 'New York'),
  (3, 'YELLOW', 'Boston'),
  (4, 'GREEN', 'Austin');

  INSERT INTO Orders (order_id, order_date, com_id, sales_id, amount) VALUES
  (1, '2014-01-01', 3, 4, 10000),
  (2, '2014-02-01', 4, 5, 5000),
  (3, '2014-03-01', 1, 1, 50000),
  (4, '2014-04-01', 1, 4, 25000);
  ```
  ```jsx
  [ 정답(1) ]
  SELECT SP.NAME
  FROM SALESPERSON SP
  WHERE SP.SALES_ID NOT IN
  (
  		SELECT OD.SALES_ID
  		FROM orders OD
  		LEFT OUTER JOIN COMPANY CMP ON CMP.COM_ID = OD.COM_ID
  		WHERE CMP.NAME = 'RED'
  )

  [ 정답(2) ]
  SELECT SP.NAME
  FROM SALESPERSON SP
  WHERE NOT EXISTS
  (
  		SELECT OD.SALES_ID
  		FROM orders OD
  		LEFT OUTER JOIN COMPANY CMP ON CMP.COM_ID = OD.COM_ID
  		WHERE CMP.NAME = 'RED'
  		AND OD.SALES_ID = SP.SALES_ID
  )
  ```
  - **정답(1) 해설 :** Orders 테이블과 Company 테이블을 조인하여 Company 테이블의 Name이 RED인 것만 뽑아내어 NOT IN 키워드를 사용해 SALES_ID가 포함되지 않으면 출력해주었습니다.
  - **정답(2) 해설 :** 정답(1)과 동일하며 NOT EXISTS 키워드를 쓴것만 다릅니다. NOT EXISTS를 사용하기 위해 서브쿼리에 다음과 같은 조건을 추가해 포함되는 것들이 아닐 때 출력되도록하였습니다. 조건 : AND OD.SALES_ID = SP.SALES_ID
