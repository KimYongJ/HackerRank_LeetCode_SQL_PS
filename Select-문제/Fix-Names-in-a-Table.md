# **Fix-Names-in-a-Table**

- [https://leetcode.com/problems/fix-names-in-a-table/](https://leetcode.com/problems/fix-names-in-a-table/)
- **문제 :** name 컬럼의 가장 앞글자만 대문자로 하고, 나머지는 소문자로 변경하여 출력합니다. 이 때 user_id기준 오름차순 정렬 출력해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Users (
  user_id INT PRIMARY KEY,
  name VARCHAR(100)
);
INSERT INTO Users (user_id, name) VALUES
(1, 'alice'),
(2, 'bOB');
```

```jsx
[ 정답 ]
select	user_id
,		concat(upper(substr(name,1,1)),lower(substr(name,2)))as name
from users
order by user_id;
```

- **해설 :** 오라클에서는 첫 글자를 대문자로 만들어주는 INITCAP 함수가 있지만 mysql은 없기 때문에 직접 구현해야 합니다. 문자열을 자를 수 있는 substr함수를 사용해 자른 후 upper 함수와 lower함수를 각각 사용해 두 문자열을 붙여주면됩니다.
- **SUBSTR**
  - **형태 :** SUBSTR(string, start, length)
  - **인자 순서 :** 원본 문자열 , 추출을 시작할 위치(_1부터시작 음수면 뒤부터 시작_), 추출할 문자수(선택사항) 마지막 생략시 START 위치부터 문자열의 끝까지 출력됩니다.
  - **예시 :** SELECT SUBSTR('MySQL Function', 2, 3) - 2번째 문자부터 3개의 문자를 추출합니다.
