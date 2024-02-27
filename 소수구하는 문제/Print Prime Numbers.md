- **Print Prime Numbers**
  - [https://www.hackerrank.com/challenges/print-prime-numbers/problem?isFullScreen=true](https://www.hackerrank.com/challenges/print-prime-numbers/problem?isFullScreen=true)
  - **문제 :** 1부터 1,000까지 숫자 중 소수인 것을 한 줄로 출력하는데, 숫자를 한 줄로 나열할 때 숫자와 숫자 사이에 ‘&’ 문자를 사용해 숫자를 붙여 출력합니다.
  ```jsx
  [ 이 문제에서는 테이블이 없기 때문에 기본 스키마를 사용합니다 ]
  SELECT ROW_NUMBER() OVER() NUM
  FROM INFORMATION_SCHEMA.COLUMNS C1
  CROSS JOIN INFORMATION_SCHEMA.COLUMNS C2
  ON C2.COLUMN_NAME = C1.COLUMN_NAME
  LIMIT 1000
  ```
  ```jsx
  [ 정답 ]
  WITH TEMP AS(
  				SELECT ROW_NUMBER() OVER() NUM
  				FROM INFORMATION_SCHEMA.COLUMNS C1
  				CROSS JOIN INFORMATION_SCHEMA.COLUMNS C2
  					ON C2.COLUMN_NAME = C1.COLUMN_NAME
  				LIMIT 1000
  )
  SELECT GROUP_CONCAT(T1.NUM SEPARATOR '&')
  FROM TEMP T1
  WHERE NOT EXISTS (
  	SELECT 1
  	FROM 	TEMP T2
  	WHERE 	T1.NUM != T2.NUM
  	AND 	T1.NUM % T2.NUM = 0
  	AND 	T2.NUM <= SQRT(T1.NUM)
  	AND 	T2.NUM > 1
  )
  AND T1.NUM > 1
  ```
  - **해설**
    - **WITH 절 :** TEMP라는 임시 테이블을 생성하여, ROW_NUMBER() 오버() 함수를 사용해 각 행에 대한 순차적인 번호(시퀀스)를 할당합니다. CROSS JOIN은 두 개의 **`INFORMATION_SCHEMA.COLUMNS`** 테이블을 조인하여 더 많은 행을 만들기 위해 사용되며, LIMIT 1000은 최대 1000개의 숫자를 생성하기 위한 제한 조건입니다.
    - **GROUP_CONCAT 함수 :** 이 함수는 여러 행의 결과를 하나의 문자열로 결합할 때 사용됩니다. 여기서 SEPARATOR '&'는 각 숫자 사이에 앰퍼샌드(&) 기호를 구분자로 사용하여 결과를 연결하라는 지시입니다.
    - **WHERE 절 :** T1 테이블이 소수인 것만 출력 되도록 하기 위해 NOT EXISTS 안의 서브쿼리에서는 소수가 아닌 숫자들만 출력 되도록 하였습니다.
    - **NOT EXISTS 안 서브쿼리 :** 이 쿼리는 이중 for문 이라고 생각하시면 됩니다. T1테이블의 한 행마다 T2 테이블 전체가 조회됩니다. 서브쿼리에서는 소수가 아닌 숫자만 출력되야 하므로 조건이 좀많습니다. 먼저 T1의 NUM과 T2의 NUM이 같지 않아야 합니다. 또한 기준이 되는 T1.NUM 값을 T2.NUM 값으로 나누었을 때 나머지가 0이 되야 소수가 아닌 숫자입니다. 그리고 T2.NUM의 범위는 1보다 커야하고, T1.NUM의 제곱근과 같거나 작아야 합니다. 제곱근 보다 작거나 같은 것은 연산을 빨리하기 위해 넣은 코드입니다.(어떤 수 N이 소수가 아니라면, 그 수는 반드시 sqrt(N) 이하의 약수를 가집니다.)
      - **T2.NUM <= SQRT(T1.NUM) 코드** 대신 **T2.NUM < (T1.NUM)** 이렇게 해도 정답이긴 합니다.
