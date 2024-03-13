# **Average-Time-of-Process-per-Machine**

- [https://leetcode.com/problems/average-time-of-process-per-machine/](https://leetcode.com/problems/average-time-of-process-per-machine/)
- **문제 :** 각 기계가 프로세스를 완료하는 데 평균적으로 얼마나 걸리는지를 찾는 것입니다. 이 평균 시간은 각 프로세스를 완료하는 데 걸린 전체 시간을 해당 기계에서 실행된 프로세스 수로 나누어 계산됩니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Activity (
  machine_id INT,
  process_id INT,
  activity_type ENUM('start', 'end'),
  timestamp FLOAT
);
INSERT INTO Activity (machine_id, process_id, activity_type, timestamp) VALUES
(0, 0, 'start', 0.712),
(0, 0, 'end', 1.520),
(0, 1, 'start', 3.140),
(0, 1, 'end', 4.120),
(1, 0, 'start', 0.550),
(1, 0, 'end', 1.550),
(1, 1, 'start', 0.430),
(1, 1, 'end', 1.420),
(2, 0, 'start', 4.100),
(2, 0, 'end', 4.510),
(2, 1, 'start', 2.500),
(2, 1, 'end', 5.000);
```

```jsx
[ 정답(1) ]
SELECT  MACHINE_ID
,       ROUND(SUM(TIMESTAMP) / COUNT(PROCESS_ID),3)  PROCESSING_TIME
FROM(
        SELECT  MACHINE_ID
        ,       PROCESS_ID
        ,       MAX(TIMESTAMP)-MIN(TIMESTAMP) TIMESTAMP
        FROM ACTIVITY
        GROUP BY MACHINE_ID, PROCESS_ID
    )MA
GROUP BY MACHINE_ID

[ 정답(2) ]
SELECT	A1.MACHINE_ID
,		ROUND(SUM(A1.TIMESTAMP - A2.TIMESTAMP) / COUNT(DISTINCT A1.PROCESS_ID),3)AS PROCESSING_TIME
FROM ACTIVITY A1
INNER JOIN ACTIVITY A2
	ON A1.MACHINE_ID = A2.MACHINE_ID
	AND A1.PROCESS_ID	= A2.PROCESS_ID
	AND A1.TIMESTAMP > A2.TIMESTAMP
GROUP BY A1.MACHINE_ID
```

- **정답(1) 해설 :** START와 END를 뺀 값의 합을 구하고, 그 값을 전체 프로세스 수로 나누어야 합니다. 그렇기에 분할해서 문제를 풀었습니다. 먼저 안쪽 서브쿼리에서 START와 END의 차이를 구하기 위해 MAX, MIN 함수를 사용해 차이를 구하는 쿼리를 만들었습니다. 그 후 이 테이블을 다시 머신ID로 그룹화하고, 프로세스 개수로 나누어 평균 시간을 구했습니다.
- **정답(2) 해설 :** SELF 조인으로도 문제를 풀어 보았습니다. 자기 자신을 조인하는데 메인 테이블보다 시간이 작은 것만 조인하도록 하여 START와 END가 한 줄에 있도록 만들었습니다. 아래 사진은 조인한 후 전체 데이터를 단순 조회했을 때 결과 입니다.
  
  ![사진1](https://github.com/KimYongJ/HackerRank_LeetCode_SQL_PS/assets/106525587/7e3a8e18-98e9-4824-ade8-176c78676b31)


  위에서 보는 바와 같이 한줄에 값이 다 있으므로 SUM을 통해 두 작업시간에 대해 차이를 더해주고, 프로세스의 개수를 파악해 나눠주기만 하면됩니다. 이 때 프로세스 아이디는 중복이 있을 수 있기 때문에 COUNT 함수안에 DISTINCT 키워드를 반드시 넣어 주어야 합니다. DISTINCT 키워드는 집계함수 안에 있을 때 같은 컬럼을 제거하기 때문에 동일 값이 많아도 하나로 카운팅됩니다.
