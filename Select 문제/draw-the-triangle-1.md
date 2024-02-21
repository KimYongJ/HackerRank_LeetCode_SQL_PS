- draw-the-triangle-1
  - [https://www.hackerrank.com/challenges/draw-the-triangle-1/problem?isFullScreen=true](https://www.hackerrank.com/challenges/draw-the-triangle-1/problem?isFullScreen=true)
  - **문제 :** ‘\*’모양으로 삼각형을 역순으로 출력하는 문제입니다. 가장 긴 별의 갯수는 20개부터 입니다.
  ```jsx
  [ 정답 ]
  Set @numb = 21;
  select repeat('* ', @numb := @numb - 1)
  from information_schema.tables
  limit 20;
  ```
  - **해설**
    - **Set @numb = 21 의미 :** Set 키워드와 ‘@’ 기호를 사용해 사용자 정의 변수를 선업합니다. 이변수를 사용해 출력되는 별의 갯수를 조절할 수 있습니다. 사용자 정의 변수는 특정 세션 동안에만 존재하고 그 세션 내에서만 값이 유지됩니다. 시스템 변수는 ‘@@’으로 시작합니다.
    - **repeat('\* ', @numb := @numb - 1) 의미 :** repeat함수는 첫번 째 인자로 전달된 문자열을 두번째인자 만큼 반복합니다. 첫번 째인자로 문자 ‘\* ‘ 를 전달하고, 두번째 인자로 사용자 정의 변수를 전달하는데 이 때 numb의 값을 1을 감소시킨 값으로 계속해서 호출 합니다. 초기 numb 값을 21로 한 이유는 -1을 먼저해줄 것이기 때문입니다.
    - **information_schema.tables 의미 :** MySQL에서는 사전에 정의된 시스템 데이터베이스를 select할 수있습니다. 이 코드는 INFORMATION_SCHEMA스키마의 \*\*\*\*tables을 select하는 것입니다. 여기서 해당 테이블은 반복 가능한 소스로 사용하기 위한 더미데이터 입니다. MySQL에서 특정 수의 반복을 생성하기 위해 기존의 큰 테이블을 사용하는 것입니다.
    - **limit 20 의미 :** 최대 20줄을 출력하라고 하였으므로 작성하였습니다.
