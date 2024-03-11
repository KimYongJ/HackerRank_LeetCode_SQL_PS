# **Not-Boring-Movies**

- [https://leetcode.com/problems/not-boring-movies/](https://leetcode.com/problems/not-boring-movies/)
- **문제 :** 테이블에서 ID의 값이 홀수이면서 영화 설명이 ‘boring’이 아닌 데이터를 출력하며 Rating 기준으로 내림차순 정렬 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Cinema (
  id INT,
  movie VARCHAR(255),
  description VARCHAR(255),
  rating FLOAT
);
INSERT INTO Cinema (id, movie, description, rating) VALUES
(1, 'War', 'great 3D', 8.9),
(2, 'Science', 'fiction', 8.5),
(3, 'irish', 'boring', 6.2),
(4, 'Ice song', 'Fantasy', 8.6),
(5, 'House card', 'Interesting', 9.1);
```

```jsx
[ 정답 ]
SELECT ID, MOVIE, DESCRIPTION, RATING
FROM CINEMA
WHERE MOD(ID, 2) = 1
AND DESCRIPTION != 'boring'
ORDER BY RATING DESC
```

- **해설 :** ID의 홀수를 구하기 위해 MySql의 MOD 함수를 사용합니다. 첫번 째 인자로 컬럼을 주고, 두번 째 인자로 나머지를 구할 숫자를 넣습니다.
