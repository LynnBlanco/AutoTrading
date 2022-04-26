# Auto Trading
NCKU DSAI HW2 - Auto Trading

We will implement a very aged prediction problem from the financial field. Given a series of stock prices, including daily open, high, low, and close prices, decide your daily action and make your best profit for the future trading.

We will use one month’s data as the test data set. Aim to maximize revenue in 20 days.

## Data Analysis
- ```Training data``` 趨勢圖，```close```, ```open```, ```high```, ```low``` 
<img src="https://github.com/LynnBlanco/AutoTrading/blob/81187bea8c687f371b8196738ccfbb6b71285123/images/Figure_1.png" width="600px"/>

- ```Testing data``` 趨勢圖，```close```, ```open```, ```high```, ```low```
<img src="https://github.com/LynnBlanco/AutoTrading/blob/81187bea8c687f371b8196738ccfbb6b71285123/images/Figure_2.png" width="600px"/>


## Model Training
本次使用 ```LSTM``` 模型，LSTM 常用於預測帶有時間序列的資料。我們使用 ```open```, ```close``` 作為特徵來訓練模型，因為要預測的目標是20日的股票開盤價錢，所以我們在訓練時以每20筆訓練資料來預測1筆資料的方式進行。

- Model summary
<img src="https://github.com/LynnBlanco/AutoTrading/blob/81187bea8c687f371b8196738ccfbb6b71285123/images/Figure_5.png" width="500px"/>

- Predict
<img src="https://github.com/LynnBlanco/AutoTrading/blob/81187bea8c687f371b8196738ccfbb6b71285123/images/Figure_4.png" width="600px"/>


## Trader Strategy
以目前持股數量為0、1或-1，並以買入之收盤價與預測收盤價做比較，以此為依據來判斷動作為買、賣或持有，並記錄每一次買入時所花費的價錢。

在20天中，將買入股票的開盤價與預測的開盤價做比較，當價差大於時則賣出，反之則持有。

|持股數量  |開盤價比較  |股票買賣  |
|:-------:|:-------:|:--------:|
|0 |預測開盤價 < 前一日開盤價 |1 |
|0 |預測開盤價 > 前一日開盤價 |-1|
|1 |預測開盤價 < 買進開盤價   |0 |
|1 |預測開盤價 > 買進開盤價   |-1|
|-1|預測開盤價 < 賣空開盤價   |1 |
|-1|預測開盤價 > 賣空開盤價   |0 |


## Code Execution
Environment: ```Python 3.7.13``` </br>

- Install ```requirements.txt```
```
$ pip install -r requirements.txt
```
- Execute ```app.py```
```
$ python app.py --training training.csv --testing testing.csv --output output.csv
```
