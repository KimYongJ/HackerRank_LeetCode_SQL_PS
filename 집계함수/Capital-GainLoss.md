# **Capital-Gain/Loss**

- [https://leetcode.com/problems/capital-gainloss/](https://leetcode.com/problems/capital-gainloss/)
- **문제 :** **Stocks** 테이블이 주어집니다. 이 테이블에는 각 주식의 이름, 거래 종류(매수 또는 매도), 거래 일자, 가격 정보가 들어 있습니다. 'operation' 열은 ENUM 타입으로 'Buy'와 'Sell' 값을 가질 수 있습니다. 주어진 문제에서는 각 주식에 대한 총 수익률(총 자본 이득/손실)을 계산해야 합니다. 자본 이득/손실은 주식을 매수한 가격과 매도한 가격의 차이를 통해 계산되며, 주식이 여러 번 거래될 수 있습니다. 각 'Sell' 연산에 대해서는 이전의 'Buy' 연산이 반드시 있으며, 해당 'Buy' 연산에 대한 매칭되는 'Sell' 연산이 있음이 보장됩니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Stocks (
    stock_name VARCHAR(255),
    operation ENUM('Buy', 'Sell'),
    operation_day INT,
    price INT
);
INSERT INTO Stocks (stock_name, operation, operation_day, price) VALUES
('Ledcode', 'Buy', 1, 1000),
('Corona Masks', 'Buy', 1, 100),
('Ledcode', 'Sell', 5, 5000),
('Handbags', 'Buy', 1, 7000),
('Handbags', 'Sell', 5, 9000),
('Corona Masks', 'Sell', 1, 1000),
('Corona Masks', 'Buy', 4, 1000),
('Corona Masks', 'Sell', 5, 1500),
('Corona Masks', 'Buy', 6, 1000),
('Corona Masks', 'Sell', 6, 700),
('Handbags', 'Buy', 1, 10000),
('Handbags', 'Sell', 1, 10000);
```

```jsx
[ 정답 ]
SELECT	STOCK_NAME
,		SUM(CASE WHEN OPERATION='Buy' THEN -PRICE ELSE PRICE END) CAPITAL_GAIN_LOSS
FROM STOCKS
GROUP BY STOCK_NAME
```

- **해설 :** 사고 판금액을 SUM해주면 되는 문제입니다. 단 매수일 때는 PRICE를 음수로 바꿔주어 차익에 대해 계산할 수 있도록 했습니다.
