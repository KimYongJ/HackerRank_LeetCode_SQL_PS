# **Reformat-Department-Table**

- [https://leetcode.com/problems/reformat-department-table/](https://leetcode.com/problems/reformat-department-table/)
- **문제 :** 이 문제는 피벗 문제로 행을 컬럼으로 옮기는 문제입니다. ID별로 매달마다의 REVENUE값을 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Department (
  id INT,
  revenue INT,
  month VARCHAR(3)
);
INSERT INTO Department (id, revenue, month) VALUES
(1, 8800, 'Jan'),
(2, 9800, 'Jan'),
(1, 7800, 'Feb'),
(3, 10000, 'Feb'),
(1, 6600, 'Mar'),
(2, 7600, 'Mar'),
(3, 8400, 'Apr'),
(1, 5200, 'Apr'),
(2, 6300, 'May'),
(3, 7200, 'May'),
(1, 5900, 'Jun'),
(2, 6900, 'Jun'),
(3, 8100, 'Jul'),
(1, 5600, 'Jul'),
(2, 7600, 'Aug'),
(3, 8700, 'Aug'),
(1, 5400, 'Sep'),
(2, 6500, 'Sep'),
(3, 7300, 'Oct'),
(1, 5800, 'Oct'),
(2, 6700, 'Nov'),
(3, 7900, 'Nov'),
(1, 6400, 'Dec'),
(2, 6900, 'Dec');
```

```jsx
[ 정답(1) ]
select	ID
,		MAX(case when dp.month = 'Jan' then dp.revenue else null end)Jan_Revenue
,		MAX(case when dp.month = 'Feb' then dp.revenue else null end)Feb_Revenue
,		MAX(case when dp.month = 'Mar' then dp.revenue else null end)Mar_Revenue
,		MAX(case when dp.month = 'Apr' then dp.revenue else null end)Apr_Revenue
,		MAX(case when dp.month = 'May' then dp.revenue else null end)May_Revenue
,		MAX(case when dp.month = 'Jun' then dp.revenue else null end)Jun_Revenue
,		MAX(case when dp.month = 'Jul' then dp.revenue else null end)Jul_Revenue
,		MAX(case when dp.month = 'Aug' then dp.revenue else null end)Aug_Revenue
,		MAX(case when dp.month = 'Sep' then dp.revenue else null end)Sep_Revenue
,		MAX(case when dp.month = 'Oct' then dp.revenue else null end)Oct_Revenue
,		MAX(case when dp.month = 'Nov' then dp.revenue else null end)Nov_Revenue
,		MAX(case when dp.month = 'Dec' then dp.revenue else null end)Dec_Revenue
from department DP
group by id

[ 정답(2) ]
select	ID
,		MAX(Jan_Revenue)Jan_Revenue
,		MAX(Feb_Revenue)Feb_Revenue
,		MAX(Mar_Revenue)Mar_Revenue
,		MAX(Apr_Revenue)Apr_Revenue
,		MAX(May_Revenue)May_Revenue
,		MAX(Jun_Revenue)Jun_Revenue
,		MAX(Jul_Revenue)Jul_Revenue
,		MAX(Aug_Revenue)Aug_Revenue
,		MAX(Sep_Revenue)Sep_Revenue
,		MAX(Oct_Revenue)Oct_Revenue
,		MAX(Nov_Revenue)Nov_Revenue
,		MAX(Dec_Revenue)Dec_Revenue
from (
		select	case when dp.month = 'Jan' then dp.revenue else null end Jan_Revenue
		,		case when dp.month = 'Feb' then dp.revenue else null end Feb_Revenue
		,		case when dp.month = 'Mar' then dp.revenue else null end Mar_Revenue
		,		case when dp.month = 'Apr' then dp.revenue else null end Apr_Revenue
		,		case when dp.month = 'May' then dp.revenue else null end May_Revenue
		,		case when dp.month = 'Jun' then dp.revenue else null end Jun_Revenue
		,		case when dp.month = 'Jul' then dp.revenue else null end Jul_Revenue
		,		case when dp.month = 'Aug' then dp.revenue else null end Aug_Revenue
		,		case when dp.month = 'Sep' then dp.revenue else null end Sep_Revenue
		,		case when dp.month = 'Oct' then dp.revenue else null end Oct_Revenue
		,		case when dp.month = 'Nov' then dp.revenue else null end Nov_Revenue
		,		case when dp.month = 'Dec' then dp.revenue else null end Dec_Revenue
		,		dp.id
		from department dp
)DP
group by id
```

- **해설 :** 정답(2)는 정답(1)을 풀어서 적어본 것입니다. CASE WHEN 구문으로 해당 행을 가로로 출력한 다음, ID를 기준으로 GROUP으로 묶습니다. GROUP BY에 ID만 적어주었기 때문에 나머지를 출력하기 위해서는 집계함수를 사용해 출력해야 합니다. MIN, MAX, SUM 어떤것을 적어도 상관없이 잘 출력됩니다. 아래 사진은 정답(2)의 서브 쿼리 실행 결과 입니다. 아래 사진의 실행 결과를 통해 GROUP BY 를 ID 기준으로 했다 생각하면 이해하기 쉽습니다.
- 사진(1)
