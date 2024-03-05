- **Customers-Who-Never-Order**

  - [https://leetcode.com/problems/customers-who-never-order/](https://leetcode.com/problems/customers-who-never-order/)
  - **문제 :** Customers 테이블에서 주문을 한번도 하지 않은 고객의 NAME컬럼을 출력하는데 컬럼명은 Customers로 출력합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Customers (
      id INT PRIMARY KEY,
      name VARCHAR(255)
  );

  CREATE TABLE Orders (
      id INT PRIMARY KEY,
      customerId INT
  );

  -- 예시 데이터 삽입
  INSERT INTO Customers (id, name) VALUES
  (1, 'Joe'),
  (2, 'Henry'),
  (3, 'Sam'),
  (4, 'Max');

  INSERT INTO Orders (id, customerId) VALUES
  (1, 3),
  (2, 1);
  ```

  ```jsx
  [ 정답(1) ]
  SELECT NAME AS Customers
  FROM CUSTOMERS CT
  WHERE NOT EXISTS (
  					SELECT 1
  					FROM ORDERS OD
  					WHERE OD.CUSTOMERID = CT.ID
  				)

  [ 정답(2) ]
  SELECT NAME AS Customers
  FROM CUSTOMERS CT
  WHERE ID NOT IN (
  					SELECT CUSTOMERID
  					FROM ORDERS
  				)

  [ 정답(3) ]
  SELECT NAME AS Customers
  FROM CUSTOMERS CT
  LEFT OUTER JOIN ORDERS OD
      ON OD.CUSTOMERID = CT.ID
  WHERE OD.ID IS NULL

  ```

  - **해설 :** Customers 테이블에 id가 orders 테이블에 없는 것만 출력하면 되는 문제이기 때문에 not exists와 not in등의 키워드를 사용했습니다. 또한 조인을 통해서도 풀 수 있기에 3가지 방법으로 풀어봤습니다.
    - 특히 not exists를 사용할 때는 서브쿼리 안에서 외부 쿼리(CUSTOMERS테이블)의 컬럼과 내부 쿼리(ORDERS 테이블)의 컬럼을 비교해야 하기 때문에 서브 쿼리 안에 외부 쿼리의 컬럼명을 적어줍니다.
