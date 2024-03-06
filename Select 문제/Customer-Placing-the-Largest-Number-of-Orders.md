- **Customer-Placing-the-Largest-Number-of-Orders**

  - [https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/)
  - **문제 :** Orders 테이블에서 가장 많은 order_number를 갖는 customer_number를 출력하는 문제 입니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Orders (
      order_number INT ,
      customer_number INT
  );

  INSERT INTO Orders (order_number, customer_number) VALUES (8,6);
  INSERT INTO Orders (order_number, customer_number) VALUES (9,2);
  INSERT INTO Orders (order_number, customer_number) VALUES (10,4);
  INSERT INTO Orders (order_number, customer_number) VALUES (11,16);
  INSERT INTO Orders (order_number, customer_number) VALUES (12,3);
  INSERT INTO Orders (order_number, customer_number) VALUES (13,5);
  INSERT INTO Orders (order_number, customer_number) VALUES (14,3);
  INSERT INTO Orders (order_number, customer_number) VALUES (15,16);
  ```

  ```jsx
  [ 정답 ]
  SELECT CUSTOMER_NUMBER
  FROM ORDERS
  GROUP BY CUSTOMER_NUMBER
  ORDER BY COUNT(*) DESC
  LIMIT 1
  ```

  - **해설 :** CUSTOMER_NUMBER 컬럼을 기준으로 그룹을 지은 후 count 결과로 내림차순 정렬합니다. 한줄만 출력하기 때문에 limit 키워드를 사용합니다.
