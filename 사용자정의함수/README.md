- User-Defined Function ( 사용자 정의 함수 )
  - MySql 기준 사용자 정의 함수 기본 형식과 사용 방법은 아래와 같습니다.
  ```jsx
  [ 기본 형식 ]
  CREATE FUNCTION `function_name` (`parameter_name` datatype)
  RETURNS datatype DETERMINISTIC
  BEGIN
      DECLARE `variable_name` datatype;
      SET `variable_name` = 값 또는 연산;
      -- 여기에 로직 추가 가능
  		--IF value > 50 then
  		--		set value = 'vip'
  		--ELSEIF value < 50 then
  		--		set value = 'vvip'
  		--END IF
      RETURN (`variable_name`); -- 또는 직접적인 계산 결과나 쿼리 결과
  END;

  [ 사용 방법 ]
  SELECT `function_name`(`parameter_value`);
  ```
  - **CREATE FUNCTION :** 함수 생성시 쓰는 키워드로, 순서대로 함수 이름 다음 괄호 안에 파라미터 이름과 데이터타입을 넣습니다.
  - **RETURNS :** 출력될 결과의 데이터타입을 적어주면 됩니다.
  - **DETERMINISTIC :** 이 키워드는 함수가 동일한 입력값에 대해 항상 동일한 결과를 반환함을 MySQL에 알려주는 역할을 합니다. 이는 함수의 성질을 정의하는 중요한 부분입니다.
  - **BEGIN - END :** 함수의 몸체 정의라고 생각하면 됩니다.
  - **DECLARE , SET :** 변수 선언 등이 가능한 키워드 입니다. 해당 키워드의 뒤에는 반드시 세미콜론(;)을 적어야 합니다. declare는 변수 선언, set은 해당 변수에 값을 넣는 역할을 합니다.
  - **RETURN :** 이 키워드는 함수 몸체에서 반환 값을 정의하며 반드시 있어야 합니다.
