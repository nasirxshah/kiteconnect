# kiteconnect
Unofficial Python client for communicating with the [Kite Connect API](https://kite.trade).

Kite Connect is a set of REST-like APIs that expose many capabilities required to build a complete investment and trading platform. Execute orders in real time, manage user portfolio, stream live market data (WebSockets), and more, with the simple HTTP API collection.



## API usage

```python
import logging
from kiteconnect import KiteConnect, KiteSession


logging.basicConfig(level=logging.DEBUG)



ksession = KiteSession(user_id="your user id")
cookies = ksession.generate_session("password","pin: two factor auth")


kite = KiteConnect()
kite.set_cookies(cookies)

# Place an order
try:
    order_id = kite.place_order(
        variety=kite.VARIETY_REGULAR,
        exchange=kite.EXCHANGE_NSE,
        tradingsymbol="INFY",
        transaction_type=kite.TRANSACTION_TYPE_BUY,
        quantity=1,
        product=kite.PRODUCT_CNC,
        order_type=kite.ORDER_TYPE_MARKET
    )

    logging.info("Order placed. ID is: {}".format(order_id))
except Exception as e:
    logging.info("Order placement failed: {}".format(e.message))

# Fetch all orders
kite.orders()
```