- **Combine-Two-Tables**
  - [https://leetcode.com/problems/combine-two-tables/](https://leetcode.com/problems/combine-two-tables/)
  - **문제 :** person 테이블에서 firstName, lastName 컬럼과 address 테이블에서 city, state 컬럼을 순서대로 출력하는데 city가 null일 경우도 출력되도록 합니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Person (
      PersonId int PRIMARY KEY,
      LastName varchar(255),
      FirstName varchar(255)
  );

  CREATE TABLE Address (
      AddressId int PRIMARY KEY,
      PersonId int,
      City varchar(255),
      State varchar(255),
      FOREIGN KEY (PersonId) REFERENCES Person(PersonId)
  );

  INSERT INTO Person (PersonId, LastName, FirstName) VALUES
  (1, '김', '철수'),
  (2, '이', '영희'),
  (3, '박', '민수');

  INSERT INTO Address (AddressId, PersonId, City, State) VALUES
  (1, 1, '서울', '서울특별시'),
  (2, 2, '부산', '부산광역시');
  ```
  ```jsx
  [ 정답 ]
  select	ps.firstName
  ,		ps.lastName
  ,		ad.city
  ,		ad.state
  from person ps
  left outer join address ad on ad.personId	=	ps.personId
  ```
