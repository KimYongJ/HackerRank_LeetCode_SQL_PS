- 정규표현식 문제

  - [https://www.hackerrank.com/challenges/weather-observation-station-11/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-11/problem?isFullScreen=true)

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

    - 문제 : 모음으로 시작하지 않거나, 모음으로 끝나지 않는 city를 중복없이 출력하세요

    ```jsx
    [ 정답 ]
    select distinct city
    from station
    where
    lower(city) regexp '^[^aieou]'
    or
    lower(city) regexp '[^aieou]$'
    ```

    - **해설 :** 대괄호 안에 ^ 기호를 사용해 모음으로 되어있지 않은 패턴을 생성한 후, 시작과 끝을 찾는 기호인 ^과 $를 사용해 or연산자로 조회했습니다.
