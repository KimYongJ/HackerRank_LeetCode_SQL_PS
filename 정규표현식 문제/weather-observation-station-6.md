- 정규표현식 문제

  - [https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true)

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

    - **문제 :** city 컬럼 값의 시작 영어 단어가 a, e, i, o, u 로 시작하는 행만 출력하는데 중복없이 출력합니다.

    ```jsx
    [ 정답 ]
    select distinct city
    from station
    where lower(city) REGEXP '^[aieou]'
    ```

    - **해설 :** 정규 표현식을 써서 해결합니다. city의 첫 글자가 대소문자인지 상관없이 작동하게 하기위해 lower로 소문자로 만든 후 정규 표현식을 사용했습니다. 정규 표현식사용시 regular expression 약자인 REGEXP를 써준 후 작은 따옴표, 혹은 큰 따옴표 안에 정규 표현식을 써줍니다. 대괄호 안에 문자열을 넣으면 해당 문자들의 패턴을 찾아줍니다. [aieou]를 적었기 때문에 a부터 u까지 문자가 포함되었는지 찾습니다. 또 가장 앞에 ^ 기호를 붙이면 해당 문자로 시작하는 문자열을 찾습니다. ^ 기호를 대괄호 안에 쓰면 전혀다른 의미가 됩니다. 그래서 결과적으로 ^[aieou] 를 사용하면 a부터 u까지 문자로 시작하는 패턴을 찾습니다.
