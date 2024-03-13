# **Recyclable-and-Low-Fat-Products**

- [https://leetcode.com/problems/recyclable-and-low-fat-products/](https://leetcode.com/problems/recyclable-and-low-fat-products/)
- **문제 :** 저지방(low fat)이면서 재활용 가능한(recyclable) 제품의 ID를 찾는 것입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Products (
    product_id int,
    low_fats enum('Y', 'N'),
    recyclable enum('Y', 'N'),
    PRIMARY KEY (product_id)
);
INSERT INTO Products (product_id, low_fats, recyclable) VALUES
(1, 'Y', 'Y'),
(2, 'N', 'Y'),
(3, 'Y', 'Y'),
(4, 'N', 'N');
```

```jsx
[ 정답 ]
SELECT  PRODUCT_ID
FROM PRODUCTS
WHERE LOW_FATS = 'Y' AND RECYCLABLE = 'Y'
```

- **해설 :** 저지방 컬럼 값이 Y이면서 재활용 가능 컬럼의 값이 Y인 것을 찾아 줍니다.
