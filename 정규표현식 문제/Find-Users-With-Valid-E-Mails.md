# **Find-Users-With-Valid-E-Mails**

- [https://leetcode.com/problems/find-users-with-valid-e-mails/](https://leetcode.com/problems/find-users-with-valid-e-mails/)
- **문제 :** 이메일이 유효한 것들만 출력하는 문제입니다. 접두사는 문자로 시작해야 하고, 중간에는 숫자, 대소문자, 밑줄, 마침표, 대시를 사용할 수 있고 접미사는 **@leetcode.com** 입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Users (
  user_id INT,
  name VARCHAR(255),
  mail VARCHAR(255),
  PRIMARY KEY (user_id)
);
INSERT INTO Users (user_id, name, mail) VALUES
(1, 'Winston', 'winston@leetcode.com'),
(2, 'Jonathan', 'jonathansgreat'),
(3, 'Annabelle', 'bella@leetcode.com'),
(4, 'Sally', 'sally.come@leetcode.com'),
(5, 'Marwan', 'quartz2928@leetcode.com'),
(6, 'David', 'david69@gmail.com'),
(7, 'Shapiro', '.shapiro@leetcode.com');
```

```jsx
[ 정답 ]
select *
from users
where mail regexp '^[a-zA-Z][a-zA-Z0-9._-]*@leetcode[.]com$'
```

- **해설**
  - **접두사 :** ^[a-zA-Z] 접두사를 표현하기 위해 ^ 문자를 사용합니다. 대괄호 안에 a-zA-Z가 들어가면 접두사가 영어 대소문자 중 하나가 됩니다.
  - **중간 패턴 :** [a-zA-Z0-9._-]\* 부분은, 시작문자 다음에 올 문자들의 패턴을 입력하는 것으로, 알파벳 대소문자와 숫자, 그리고 점(.) 언더바(\_) 대시(-)가 들어갈 수 있는데 에스터리스크가 들어감으로써 해당하는 패턴의 문자가 0번이상 반복될 수 있음을 의미합니다.
  - **접미사 :** 접미사는 패턴 마지막에 $ 기호로 표시합니다. 이 때, 대괄호 안에 점(.)을 적은 이유는, 정규 표현식에서 마침표는 특별한 의미를 가지는 메타문자로 어떤 한 문자와도 일치할 수 있다는 의미입니다. 하지만 이메일 주소에서 마침표 문자는 문자 그대로의 점(.)으로 인식해야 하기 때문에 대괄호[]로 감싸 사용합니다.
