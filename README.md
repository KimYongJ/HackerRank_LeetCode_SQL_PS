# SQL_ps

해커랭크, 리트코트 SQL 문제 풀이

## MySQL로 문제를 풀었습니다.

- [https://www.hackerrank.com/dashboard](https://www.hackerrank.com/dashboard)
- [https://leetcode.com/problemset/](https://leetcode.com/problemset/)

- **정규 표현식을 연습할 수 있는 사이트 : [https://regexone.com/lesson/introduction_abcs](https://regexone.com/lesson/introduction_abcs)**
- **정규 표현식 실시간 확인할 수 있는 사이트 : [https://regexr.com/](https://regexr.com/)**

# SQL 표준 실행 순서

1. **FROM:** 먼저 **FROM** 절이 실행되어 쿼리가 참조할 테이블이나 뷰, 서브쿼리를 결정합니다. 여기서 지정된 테이블들의 데이터는 다음 단계들에 사용됩니다.
2. **JOIN:** **FROM** 절 다음에 **JOIN**이 실행되어 테이블 간의 결합이 이루어집니다. **JOIN**의 조건이 평가되어 어떤 행들이 결합될지 결정합니다.
3. **WHERE**: **JOIN** 다음으로 실행되어 주어진 조건에 맞는 행들을 필터링합니다. **WHERE** 절은 **GROUP BY**, **HAVING**, **SELECT** 절에 앞서 처리되기 때문에, 그 이후 단계에서 처리되는 양을 줄여줍니다.
4. **GROUP BY**: **WHERE** 절에 의해 필터링 된 결과를 기반으로 **GROUP BY**가 실행되어 지정된 컬럼 값을 기준으로 행들을 그룹화합니다.
5. **HAVING**: **GROUP BY**에 의해 형성된 그룹들에 대하여 추가적인 필터를 적용합니다. 이 조건은 각 그룹에 대한 집계 함수의 결과를 기반으로 한 필터링을 수행합니다.
6. **SELECT**: 위 단계를 지난 후 필요한 컬럼들을 선택합니다. **SELECT** 절의 집계 함수도 이 단계에서 계산됩니다.
7. **DISTINCT**: **SELECT**에 **DISTINCT**가 사용된 경우, 중복 값을 제거합니다.
8. **ORDER BY**: 거의 마지막 단계로 **ORDER BY**가 실행되어 결과 집합을 지정된 순서대로 정렬합니다.
9. **LIMIT** / **OFFSET**: 마지막으로, 쿼리 결과의 특정 범위를 반환하기 위해 **LIMIT** 및 **OFFSET**이 적용됩니다.
