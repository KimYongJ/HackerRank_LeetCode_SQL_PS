- 정규표현식 문제

  - [https://www.hackerrank.com/challenges/weather-observation-station-12/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-12/problem?isFullScreen=true)

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

    - **문제 :** 모음으로 시작하지 않고, 끝나지도 않는 city를 중복없이 출력하세요

    ```jsx
    [ 정답 ]
    select distinct city
    from station
    where lower(city) regexp '^[^aieou].*[^aieou]$'
    ```

    - **해설 :** 대괄호 안에 ^ 키워드를 넣음으로 써 모음이 아닌 문자 패턴을 생성하고, 대괄호 왼쪽과 오른쪽에 각각 ^ 키워드와 $ 키워드를 넣음으로 써 모음이 아닌 문자 패턴으로 시작하고, 끝나는 것을 표현했습니다. 중간에 점(.)의 의미는 임의의 단일 문자와 일치한다는 것을 의미하며 어떤 문자든 상관없이 매칭될 수 있음을 의미합니다. 점(.) 뒤에 바로 에스터리스크(_)는 바로 앞에 나온 요소가 0 번이상 반복될 수 있음을 의미합니다. 점(.)과 에스터리스크(_)가 같이 사용됨으로 써 어떤 문자든 0개 이상 존재할 수 있다는 의미가 됩니다.
