# **Patients-With-a-Condition**

- [https://leetcode.com/problems/patients-with-a-condition/](https://leetcode.com/problems/patients-with-a-condition/)
- **문제 :** **Patients** 테이블에서 1형 당뇨병(Type I Diabetes) 환자들을 찾는 문제입니다. 1형 당뇨병은 **DIAB1 문자를 포함하는** 코드를 갖고 있습니다. 환자들의 진단 조건은 **conditions** 필드에 공백으로 구분되어 저장되어 있으며, 여러 조건이 동시에 있을 수 있습니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Patients (
  patient_id INT,
  patient_name VARCHAR(255),
  conditions VARCHAR(255)
);
INSERT INTO Patients (patient_id, patient_name, conditions) VALUES
(1, 'Daniel', 'YFEV COUGH'),
(2, 'Alice', ''),
(3, 'Bob', 'DIAB100 MYOP'),
(4, 'George', 'ACNE DIAB100'),
(5, 'Alain', 'DIAB201');
```

```jsx
[ 정답 ]
SELECT *
FROM PATIENTS
WHERE CONDITIONS REGEXP '^DIAB1| DIAB1'
```

- **해설 :** DIAB1으로 시작하는 문자와 | 키워드를 사용해 DIAB1 문자를 갖는 패턴을 형성합니다. 이 때 마지막 DIAB1앞에 띄어쓰기를 써야 합니다. 그래야 띄어쓰기를 포함한 6개의 문자가 하나의 패턴으로 인식되어 정상 출력이 이루어집니다.
