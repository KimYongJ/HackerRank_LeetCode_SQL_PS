- symmetric-pairs

  - [https://www.hackerrank.com/challenges/symmetric-pairs/problem?isFullScreen=true](https://www.hackerrank.com/challenges/symmetric-pairs/problem?isFullScreen=true)

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Functions (
      X INT,
      Y INT
  );

  INSERT INTO Functions (X, Y) VALUES
  (20, 20),
  (20, 20),
  (20, 21),
  (23, 22),
  (22, 23),
  (21, 20);
  ```

  - **문제 :** 대칭쌍을 출력합니다. 두 쌍 (X1, Y1)과 (X2, Y2)가 대칭 쌍이라고 하는 경우는 X1 = Y2이고 X2 = Y1일 때입니다. 출력은 x의 값에 따라 오름차순으로 모든 대칭쌍을 출력하는 쿼리를 출력합니다. 쌍을 출력할 때는 X1≤Y1이 되도록 합니다.

  ```jsx
  [ 정답 ]
  SELECT F1.X, F1.Y
  FROM FUNCTIONS F1
  INNER JOIN FUNCTIONS F2
      ON F1.X = F2.Y
      AND F1.Y = F2.X
  GROUP BY F1.X, F1.Y
  HAVING COUNT(1) > 1 OR F1.X<F1.Y
  ORDER BY F1.X
  ```

  - **해설 :** inner join 으로 두 테이블의 대칭 쌍인 것을 조인합니다. 그 후 GROUP BY 절로 압축한 후 HAVING 절을 사용해서 20 20 과 같이 같은 값일 경우 출력되도록 COUNT(1) > 1 구문을 걸어주고, 문제 조건에서 출력될 때 X < Y 조건이 있으니 해당 구문도 OR절로 묶어 걸어줍니다. 그리고 X를 기준으로 오름차순 출력이기 때문에 ORDER BY도 진행해 줍니다.
