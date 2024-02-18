- 정규표현식 문제

  - [https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true)

    ```jsx
    [ 문제 조건 ]
    CREATE TABLE IF NOT EXISTS STATION (
        ID int auto_increment primary key,
        CITY varchar(100),
        STATE varchar(100),
        LAT_N decimal(10, 8),
        LONG_W decimal(11, 8)
    );

    -- 임시 데이터 삽입
    INSERT INTO STATION (CITY, STATE, LAT_N, LONG_W) VALUES
    ('Auckland', 'Auckland Region', 36.848460, 174.763332),
    ('Edinburgh', 'Scotland', 55.953251, -3.188267),
    ('Istanbul', 'Istanbul Province', 41.008238, 28.978359),
    ('Osaka', 'Osaka Prefecture', 34.693738, 135.502165),
    ('Utrecht', 'Utrecht Province', 52.090737, 5.121420),
    ('London', 'England', 51.507351, -0.127758),
    ('Tokyo', 'Tokyo Metropolis', 35.689487, 139.691706),
    ('Berlin', 'Berlin State', 52.520007, 13.404954);
    ```

    - **문제 :** STATION 테이블에서 첫 글자와 마지막 글자가 모두 모음(a, e, i, o, u)인 도시 이름의 목록을 조회합니다. 결과에 중복이 포함되어서는 안 됩니다.

    ```jsx
    [ 정답(1) ]
    SELECT distinct CITY
    FROM station
    WHERE LOWER(CITY) REGEXP '^[aieou]'
    or LOWER(CITY) REGEXP '[aieou]$'

    [ 정답(2) ]
    SELECT distinct CITY
    FROM station
    WHERE LOWER(CITY) REGEXP '^[aieou].*[aieou]$'
    ```

    - **해설 :** 정답 2를 보면, 정규 표현식은 3가지로 구분됩니다. 먼저 점(.) 이전에 ^[aieou] 문자열은 모음으로 시작(^)하는 문자열을 찾고, 마지막 [aieou]$ 이부분은 모음으로 종료($)되는 문자열을 찾습니다. 여기서 점(.)의 의미는 임의의 단일 문자와 일치한다는 것을 의미하며 어떤 문자든 상관없이 매칭될 수 있음을 의미합니다. 점(.) 뒤에 바로 에스터리스크(_)는 바로 앞에 나온 요소가 0 번이상 반복될 수 있음을 의미합니다. 점(.)과 에스터리스크(_)가 같이 사용됨으로 써 어떤 문자든 0개 이상 존재할 수 있다는 의미가 됩니다.
