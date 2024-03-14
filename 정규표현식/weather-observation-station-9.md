- 정규표현식 문제

  - [https://www.hackerrank.com/challenges/weather-observation-station-9/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-9/problem?isFullScreen=true)

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

    - **문제 :** 모음으로 시작하지 않는 city를 출력하며, 중복을 허용하지 않습니다.

    ```jsx
    [ 정답(1) ]
    select distinct city
    from station
    where lower(city) regexp '^[^aieou]'

    [ 정답(2) ]
    select distinct city
    from station
    where lower(city) not regexp '^[aieou]'
    ```

    - **정답 (1) 해설 :** 다른 문제들과 비슷하며, 대괄호 밖에 ^ 문자는 ~~으로 시작하는 문자를 찾는 것이고, 대괄호 안에 ^를 적을 경우 해당 문자를 포함하지 않는 패턴을 찾게 됩니다.(대괄호 안에는 문자 패턴을 넣음) 그래서 대괄호 안의 ^는 모음이 아닌 문자 패턴을 찾게 되고, 대괄호 밖의 ^는 해당 패턴으로 시작하는 문자를 찾게 됩니다.
    - **정답 (2) 해설 :** 모음으로 시작하는 단어를 찾는데, regexp 키워드 앞에 not을 붙여줌으로 써 모음으로 시작하지 않는 단어를 찾게 됩니다.
