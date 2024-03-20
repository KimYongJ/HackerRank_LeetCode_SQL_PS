# **15-Days-of-Learning-SQL**

- [https://www.hackerrank.com/challenges/15-days-of-learning-sql/problem?isFullScreen=true](https://www.hackerrank.com/challenges/15-days-of-learning-sql/problem?isFullScreen=true)
- **문제**
  - **Julia는 15일간의 SQL 학습 콘테스트를 진행했습니다.**
  - **콘테스트 시작일은 2016년 3월 1일이고 종료일은 2016년 3월 15일입니다. 이외 범위는 주어지지 않습니다.**
  - **콘테스트 첫날부터 매일 최소 1번 이상 제출한 유일한 해커의 총 수를 출력하고, 매일 최대 횟수의 제출을 한 해커의 hacker_id와 이름을 찾는 쿼리를 작성하십시오. 만약 여러 해커가 최대 횟수의 제출을 했다면, 가장 낮은 hacker_id를 출력하십시오. 쿼리는 날짜별로 정렬하여 이 정보를 콘테스트 기간 동안 매일 출력해야 합니다.**

```jsx
[ 문제 조건 ]
CREATE TABLE Hackers (
    hacker_id INT, name VARCHAR(255)
);
CREATE TABLE Submissions (
    submission_date DATE,    submission_id INT,
    hacker_id INT,    score INT
);
INSERT INTO Hackers (hacker_id, name) VALUES
(15758, 'Rose'),(20703, 'Angela'),(36396, 'Frank'),
(38289, 'Patrick'),(44065, 'Lisa'),(53473, 'Kimberly'),
(62529, 'Bonnie'),(79722, 'Michael');
INSERT INTO submissions (submission_date, submission_id, hacker_id, score)VALUES
('2016-03-01', 8494, 20703, 0),('2016-03-01', 22403, 53473, 15),
('2016-03-01', 23965, 79722, 60),('2016-03-01', 30173, 36396, 70),
('2016-03-02', 34928, 20703, 0),('2016-03-02', 38740, 15758, 60),
('2016-03-02', 42769, 79722, 25),('2016-03-02', 44364, 79722, 60),
('2016-03-03', 45440, 20703, 0),('2016-03-03', 49050, 36396, 70),
('2016-03-03', 50273, 79722, 5),('2016-03-04', 50344, 20703, 0),
('2016-03-04', 51360, 44065, 90),('2016-03-04', 54404, 53473, 65),
('2016-03-04', 61533, 79722, 45),('2016-03-05', 72852, 20703, 0),
('2016-03-05', 74546, 38289, 0),('2016-03-05', 76487, 62529, 0),
('2016-03-05', 82439, 36396, 10),('2016-03-05', 90006, 36396, 40),
('2016-03-06', 90404, 20703, 0),('2016-03-08', 8494, 20703, 0),
('2016-03-08', 22403, 53473, 15);
```

```jsx
[ 정답 ]
SELECT    submission_date
,        (
            SELECT COUNT(DISTINCT S2.HACKER_ID)
            FROM submissions S2
            WHERE S2.submission_date = S1.submission_date
            AND (
                    SELECT COUNT(DISTINCT S3.submission_date)
                    FROM submissions S3
                    WHERE    S3.HACKER_ID = S2.HACKER_ID
                    AND        S3.submission_date < S1.submission_date
                ) = DATEDIFF(S1.submission_date, '2016-03-01')
        )EVERY_DAY                            -- 설명 2
,        (
            SELECT HACKER_ID
            FROM submissions S2
            WHERE S2.submission_date = S1.submission_date
            GROUP BY HACKER_ID
            ORDER BY COUNT(HACKER_ID) DESC, HACKER_ID
            LIMIT 1
        )WHO                                   -- 설명 3
,        (
            SELECT NAME
            FROM HACKERS
            WHERE HACKER_ID = WHO
        ) NAME                                 -- 설명 4
FROM (
        SELECT DISTINCT submission_date
        FROM submissions                       -- 설명 1
)S1
GROUP BY S1.submission_date
ORDER BY S1.submission_date
```

- **해설**
  - **상관 서브쿼리로만 이루어져있기 때문에 하나하나 설명합니다.**
  - **설명 1**
    - 이 문제는 상관 서브쿼리로 풀 수 있기 때문에 메인 테이블을 중복을 제거한 submission_date 만 출력 되도록 만듭니다.
  - **설명 2 : EVERY_DAY 컬럼**
    - **이 컬럼은 1일부터 15일까지 한번도 안끊기고 매일 제출한 해커들의 아이디 개수를 출력해야 합니다. 날짜별로 중복을 제거한 해커 아이디**( _SELECT COUNT(DISTINCT S2.HACKER_ID) 부분_ )**를 세야하기 때문에 메인 행의 날짜와 서브행의 날짜를 where 조건에 걸어 도출할 구간을 정해줍니다**( _WHERE S2.submission_date = S1.submission_date_ ) **또한 아이디 카운팅시 해당 아이디가 메인행의 날짜까지 매일 제출한 아이디인지 파악하기 위해 한번 더 서브쿼리를 만들어 where 절에 조건으로 추가해줍니다**.
    - **이렇게 서브쿼리에 또 서브쿼리로 들어가기 때문에 설명이 복잡합니다. 가장 마지막 서브쿼리를 S3 서브쿼리라 하겠습니다. S3서브쿼리의 핵심은 S2 서브쿼리에서 해커 아이디에 대해 유효성 검증을 하는것입니다. S2 해커 아이디가 매일 제출했는지를 말이죠. 이를 확인하기 위해 S3 서브쿼리에서 HACKER_ID의 범위를 S2 쿼리의 해커 아디로 제한을 둡니다**( _WHERE S3.HACKER_ID = S2.HACKER_ID 부분_ ) **또한 날짜 구간도 제한을 줘야 하기 때문에 날짜도 S1의 날짜보다 작은 것으로 제한을 둡니다.**( _AND S3.submission_date < S1.submission_date 부분_ ) **이렇게 제한을 둔 상태에서 제출 일자를 세는데 중복을 제거한 제출 일자를 셉니다.**( _SELECT COUNT(DISTINCT S3.submission_date) 부분_ ) **이렇게 얻은 제출 일자 개수가 메인행의 날짜에서 3월1일을 뺀 부분과 같은지 체크합니다.**( _DATEDIFF(S1.submission_date, '2016-03-01')부분_ ) **DATEDIFF 부분은 문제를 풀기 위한 하나의 FLAG로 작용합니다. 메인행의 날짜가 증가함에 따라 DATEDIFF함수의 결과는 0, 1, 2, 3, 4 . . 가됩니다.**
  - **설명 3 : WHO 컬럼**
    - **날짜 구간 별로 가장 많이 제출한 해커의 아이디를 출력해야 합니다. 날짜 구간을 제한을 두기위해 메인행과 서브행의 날짜를 조건절에 추가해줍니다.**( _WHERE S2.submission_date = S1.submission_date_ ) **그 후 HACKER_ID로 그룹을 묶고 ORDER BY 절을 사용해 가장 많은 해커 아이디를 기준으로 내림차순, 단순 해커 아이디를 기준으로 오름차순정렬합니다. 그리고 LIMIT으로 1행만 출력되도록하면 해당 날짜에 가장 많이 제출하고, 아이디가 가장 작은 것이 구해집니다.**
  - **설명 4 : NAME 컬럼**
    - **WHO 컬럼에서 나온 결과를 바탕으로 이름을 단순 출력합니다. 상관 서브쿼리는 위에서 밑으로 실행되기 때문에 WHO 컬럼을 먼저 구한 후 NAME컬럼에 상관해야합니다.**
