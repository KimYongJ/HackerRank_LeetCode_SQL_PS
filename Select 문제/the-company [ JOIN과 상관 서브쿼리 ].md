- the-company
  - [https://www.hackerrank.com/challenges/the-company/problem?isFullScreen=true](https://www.hackerrank.com/challenges/the-company/problem?isFullScreen=true)
  - **문제 :** Company 테이블에 있는 값을 출력하고, company_code 코드를 기준으로 Lead_Manager 테이블에서 lead_manager_code 개수를 카운팅하고, Senior_Manager 테이블에서 senior_manager_code 값을 카운팅하고, Manager 테이블에서 manager_code 값을 카운팅하고, Employee 테이블에서 employee_code 컬럼 값을 카운팅하여 출력하면 됩니다. 이 때 중복되는 행이 있을 수 있습니다. 그 부분은 제거를 해야 합니다. 그리고 출력은 company_code기준으로 오름차순 정렬이며, Company 테이블의 company_code는 모든 테이블의 외래키라고 생각하고 문제를 풀어도 됩니다.
  ```jsx
  [ 예상 출력 ]
  C1 Monika 1 2 1 2
  C2 Samantha 1 1 2 2
  ```
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Company (
      company_code VARCHAR(50),
      founder VARCHAR(100)
  );

  CREATE TABLE Lead_Manager (
      lead_manager_code VARCHAR(50),
      company_code VARCHAR(50)
  );

  CREATE TABLE Senior_Manager (
      senior_manager_code VARCHAR(50),
      lead_manager_code VARCHAR(50),
      company_code VARCHAR(50)
  );

  CREATE TABLE Manager (
      manager_code VARCHAR(50),
      senior_manager_code VARCHAR(50),
      lead_manager_code VARCHAR(50),
      company_code VARCHAR(50)
  );

  CREATE TABLE Employee (
      employee_code VARCHAR(50),
      manager_code VARCHAR(50),
      senior_manager_code VARCHAR(50),
      lead_manager_code VARCHAR(50),
      company_code VARCHAR(50)
  );

  -- Company 테이블 삽입
  INSERT INTO Company (company_code, founder) VALUES
  ('C1', 'Monika'),
  ('C2', 'Samantha');

  -- Lead_Manager 테이블 삽입
  INSERT INTO Lead_Manager (lead_manager_code, company_code) VALUES
  ('LM1', 'C1'),
  ('LM2', 'C2');

  -- Senior_Manager 테이블 삽입
  INSERT INTO Senior_Manager (senior_manager_code, lead_manager_code, company_code) VALUES
  ('SM1', 'LM1', 'C1'),
  ('SM2', 'LM1', 'C1'),
  ('SM3', 'LM2', 'C2');

  -- Manager 테이블 삽입
  INSERT INTO Manager (manager_code, senior_manager_code, lead_manager_code, company_code) VALUES
  ('M1', 'SM1', 'LM1', 'C1'),
  ('M2', 'SM3', 'LM2', 'C2'),
  ('M3', 'SM3', 'LM2', 'C2');

  -- Employee 테이블 삽입
  INSERT INTO Employee (employee_code, manager_code, senior_manager_code, lead_manager_code, company_code) VALUES
  ('E1', 'M1', 'SM1', 'LM1', 'C1'),
  ('E2', 'M1', 'SM1', 'LM1', 'C1'),
  ('E3', 'M2', 'SM3', 'LM2', 'C2'),
  ('E4', 'M3', 'SM3', 'LM2', 'C2');
  ```
  - 두가지 방법으로 풀어 보고, 해설을 제시합니다.
  ```jsx
  [ 정답(1) ]
  SELECT CMP.COMPANY_CODE , CMP.FOUNDER , LM.CNT , SM.CNT , M.CNT , EMP.CNT
  FROM COMPANY CMP
  LEFT OUTER JOIN (
                      SELECT COUNT(DISTINCT lead_manager_code) CNT, COMPANY_CODE
                      FROM LEAD_MANAGER
                      GROUP BY COMPANY_CODE
                  )LM ON LM.COMPANY_CODE = CMP.COMPANY_CODE
  LEFT OUTER JOIN (
                      SELECT COUNT(DISTINCT senior_manager_code) CNT ,  COMPANY_CODE
                      FROM SENIOR_MANAGER
                      GROUP BY  COMPANY_CODE
                  )SM ON SM.COMPANY_CODE = CMP.COMPANY_CODE
  LEFT OUTER JOIN (
                      SELECT COUNT(DISTINCT manager_code) CNT,   COMPANY_CODE
                      FROM MANAGER
                      GROUP BY   COMPANY_CODE
                  )M ON M.COMPANY_CODE = CMP.COMPANY_CODE
  LEFT OUTER JOIN (
                      SELECT COUNT(DISTINCT employee_code) CNT, COMPANY_CODE
                      FROM EMPLOYEE
                      GROUP BY  COMPANY_CODE
                  )EMP ON EMP.COMPANY_CODE = CMP.COMPANY_CODE
  ORDER BY CMP.COMPANY_CODE
  ```
  - **해설 :** COMPANY 테이블을 기준으로 나머지 테이블들을 COMPANY_CODE 컬럼 기준으로 조인해줍니다. 이 때 각 테이블당 카운팅하고자 하는 컬럼을 COUNT함수 안에 넣어 줍니다. 이 때 중복된 행이 있을 수 있으므로 COUNT함수 안에 DISTINCT키워드를 넣어주는데 COUNT 함수 안에서 사용되는 DISTINCT 키워드는 일반적인 DISTINCT와는 다르게 작동합니다.
    - **DISTINCT :** 보통 DISTINCT 키워드는 SQL 쿼리에서 선택된 모든 컬럼에 대해 중복된 행을 제거하는 키워드입니다. 그러나 COUNT() 함수와 함께 사용될 때는 조금 달라집니다. COUNT( DISTINCT employee_code ) 와 같이 사용하면, 지정된 컬럼 내에서 중복된 값을 가진 행을 하나로 취급하여 개수를 셉니다. 즉, 해당 컬럼에서 고유한 값들의 수를 세는 것입니다. 만약 employee_code가 여러 행에 걸쳐 나타난다면, DISTINCT를 사용함으로써 그 사람은 카운팅을 단 한 번만 하게 됩니다.
  - 출력은 조인한 테이블 들의 COUNT 함수 결과를 붙여 출력해주고 COMPANY_CODE 컬럼을 기준으로 오름차순 정렬 후 출력합니다.
  ```jsx
  [ 정답(2) ]
  SELECT    CMP.COMPANY_CODE
  ,        CMP.FOUNDER
  ,        (SELECT COUNT(DISTINCT LEAD_MANAGER_CODE) FROM LEAD_MANAGER WHERE COMPANY_CODE = CMP.COMPANY_CODE)
  ,        (SELECT COUNT(DISTINCT SENIOR_MANAGER_CODE) FROM SENIOR_MANAGER WHERE COMPANY_CODE = CMP.COMPANY_CODE)
  ,        (SELECT COUNT(DISTINCT MANAGER_CODE) FROM MANAGER WHERE COMPANY_CODE = CMP.COMPANY_CODE)
  ,        (SELECT COUNT(DISTINCT EMPLOYEE_CODE) FROM EMPLOYEE WHERE COMPANY_CODE = CMP.COMPANY_CODE)
  FROM COMPANY CMP
  ORDER BY CMP.COMPANY_CODE
  ```
  - **해설 :** 처음 제시한 쿼리는 조인 조건을 명시하여 코드가 길어집니다. 이를 줄이기 위해 상관 서브쿼리를 해 풀어 봤습니다.
    - **상관 서브쿼리 :** 메인 쿼리의 각 행마다 실행되는 서브 쿼리로, 메인 쿼리의 컬럼 값을 참조하여 실행 됩니다. 이런 방식으로 메인 쿼리의 현재 행에 대한 정보를 사용하여 서브 쿼리의 결과를 필터링 할 수 있습니다.
      - **단점 :** 상관 서브 쿼리는 메인 쿼리의 각 행에 대해 별도로 실행되기 때문에 데이터 셋이 크면 **계속 쿼리가 실행되어 성능이 저하**됩니다.
  - 메인 쿼리의 한 행마다 각 관리 계층 테이블을 조회합니다. 메인 쿼리의 행과 같은 COMPANY_CODE를 가진 레코드의 수를 세기 위해 WHERE 조건에 COMPANY_CODE 컬럼이 같은지 검사하는 구문을 넣습니다. 그리고 중복 행이 있을 수 있으므로 COUNT 함수 안에 DISTCINT 키워드를 넣고, 중복 행을 제거할 컬럼명을 넣어 주면 됩니다.
