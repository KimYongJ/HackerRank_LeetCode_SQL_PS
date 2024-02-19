- 정규표현식 문제

  - [https://www.hackerrank.com/challenges/weather-observation-station-7/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-7/problem?isFullScreen=true)

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

    - **문제 :** STATIION테이블에서 모음으로 끝나는 CITY이름의 목록을 조회하는 문제며 중복된결과 출력은 하지 않습니다.

    ```jsx
    [ 정답 ]
    SELECT distinct CITY
    FROM station
    WHERE LOWER(CITY) REGEXP '[aieou]$'
    ```

    - **해설 :** lower함수로 모두 소문자로 변환 후 REGEXP 키워드를 사용해 모음으로 끝나는 영어 단어를 찾아 줍니다. $(달러) 키워드는 특정 단어로 끝나는 것을 찾아줍니다. 대괄호 안에 문자열을 넣으면 해당 문자들의 패턴을 찾아줍니다. [aieou]를 적었기 때문에 a부터 u까지 문자가 포함되었는지 찾습니다.
