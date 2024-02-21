- salary-of-employees
  - [https://www.hackerrank.com/challenges/salary-of-employees/problem?isFullScreen=true](https://www.hackerrank.com/challenges/salary-of-employees/problem?isFullScreen=true)
  - **문제 :** employee 테이블에서 급여가 2000이상이며 근무기간이 10미만인 직원의 name을 출력하는데 employee_id기준으로 오름차순 정렬 출력하는 문제 입니다.
  ```jsx
  [ 정답 ]
  select name
  from employee
  where salary >= 2000
  and months < 10
  order by employee_id
  ```
