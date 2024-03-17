# **Exchange-Seats**

- [https://leetcode.com/problems/exchange-seats/](https://leetcode.com/problems/exchange-seats/)
- **문제**
  - 연속적으로 증가하는 **`id`**를 가진 **`Seat`** 테이블이 있고, 각 행은 학생의 이름과 그들의 **`id`**를 나타냅니다.
  - 문제의 목적은 두 명의 연속된 학생들의 좌석 **`id`**를 교환하는 것입니다. 만약 학생 수가 홀수라면 마지막 학생의 좌석은 교환되지 않습니다.
  - 결과는 **`id`**에 따라 오름차순으로 정렬되어야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Seat (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student VARCHAR(255)
);
INSERT INTO Seat (id, student) VALUES
(1, 'Abbot'),
(2, 'Doris'),
(3, 'Emerson'),
(4, 'Green'),
(5, 'Jeames');
```

```jsx
[ 정답 ]
SELECT	S.ID
,		CASE WHEN S.ID % 2=1 THEN COALESCE(A.STUDENT,S.STUDENT)
		ELSE B.STUDENT END STUDENT
FROM SEAT S
LEFT JOIN SEAT A
	ON S.ID+1	=	A.ID
LEFT JOIN SEAT B
	ON S.ID-1	=	B.ID
```

- **해설**
  - 조인을 활용해 메인 테이블의 한칸 앞 행과 뒷행을 조인해 한줄로 만들어 줍니다. 조인 실 후 전체 테이블 select문 실행시 테이블을 다 출력하면 아래와 같은 결과가 됩니다.
    사진(1)
    그 후 홀수이면 뒷 행의 학생이름을 출력해줍니다, 행의 줄 개수가 홀수일 때는 마지막 행의 이름은 자기자신이여야 하기 때문에 다음 행의 학생 이름이 NULL일 때 자기 자신을 출력해줍니다. 짝수이면 이전 행의 이름을 출력하는데 이전행은 무조건 있기 때문에(짝수니까..) COALESCE 함수를 사용할 필요는 없습니다.
