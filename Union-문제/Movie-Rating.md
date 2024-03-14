# **Movie-Rating**

- [https://leetcode.com/problems/movie-rating/](https://leetcode.com/problems/movie-rating/)
- **문제 :** 영화 평점 데이터베이스에서 다음 두 가지 정보를 찾는 것입니다:
  1. 가장 많은 영화에 평점을 매긴 사용자의 이름을 찾습니다. 동점인 경우, 이름이 사전 순으로 더 앞서는 사용자를 선택합니다.
  2. 2020년 2월에 평균 평점이 가장 높은 영화의 이름을 찾습니다. 동점인 경우, 영화 제목이 사전 순으로 더 앞서는 영화를 선택합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Movies (
    movie_id INT,
    title VARCHAR(255)
);
CREATE TABLE Users (
    user_id INT,
    name VARCHAR(255)
);
CREATE TABLE MovieRating (
    movie_id INT,
    user_id INT,
    rating INT,
    created_at DATE
);
INSERT INTO Movies (movie_id, title) VALUES
(1, 'Avengers'),
(2, 'Frozen 2'),
(3, 'Joker');
INSERT INTO Users (user_id, name) VALUES
(1, 'Daniel'),
(2, 'Monica'),
(3, 'Maria'),
(4, 'James');
INSERT INTO MovieRating (movie_id, user_id, rating, created_at) VALUES
(1, 1, 3, '2020-01-12'),
(1, 2, 4, '2020-02-11'),
(1, 3, 4, '2020-02-12'),
(1, 4, 5, '2020-01-01'),
(2, 1, 1, '2020-02-17'),
(2, 1, 1, '2020-02-01'),
(2, 3, 2, '2020-03-01'),
(2, 3, 2, '2020-02-02'),
(3, 1, 5, '2020-02-22'),
(3, 2, 4, '2020-02-25');

INSERT INTO Movies (movie_id, title) VALUES
(1, 'Rebecca');
INSERT INTO Users (user_id, name) VALUES
(1, 'Rebecca');
INSERT INTO MovieRating (movie_id, user_id, rating, created_at) VALUES
(1, 1, 5, '2020-02-12');
```

```jsx
[ 정답 ]
SELECT NAME AS RESULTS
FROM(
		SELECT	U.NAME
		FROM MOVIERATING M
		INNER JOIN USERS U
				ON U.USER_ID = M.USER_ID
		GROUP BY U.USER_ID, U.NAME
		ORDER BY COUNT(*) DESC , NAME
		LIMIT 1
)TEMP

UNION ALL

SELECT TITLE AS RESULTS
FROM(
		SELECT	M.TITLE
		FROM movierating MR
		INNER JOIN MOVIES M
			ON M.MOVIE_ID = MR.MOVIE_ID
		WHERE DATE_FORMAT(MR.created_at, "%Y-%m") = '2020-02'
		GROUP BY MR.MOVIE_ID, M.TITLE
		ORDER BY AVG(MR.RATING) DESC, M.TITLE
		LIMIT 1
)TEMP

```

- **해설 :** 각각의 결과를 따로 구한 후 UNION ALL로 합쳐줍니다. 이 때 UNION을 쓰면 안됩니다. 이유는 두 쿼리가 같은 값을 갖는다면 UNION은 한줄로 출력하기 때문입니다. 2020년 2월의 평균 평점을 구하기 위해 DATE_FORMAT함수를 사용했습니다.
- **DATE_FORMAT**
  - 날짜와 시간 값을 지정된 형식의 문자열로 변환하는 데 사용됩니다. 포맷은 자유롭게 합쳐서 사용할 수 있으며 아래와 같습니다.
  - **`%Y`**: 4자리 연도 (예: 2021)
  - **`%y`**: 2자리 연도 (예: 21)
  - **`%M`**: 월의 전체 이름 (예: January, February, ... , December)
  - **`%m`**: 2자리 월 (예: 01~12)
  - **`%c`**: 월 (예: 1~12)
  - **`%d`**: 2자리 일 (예: 01~31)
  - **`%e`**: 일 (예: 1~31)
  - **`%H`**: 24시간 형식의 2자리 시간 (예: 00~23)
  - **`%h`** 또는 **`%I`**: 12시간 형식의 2자리 시간 (예: 01~12)
  - **`%i`**: 2자리 분 (예: 00~59)
  - **`%s`**: 2자리 초 (예: 00~59)
  - **`%p`**: AM 또는 PM
  - **`%W`**: 주의 요일의 전체 이름 (예: Sunday)
  - **`%a`**: 주의 요일의 축약형 이름 (예: Sun)
  - **`%b`**: 월의 축약형 이름 (예: Jan)
  - **`%j`**: 연중 일수 (예: 001~366)
  - 예)
    - March 15, 2021 표현을 원할 경우 : SELECT DATE_FORMAT('2021-03-15', '%M %d, %Y');
- **UNION 과 UNION ALL :** UNION과 UNION ALL은 두 개 이상 SELECT 문의 결과를 하나의 결과 집합으로 결합합니다. 그러나 UNION은 중복된 행은 제거하고 고유한 결과만을 반환합니다. 내부적인 작업을 통해 중복을 제거하기 때문에 UNION ALL 보다 느릴 수 있습니다. UNION ALL은 중복된 행을 모두 포함하여 반환합니다.
