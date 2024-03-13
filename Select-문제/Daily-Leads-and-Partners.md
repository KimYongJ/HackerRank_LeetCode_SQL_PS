# **Daily-Leads-and-Partners**

- [https://leetcode.com/problems/daily-leads-and-partners/](https://leetcode.com/problems/daily-leads-and-partners/)
- **문제 :** 특정 날짜(date_id)와 제품(make_name)에 대해 고유 리드(id)와 파트너(id)의 수를 찾아야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE DailySales (
    date_id DATE,
    make_name VARCHAR(255),
    lead_id INT,
    partner_id INT
);
INSERT INTO DailySales (date_id, make_name, lead_id, partner_id) VALUES
('2020-12-08', 'toyota', 0, 1),
('2020-12-08', 'toyota', 1, 1),
('2020-12-08', 'toyota', 0, 2),
('2020-12-08', 'toyota', 1, 2),
('2020-12-08', 'toyota', 0, 1),
('2020-12-08', 'toyota', 1, 1),
('2020-12-08', 'honda', 0, 2),
('2020-12-08', 'honda', 1, 2),
('2020-12-08', 'honda', 2, 2),
('2020-12-08', 'honda', 1, 1),
('2020-12-08', 'honda', 0, 1),
('2020-12-08', 'honda', 1, 2);
```

```jsx
[ 정답 ]
SELECT  DATE_ID
,       MAKE_NAME
,       COUNT(DISTINCT LEAD_ID) unique_leads
,       COUNT(DISTINCT PARTNER_ID) unique_partners
FROM DAILYSALES
GROUP BY DATE_ID, MAKE_NAME
```

- **해설 :** 특정 날짜와 제품을 그룹화한 후 중복을 제거한 LEAD_ID와 PARTNER_ID를 출력합니다. 이 때 COUNT 함수 안에 DISTINCT 키워드가 들어가면 같은 값을 가지는 컬럼은 제거하고 수를 집계합니다.
