# **Top-Travellers**

- [https://leetcode.com/problems/top-travellers/](https://leetcode.com/problems/top-travellers/)
- **문제 :** 사용자와 그들이 여행한 거리를 기록하는 **Users** 테이블과 **Rides** 테이블을 사용하여 각 사용자가 여행한 총 거리를 출력합니다. 출력은 거리 기준으로 내림차순으로 정렬하고 거리가 같다면 이름순으로 오름차순 정렬 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Users (
  id INT,
  name VARCHAR(255)
);
CREATE TABLE Rides (
  id INT,
  user_id INT,
  distance INT
);
INSERT INTO Users (id, name) VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Alex'),
(19, 'Alice');
INSERT INTO Rides (id, user_id, distance) VALUES
(1, 1, 120),
(2, 2, 317),
(3, 3, 222),
(4, 7, 100),
(5, 13, 312),
(9, 7, 230);
```

```jsx
[ 정답 ]
SELECT  US.NAME
,       SUM(COALESCE(RD.DISTANCE,0)) AS TRAVELLED_DISTANCE
FROM USERS US
LEFT OUTER JOIN RIDES RD
    ON RD.USER_ID = US.ID
GROUP BY US.ID, US.NAME
ORDER BY TRAVELLED_DISTANCE DESC, US.NAME
```

- **해설 :** 기준을 USERS 테이블로 잡은 후 RIDES 테이블을 OUTER JOIN하여 USERS 테이블이 전부 다 출력 되도록 합니다. 그리고 거리의 합을 위해 그룹을 묶어주는데, 이 때 US.NAME만 출력한다고 US.NAME만 그룹으로 묶을 경우 같은 이름인 것들이 한꺼번에 묶이기 때문에 US.ID도 꼭 GROUP 조건에 넣어 주어야 합니다.
