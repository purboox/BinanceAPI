# Binance API

Examples: 

```
from BinanceAPI import *

def errexit(msg):
    print("Error: " + msg)
    exit(1)


key = 'your-API-key'
secret = 'your-API-secret'
binance = BinanceAPI(key, secret)

symbol = "ETHBTC"


# 1. Get the lastest price of a symbol
ret = binance.get_ticker(symbol)
if 'msg' in ret:
    errexit(ret['msg'])

lastPrice = float(ret["lastPrice"])
print 'Latest Price: %lf\n' % lastPrice


# 2. Get the depth of a symbol, 5 orders per orderbook
ret = binance.get_orderbooks(symbol, 5)
if 'msg' in ret:
    errexit(ret['msg'])

print 'Bids:'
for (price, volume, dummy) in ret['bids']:
    print '%lf\t%lf' % (float(price), float(volume))

print 'Asks: '
for (price, volume, dummy) in ret['asks']:
    print '%lf\t%lf' % (float(price), float(volume))
print ''


# 3. Place a LIMIT order
ret = binance.buy_limit(symbol, 0.1, 0.01)
if 'msg' in ret:
    errexit(ret['msg'])

orderId = ret['orderId']
print 'Limit order %d has been placed.' % orderId


# 4. Place a MARKET order
ret = binance.sell_market(symbol, 0.1)
if 'msg' in ret:
    errexit(ret['msg'])

orderId = ret['orderId']
print 'Market order %d has been placed. ' % orderId


# 5. Check an order's status
ret = binance.query_order(symbol, orderId)
if 'msg' in ret:
    errexit(ret['msg'])

print 'Order status: ' + ret['status']


# 6. Cancel an order
ret = binance.cancel(symbol, orderId)
if 'msg' in ret:
    errexit(ret['msg'])

print 'Order has been canceled.'


# 7. Get a list of open orders
ret = binance.get_open_orders(symbol)
if 'msg' in ret:
    errexit(ret['msg'])

for order in ret:
    orderId = order['orderId']
    price = float(order['price'])
    origQty = float(order['origQty'])
    executedQty = float(order['executedQty'])
    print "%d: %lf\t%lf\t%lf" % (orderId, price, origQty, executedQty)
print ''


# 8. Get balances
ret = binance.get_account()
if 'msg' in ret:
    errexit(ret['msg'])

print 'Balances: '
for entry in ret['balances']:
    print '%s: %s' % (entry['asset'], entry['free'])

```

