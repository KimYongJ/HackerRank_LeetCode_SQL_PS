# **Invalid-Tweets**

- [https://leetcode.com/problems/invalid-tweets/](https://leetcode.com/problems/invalid-tweets/)
- **문제 :** CONTENT가 15글자를 초과하는 트윗 아이디를 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Tweets (
    tweet_id INT,
    content VARCHAR(280)
);
INSERT INTO Tweets (tweet_id, content) VALUES
(1, 'Vote for Biden'),
(2, 'Let us make America great again!');
```

```jsx
[ 정답 ]
SELECT TWEET_ID
FROM TWEETS
WHERE LENGTH(CONTENT) > 15
```

- **해설 :** LENGTH 함수로 길이를 구해 해결했습니다.
