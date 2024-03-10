# **Article-Views-I**

- [https://leetcode.com/problems/article-views-i/](https://leetcode.com/problems/article-views-i/)
- **문제 :** 자신이 작성한 글을 본 저자들의 목록을 찾는 것입니다. author_id를 오름차순으로 출력하며 author_id 컬럼은 작가id, viewer_id는 글을 본 저자 아이디 입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Views (
  article_id INT,
  author_id INT,
  viewer_id INT,
  view_date DATE
);
INSERT INTO Views (article_id, author_id, viewer_id, view_date) VALUES
(1, 5, 5, '2019-08-01'),
(1, 3, 6, '2019-08-02'),
(2, 7, 7, '2019-08-01'),
(2, 7, 6, '2019-08-02'),
(4, 1, 1, '2019-07-22'),
(3, 4, 4, '2019-07-21'),
(3, 4, 4, '2019-07-21');
```

```jsx
[ 정답 ]
SELECT DISTINCT AUTHOR_ID ID
FROM VIEWS
WHERE AUTHOR_ID = VIEWER_ID
ORDER BY AUTHOR_ID
```

- **해설 :** AUTHOR_ID 컬럼과 VIEWER_ID 컬럼이 같은 것을 출력합니다. 이 때 AUTHOR_ID ID의 중복 출력을 막기 위해 중복 제거 키워드인 distinct를 사용합니다.
