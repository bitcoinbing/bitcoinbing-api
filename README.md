# Bitcoinbing Public Rest API

## General API Information
1. Base API Endpoint: https://publicapi.bitcoinbing.io
2. All public api will return either JSON or Array object.
3. Data is returned in descending order. Newest first, oldest last.
4. All time and timestamp related fields are in seconds.

### Public API

1. #### MARKET STATUS
   GET `/api/public/market-status`  [Live link](https://publicapi.bitcoinbing.io/api/public/market-status)

    > "Market Status" will give your an overview of markets and assets. This is helpful when you want to track the configuration of our markets, track fees or status of withdrawal deposit, market configuration and more. This response is not recommended for price polling because accurate realtime price is not guaranteed as there could be some delays. We recommend using price ticker API for all price tracking activity.
    
    Response object will have 2 keys `Markets`(all market related configs will be in this key) and `Assets`(all assets related configs will be here). 
    ### Response:
    ```
    {
        "Markets": [
            {
              "coin": "BTC",
              "pair": "USDT",
              "fee": 0.0025,
              "basePrecision": 0,
              "quotePrecision": 8,
              "minBuyAmount": 5.0,
              "minSellAmount": 5.0,
              "tradingStatus": "enable",
              "low": 9776.53700514,
              "high": 10957.42273101,
              "close": 10844.70389819,
              "open": 10648.15092657,
              "volumefrom": "272,755.19589541",
              "volumeto": "534,223.16923906",             
              "timestamp": 1562146720
            },
            ...
        ],
        "Assets": [
            {
                "coin": "BTC",
                "name": "Bitcoin",
                "deposit": "enable",
                "withdrawal": "enable",
                "minWithdrawalAmount": "0.002",
                "withdrawalFee": "0.001"                
            },
            ...
        ]
    }
    ```
    
    
    1. **`Markets` key has multiple market related configuration, and description of every field in market is as below:**
    
        1. `coin`: Coin name.
        1. `pair`: Pair name.
        1. `fee`: Fee consists of `buy` and `sell` order's fee percentage.
        1. `basePrecision`: Maximum precision of base asset, this the decimal point.
        1. `quotePrecision`: Maximum  precision of quote asset.
        1. `minBuyAmount`: Minimum buy amount of base asset.
        1. `minSellAmount`: Minumum sell amount of base asset.
        1. `tradingStatus`:Trading Status.
        1. `low`: 24 hrs lowest price of base coin & pair.
        1. `high`: 24 hrs highest price of base coin & pair.
        1. `close`: Last traded price in current market.
        1. `open`: Market Open price 24hrs ago.
        1. `volumefrom`: Previous 24hrs traded volume.
        1. `volumeto`: Current traded volume.            
        1. `timestamp`: Timestamp when information is fetched.
    1. **`Assets` key have multiple asset related configuration as described below:**
    
        1. `coin`: Coin name.
        1. `name`: Display name of asset.
        1. `deposit`: Denotes whether deposit is enabled or disabled.
        1. `withdrawal`: Denotes whether withdrawal is enabled or disabled.
        1. `minWithdrawAmount`: Minimum withdrawal amount in a single transaction.
        1. `withdrawFee`: Withdrawal fee of asset.
              
        


1. #### MARKET TICKER
   GET `/api/public/market-ticker` [Live link](https://publicapi.bitcoinbing.io/api/public/market-ticker)
    > Get the latest market heart-beat for all the markets for the last 24hrs.
    
    Returns JSON response which has active market data with all ticker related values.
    ### Response:
    ```
    {
        "btcusdt": {
          "coin": "BTC",
          "pair": "USDT",
          "name": "BTC/USDT",
          "buy": 11106.69555345,
          "sell": 11139.17860952,
          "low": 9776.53700514,
          "high": 10957.42273101,
          "close": 10844.70389819,
          "open": 10648.15092657,
          "volume": "534,223.16923906",
          "timestamp": 1562148430
        },
        ...
    }
    ```
    Response has multiple key which denotes market data, this is in JSON. Find all the fields below:
    
    1. `coin`: Coin name
    1. `pair`: Pair name
    1. `name`: Display text.
    1. `buy`: Last buy order price
    1. `sell`: Last sell order price
    1. `low`: 24 hrs lowest price of base asset
    1. `high`: 24 hrs highest price of base asset
    1. `close`: Last traded price in current market
    1. `open`: Market Open price 24hrs ago
    1. `volume`: Last 24hrs traded volume
    1. `timestamp`: Timestamp when ticker information is fetched
    
      
    

1. #### MARKET DEPTH
   GET `/api/public/market-depth` [Live link](https://publicapi.bitcoinbing.io/api/public/market-depth?fsym=BTC&tsym=USDT)
    > Get last 25 orders for any market
    
    Returns JSON response which has order book of a perticular market
    ### Response:
    ```
    {
    "buy":[
                [
                  "11,389.20344241",
                  "0.00263210"
                ],
                ...
           ],
    "sell":[
               [
                 "11,394.37373348",
                 "0.00360129"
               ],
               ...
           ],
     "timestamp":1559561187,
    }
    
    ```
    1. `["11,389.20344241","0.00263210"]` : [ PRICE, AMOUNT ]
    1. URL param `fsym=BTC&tsym=USDT` : Replace this with any market to get the desired order book.
                                        fsym='COIN_NAME' and tsym='PAIR_NAME'
    
1. #### TRADE HISTORY
   GET `api/public/trading-history` [Live link](https://publicapi.bitcoinbing.io/api/public/trading-history?fsym=BTC&tsym=USDT)
    > Get trade history of a market
    
    Returns JSON response which has trade history of a perticular market
    ### Response:
    ```
    [
      {
         "code": "BTC",
         "pair": "USDT",
         "type": "Buy",
         "price": "11,412.51340509",
         "amount": "0.00305040",
         "timestamp": "1562149565"
       }  
   ...
   ]
    ```
    1. URL param `fsym=BTC&tsym=USDT` : Replace this with any market to get the desired order book.
                                        fsym='COIN_NAME' and tsym='PAIR_NAME'
    
    
If you have any questions regarding APIs, please reach out to us at support@bitcoinbing.io
