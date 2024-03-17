# **Group-Sold-Products-By-The-Date**

- [https://leetcode.com/problems/group-sold-products-by-the-date/](https://leetcode.com/problems/group-sold-products-by-the-date/)
- **문제 :** **Activities** 테이블에는 제품이 판매된 날짜(**sell_date**)와 제품 이름(**product**)이 기록되어 있습니다. 이 테이블은 중복된 행을 포함할 수 있으며, 기본 키가 없습니다. 각 행은 시장에서 특정 날짜에 판매된 제품의 이름과 그 날짜를 나타냅니다. 날짜별로 판매된 서로 다른 제품의 개수와 그 제품들의 이름을 출력하는 문제입니다. 판매된 제품 이름은 사전식 순서(lexicographically)로 정렬되어야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Activities (
  sell_date DATE,
  product VARCHAR(255)
);
INSERT INTO Activities (sell_date, product) VALUES
('2020-05-30', 'Headphone'),
('2020-06-01', 'Pencil'),
('2020-06-02', 'Mask'),
('2020-05-30', 'Basketball'),
('2020-06-01', 'Bible'),
('2020-06-02', 'Mask'),
('2020-05-30', 'T-shirt');
```

```jsx
[ 정답 ]
SELECT  SELL_DATE
,       COUNT(DISTINCT PRODUCT) AS NUM_SOLD
,       GROUP_CONCAT(DISTINCT PRODUCT ORDER BY PRODUCT) PRODUCTS
FROM ACTIVITIES
GROUP BY SELL_DATE
```

- **해설 :** 날짜 별로 집계를 해야하기 때문에 SELL_DATE기준으로 GROUP을 묶습니다. 그 후 COUNT함수 안에 개수를 세야할 품목(PRODUCT)를 넣습니다. 이 때 중복되는 품목은 제거해야 하기 때문에 DISTINCT 키워드를 넣어야 합니다. 이 키워드가 들어가서 중복된 품목명은 제거됩니다. 또한 집계되는 품목명에 대해 가로로 붙일 때 GROUP_CONCAT 함수를 사용합니다. 이 때도 품목명의 중복 제거를위해 DISTINCT 키워드를 사용하며, 사전순으로 출력해야 하기 때문에 ORDER BY 도 같이 적어줍니다.
- **GROUP_CONCAT :** MySQL에서 제공하는 집계 함수로, 선택된 열의 값들을 하나의 문자열로 연결할 때 사용됩니다.
  - **특징**
    1. 연결시 콤마(,)로 구분해 연결합니다.
    2. 기본 구분자인 콤마(,) 대신 다른 문자 구분을 원하면 SEPARATOR 옵션을 사용하면 됩니다. EX) SELECT GROUP_CONCAT(원하는컬럼 SEPARATOR '; ') FROM …
    3. 함수 내에서 ORDER BY 절을 사용해 값들을 특정 순서로 정렬할 수 있습니다.
    4. 함수 내에서 DISTINCT 키워드를 통해 중복 제거가 가능합니다.
