# **Triangle-Judgement**

- [https://leetcode.com/problems/triangle-judgement/](https://leetcode.com/problems/triangle-judgement/)
- **문제 :** Triangle 테이블에서 삼격형인 조건일 경우 Yes를, 아닌 경우 No를 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Triangle (
  x INT,
  y INT,
  z INT,
  PRIMARY KEY (x, y, z)
);

INSERT INTO Triangle (x, y, z) VALUES
(13, 15, 30),
(10, 20, 15);
```

```jsx
[ 정답 ]
SELECT X, Y, Z,
CASE WHEN X+Y>Z AND X+Z>Y AND Z+Y>X THEN 'YES' ELSE 'NO' END TRIANGLE
FROM TRIANGLE
```

- **해설 :** 삼각형의 조건은 나머지 두변의 합이 다른 변보다 항상 크기 때문에 case when 구문을 사용해 여러 조건에 대해 and를 하여 탐색합니다.
