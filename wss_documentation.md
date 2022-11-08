<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [P2B WSS](#p2b-wss)
  - [General information](#general-information)
  - [Ping and server time](#ping-and-server-time)
    - [Ping](#ping)
    - [Server time](#server-time)
  - [Depth of market](#depth-of-market)
    - [Subscribe](#subscribe)
    - [Unsubscribe](#unsubscribe)
  - [Last price](#last-price)
    - [Subscribe](#subscribe-1)
    - [Unsubscribe](#unsubscribe-1)
  - [Kline (candlestick)](#kline-candlestick)
    - [Subscribe](#subscribe-2)
    - [Unsubscribe](#unsubscribe-2)
  - [Market status](#market-status)
    - [Subscribe](#subscribe-3)
    - [Unsubscribe](#unsubscribe-3)
  - [Deals](#deals)
    - [Subscribe](#subscribe-4)
    - [Unsubscribe](#unsubscribe-4)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# P2B WSS

- - -

## General information

- - -

The base endpoint is: **wss://apiws.p2pb2b.com/**

Connection will be closed by server in cause of inactivity after 100 seconds.

JSON Structure of request message:
```
{"method":"method_name","params":[arg_1, arg_2, arg_n],"id":arbitrary_integer}
```

- - -

## Ping and server time

- - -

### Ping
> Params: None

Request example:
```
{"method":"server.ping","params":[],"id":1}
```

Response example:
```
{
   "error":null,
   "result":"pong",
   "id":1
}
```

- - -

### Server time
Request example:
```
{"method":"server.time","params":[],"id":1}
```

Response example:
```
{
    "error": null,
    "result": 1657618658,   //time in seconds since 1970-01-01
    "id": 2
}
```

## Depth of market

- - -

### Subscribe
> Params: market, limit, interval

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe   |
|limit  |Integer   |Yes   |The value cannot be less than **1** and more than **100**
|interval   |String   |Yes   |Valid values: 0, 0.00000001, 0.0000001, 0.000001, 0.00001, 0.0001, 0.001, 0.01, 0.1. Interval of precision for order.  |

Request example:
```
{"method":"depth.subscribe","params":["BTC_USDT", 10, "0"],"id":1}
```

Update message example:
```
{
    "method": "depth.update",
    "params": [
        false,                          // true - all records, false - new records
        {
            "asks": [                   // side
                [
                    "19509.81",         // price 
                    "0.277"             // amount
                ]
            ]
        },
        "BTC_USDT"
    ],
    "id": null
}
```

- the "true" flag sends each 60 seconds
- the "false" flag sends each 1 second


- - -

### Unsubscribe
> Params: none

Request example:
```
{"method":"depth.unsubscribe","params":[],"id":1}
```

- - -

## Last price

- - -

### Subscribe
> Params: market1, market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |


Request example:
```
{"method":"price.subscribe","params":["ETH_BTC", "BTC_USDT", "ETH_BUSD"],"id":1}
```

Update message example:
```
{
    "method": "price.update",
    "params": [
        "ETH_BTC",      //market
        "0.053836"      //last price
    ],
    "id": null
}
```

- - -

### Unsubscribe
> Params: none

Request example:
```
{"method":"price.unsubscribe","params":[],"id":1}
```

- - -

## Kline (candlestick)

- - -

### Subscribe
> Params: market, period

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Market for subscribe. Subscription is possible for single market in single-stream   |
|period   |Integer   |Yes   |Kline/Candlestick chart intervals: 900, 1800, 3600, 86400 in seconds  |

Request example:
```
{"method":"kline.subscribe","params":["ETH_BTC", 3600],"id":1}
```

Update message example:
```
{
    "method": "kline.update",
    "params": [
        [
            1657648800,             // Kline start time 
            "0.054146",             // Kline open price
            "0.053938",             // Kline close price (current price)
            "0.054146",             // Kline high price
            "0.053911",             // Kline low price
            "596.4674",             // Volume for stock currency
            "32.2298758767",        // Volume for money currency
            "ETH_BTC"               // Market
        ]
    ],
    "id": null
}
```

- - -

### Unsubscribe
> Params: none

Request example:
```
{"method":"kline.unsubscribe","params":[],"id":1}
```

- - -

## Market status
Market statistic for last 24 hours

- - -

### Subscribe
> Params: market1, market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"state.subscribe","params":["ETH_BTC", "BTC_USDT", "ETH_BUSD"],"id":1}
```

Update message example:
```
{
    "method": "state.update",
    "params": [
        "ETH_BTC",
        {
            "high": "0.055774",         // High price for the last 24h
            "close": "0.053679",        // Close price for the last 24h
            "low": "0.053462",          // Low price for the last 24h
            "period": 86400,            // Period 24h
            "last": "0.053679",         // Last price for the last 24h
            "volume": "38463.6132",     // Stock volume for the last 24h
            "open": "0.055682",         // Open price for the last 24h
            "deal": "2091.0038055314"   // Money volume for the last 24h
        }
    ],
    "id": null
}
```

- - -

### Unsubscribe
> Params: none

Request example:
```
{"method":"state.unsubscribe","params":[],"id":1}
```

- - -

## Deals

- - -

### Subscribe
> Params: market1, market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe.  |

Request example:
```
{"method":"deals.subscribe","params":["ETH_BTC", "BTC_USDT", "ETH_BUSD"],"id":1}
```

Update message example:
```
{
    "method": "deals.update",
    "params": [
        "ETH_BTC",
        [
            {
                "id": 4503032979,               // Order_id
                "amount": "0.103",              
                "type": "sell",                 // Side
                "time": 1657661950.8487639,     // Creation time
                "price": "0.05361"              
            },
            {
                "id": 4503032978,
                "amount": "0.522",
                "type": "sell",
                "time": 1657661950.8460829,
                "price": "0.05361"
            }
        ]
    ],
    "id": null
}
```

- - -

### Unsubscribe
> Params: none

Request example:
```
{"method":"deals.unsubscribe","params":[],"id":1}
```
