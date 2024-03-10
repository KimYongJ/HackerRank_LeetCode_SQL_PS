# **List-the-Products-Ordered-in-a-Period**

- [https://leetcode.com/problems/list-the-products-ordered-in-a-period/](https://leetcode.com/problems/list-the-products-ordered-in-a-period/)
- **문제 :** 2020년 2월에 적어도 100개 이상 주문된 제품의 이름과 그 수량을 구하는 문제 입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Products (
  product_id INT,
  product_name VARCHAR(255),
  product_category VARCHAR(255)
);
CREATE TABLE Orders (
  product_id INT,
  order_date DATE,
  unit INT
);
INSERT INTO Products (product_id, product_name, product_category) VALUES
(1, 'Leetcode Solutions', 'Book'),
(2, 'Jewels of Stringology', 'Book'),
(3, 'HP', 'Laptop'),
(4, 'Lenovo', 'Laptop'),
(5, 'Leetcode Kit', 'T-shirt');
INSERT INTO Orders (product_id, order_date, unit) VALUES
(1, '2020-02-05', 60),
(1, '2020-02-10', 70),
(2, '2020-01-18', 30),
(2, '2020-02-11', 80),
(3, '2020-02-17', 2),
(3, '2020-02-24', 3),
(4, '2020-03-01', 20),
(4, '2020-03-04', 30),
(4, '2020-03-05', 60),
(5, '2020-02-25', 50),
(5, '2020-02-27', 50),
(5, '2020-03-01', 50);
```

```jsx
[ 정답 ]
SELECT PD.PRODUCT_NAME
,       SUM(OD.UNIT) AS UNIT
FROM ORDERS OD
INNER JOIN PRODUCTS PD ON PD.PRODUCT_ID = OD.PRODUCT_ID
WHERE DATE_FORMAT(ORDER_DATE,'%Y-%m') = '2020-02'
GROUP BY PD.PRODUCT_NAME
HAVING SUM(OD.UNIT) >= 100
```

- **해설 :** ORDERS 테이블과 PRODUCTS테이블을 조인한 후 제품명을 기준으로 그룹화 하고, HAVING절에 합계가 100개 이상인 것만 조회되도록 조건을 걸어줍니다. 또한 2020년 2월이라고 하였으므로 WHERE 조건에 ORDER_DATE 컬럼값을 2020-02와 같은 포멧으로 변경 한 후 해당 데이터만 조회되도록 합니다.
  - **DATE_FORMAT :** MySQL에서 날짜 및 시간 값을 원하는 형식의 문자열로 변환하는데 사용됩니다. 이 함수는 다양한 형식 지정자를 사용하여 날짜의 특정 부분을 추출하거나 표시 형식을 변경할 수 있습니다.
    - **형식 :** DATE_FORMAT(date, format)
    - **인자 순서 :** (변환하려는 날짜 or 시간값) , (결과로 반환되어야 하는 형식 지정 문자)
    - **형식 지정자 예시**
      - **`%Y`**: 4자리 연도 (예: 2021)
      - **`%y`**: 2자리 연도 (예: 21)
      - **`%m`**: 월을 두 자리 숫자로 (예: 01 ~ 12)
      - **`%d`**: 일을 두 자리 숫자로 (예: 01 ~ 31)
      - **`%H`**: 시간을 24시간 형식의 두 자리 숫자로 (00 ~ 23)
      - **`%i`**: 분을 두 자리 숫자로 (00 ~ 59)
      - **`%s`**: 초를 두 자리 숫자로 (00 ~ 59)
