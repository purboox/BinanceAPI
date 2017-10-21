# Python Binance API

This project provides a Python wrapper of the [Binance API](https://www.binance.com/restapipub.html). As simplicity is the focus of this project, the wrapper is intuitive and easy to use. 

#### Requirements

* python 2.7
* python-requests >= 2.14.0

#### Getting started
```python

from BinanceAPI import *

key = 'your-API-key'
secret = 'your-API-secret'
binance = BinanceAPI(key, secret)
```

#### Getting latest price of a symbol
```python

ret = binance.get_ticker("ETHBTC")
print 'Latest Price: %.8lf' % ret["lastPrice"]
```
<details>
 <summary>View Response</summary>

```
Latest Price: 0.04900000
```
</details>

#### Getting the depth of a symbol, 5 orders per orderbook
```python
binance.get_orderbooks("ETHBTC", 5)
```
<details>
 <summary>View Response</summary>

```js
{
    'lastUpdateId': 18044415, 
    'bids': [
        ['0.04895000', '3.81000000', []], 
        ['0.04894900', '24.39600000', []], 
        ['0.04894800', '3.97400000', []], 
        ['0.04894300', '10.75200000', []], 
        ['0.04892900', '0.84400000', []]
    ], 
    'asks': [
        ['0.04910000', '3.73800000', []], 
        ['0.04914400', '15.00000000', []], 
        ['0.04914700', '28.22000000', []], 
        ['0.04927600', '12.15100000', []], 
        ['0.04935000', '70.00000000', []]
    ]
}
```
</details>

#### Placing a LIMIT order
```python
binance.sell_limit("ETHBTC", 0.1, 1)
```

<details>
 <summary>View Response</summary>

```js
{
    'orderId': 10388204, 
    'clientOrderId': 'PUHmAEVLfYLfYR6637KNlG', 
    'origQty': '0.10000000', 
    'symbol': 'ETHBTC', 
    'side': 'SELL', 
    'timeInForce': 'GTC', 
    'status': 'NEW', 
    'transactTime': 1508557754003, 
    'type': 'LIMIT', 
    'price': '1.00000000', 
    'executedQty': '0.00000000'
}
```
</details>

#### Placing a MARKET order
```python
binance.buy_market("ETHBTC", 0.1)
```

#### Checking an order's status
```python
orderId = 10388204
binance.query_order("ETHBTC", orderId)
```

<details>
 <summary>View Response</summary>

```js
{
    'orderId': 10388204, 
    'clientOrderId': '6SHkb2Oo1d6WHOEvWynhsl', 
    'origQty': '0.10000000', 
    'icebergQty': '0.00000000', 
    'symbol': 'ETHBTC', 
    'side': 'SELL', 
    'timeInForce': 'GTC', 
    'status': 'CANCELED', 
    'stopPrice': '0.00000000', 
    'time': 1508557754003, 
    'type': 'LIMIT', 
    'price': '1.00000000', 
    'executedQty': '0.00000000'
}
```
</details>

#### Canceling an order
```python
orderId = 10388204
binance.cancel("ETHBTC", orderId)

# an error would occur if the order does not exist or is closed
binance.cancel("ETHBTC", orderId)
```

<details>
 <summary>View Response</summary>

```js
{
    'orderId': 10388204, 
    'clientOrderId': '6akmdNpyldQMMr5q9UrOnC', 
    'symbol': 'ETHBTC', 
    'origClientOrderId': '6SHkb2Oo1d6WHOEvWynhsl'
}

{
    'msg': 'UNKNOWN_ORDER', 
    'code': -2011
}
```
</details>

#### Getting a list of open orders
```python
binance.get_open_orders("ETHBTC")
```

<details>
 <summary>View Response</summary>

```js
[
    {
        'orderId': 10388996, 
        'clientOrderId': 'BqE6UXhquxwHKGEK2AMpJL', 
        'origQty': '0.01000000', 
        'icebergQty': '0.00000000', 
        'symbol': 'ETHBTC', 
        'side': 'SELL', 
        'timeInForce': 'GTC', 
        'status': 'NEW', 
        'stopPrice': '0.00000000', 
        'time': 1508558434918, 
        'type': 'LIMIT', 
        'price': '1.00000000', 
        'executedQty': '0.00000000'
    }, 
    {
        'orderId': 10389084, 
        'clientOrderId': 'QoI5XaqhW533pFL5fHxz5V', 
        'origQty': '0.02000000', 
        'icebergQty': '0.00000000', 
        'symbol': 'ETHBTC', 
        'side': 'SELL', 
        'timeInForce': 'GTC', 
        'status': 'NEW', 
        'stopPrice': '0.00000000', 
        'time': 1508558467200, 
        'type': 'LIMIT', 
        'price': '1.00000000', 
        'executedQty': '0.00000000'
    }
]
```
</details>

#### Getting a list of current positions (balances)
```python
binance.get_account()["balances"]
```
<details>
 <summary>View Response</summary>

```js
{
    'buyerCommission':0,
    'canWithdraw':True,
    'takerCommission':10,
    'canTrade':True,
    'makerCommission':10,
    'sellerCommission':0,
    'canDeposit':True,
    'balances':[
        {
            'locked':'0.00000000',
            'asset':'BTC',
            'free':'0.94532595'
        },
        {
            'locked':'0.00000000',
            'asset':'LTC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ETH',
            'free':'0.74797941'
        },
        {
            'locked':'0.00000000',
            'asset':'BNC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ICO',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'NEO',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'BNB',
            'free':'75.57729383'
        },
        {
            'locked':'0.00000000',
            'asset':'123',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'456',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'QTUM',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'EOS',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'SNT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'BNT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'GAS',
            'free':'2.59734164'
        },
        {
            'locked':'0.00000000',
            'asset':'BCC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'BTM',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'USDT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'HCC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'HSR',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'OAX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'DNT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'MCO',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ICN',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ELC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'PAY',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ZRX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'OMG',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'WTC',
            'free':'28.95569000'
        },
        {
            'locked':'0.00000000',
            'asset':'LRX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'YOYO',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'LRC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'LLT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'TRX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'FID',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'SNGLS',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'STRAT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'BQX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'FUN',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'KNC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'CDT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'XVG',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'IOTA',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'SNM',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'LINK',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'CVC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'TNT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'REP',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'CTR',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'MDA',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'MTL',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'SALT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'NULS',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'SUB',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'STX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'MTH',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'CAT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ADX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'PIX',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ETC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ENG',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'ZEC',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'AST',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'1ST',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'GNT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'DGD',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'BAT',
            'free':'0.00000000'
        },
        {
            'locked':'0.00000000',
            'asset':'DASH',
            'free':'0.00000000'
        }
    ]
}
```
</details>

