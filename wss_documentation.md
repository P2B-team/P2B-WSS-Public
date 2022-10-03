<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [P2B WSS Public (14.07.2022)](#p2b-wss-public-14072022)
  - [General WSS information](#general-wss-information)
  - [Ping and server time query](#ping-and-server-time-query)
    - [Ping](#ping)
    - [Server time](#server-time)
  - [Subscribing/unsubscribing to depth update for market](#subscribingunsubscribing-to-depth-update-for-market)
    - [Subscription to depth update for market](#subscription-to-depth-update-for-market)
    - [Unsubscription to depth update for market](#unsubscription-to-depth-update-for-market)
  - [Subscribing/unsubscribing to the last price for markets](#subscribingunsubscribing-to-the-last-price-for-markets)
    - [Subscription to last price updating for btc-like markets](#subscription-to-last-price-updating-for-btc-like-markets)
    - [Unsubscription to last price updating for btc-like markets](#unsubscription-to-last-price-updating-for-btc-like-markets)
    - [Subscription to last price updating for eth-like markets](#subscription-to-last-price-updating-for-eth-like-markets)
    - [Unsubscription to last price updating for eth-like markets](#unsubscription-to-last-price-updating-for-eth-like-markets)
    - [Subscription to last price updating for oth-like markets](#subscription-to-last-price-updating-for-oth-like-markets)
    - [Unsubscription to last price updating for oth-like markets](#unsubscription-to-last-price-updating-for-oth-like-markets)
    - [Unsubscription to last price updating for all markets types](#unsubscription-to-last-price-updating-for-all-markets-types)
  - [Subscribing/unsubscribing to the last kline (candlestick) bars for market](#subscribingunsubscribing-to-the-last-kline-candlestick-bars-for-market)
    - [Subscription to the last kline (candlestick) bars for btc-like market](#subscription-to-the-last-kline-candlestick-bars-for-btc-like-market)
    - [Unsubscription to the last kline (candlestick) bars for btc-like market](#unsubscription-to-the-last-kline-candlestick-bars-for-btc-like-market)
    - [Subscription to the last kline (candlestick) bars for eth-like market](#subscription-to-the-last-kline-candlestick-bars-for-eth-like-market)
    - [Unsubscription to the last kline (candlestick) bars for eth-like market](#unsubscription-to-the-last-kline-candlestick-bars-for-eth-like-market)
    - [Subscription to the last kline (candlestick) bars for oth-like market](#subscription-to-the-last-kline-candlestick-bars-for-oth-like-market)
    - [Unsubscription to the last kline (candlestick) bars for oth-like market](#unsubscription-to-the-last-kline-candlestick-bars-for-oth-like-market)
    - [Unsubscription to the last kline (candlestick) bars for all market types](#unsubscription-to-the-last-kline-candlestick-bars-for-all-market-types)
  - [Subscribing/unsubscribing to state update](#subscribingunsubscribing-to-state-update)
    - [Subscription to the state update for btc-like markets](#subscription-to-the-state-update-for-btc-like-markets)
    - [Unsubscription to the state update for btc-like markets](#unsubscription-to-the-state-update-for-btc-like-markets)
    - [Subscription to the state update for eth-like markets](#subscription-to-the-state-update-for-eth-like-markets)
    - [Unsubscription to the state update for eth-like markets](#unsubscription-to-the-state-update-for-eth-like-markets)
    - [Subscription to the state update for oth-like markets](#subscription-to-the-state-update-for-oth-like-markets)
    - [Unsubscription to the state update for oth-like markets](#unsubscription-to-the-state-update-for-oth-like-markets)
    - [Unsubscription to the state update for all markets](#unsubscription-to-the-state-update-for-all-markets)
  - [Subscribing/unsubscribing to deals update for markets](#subscribingunsubscribing-to-deals-update-for-markets)
    - [Subscription to deals update for btc-like markets](#subscription-to-deals-update-for-btc-like-markets)
    - [Unsubscription to deals update for btc-like markets](#unsubscription-to-deals-update-for-btc-like-markets)
    - [Subscription to deals update for eth-like markets](#subscription-to-deals-update-for-eth-like-markets)
    - [Unsubscription to deals update for eth-like markets](#unsubscription-to-deals-update-for-eth-like-markets)
    - [Subscription to deals update for oth-like markets](#subscription-to-deals-update-for-oth-like-markets)
    - [Unsubscription to deals update for oth-like markets](#unsubscription-to-deals-update-for-oth-like-markets)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# P2B WSS Public (14.07.2022)

- - -

## General WSS information

- - -

The base endpoint is: **wss://apiws.p2pb2b.com/**

For subscribe to price, kline, state, 
Is 3 types of markets. 
* If market like TICKER_BTC - is BTC market type, e.g. ETH_BTC, BNB_BTC, etc;
* If market like TICKER_ETH - is ETH market type. e.g. BNB_ETH, WAVES_ETH, etc;
* All other markets - is OTH market type, e.g. BTC_USDT, ETH_BUSD, etc.

Further, in the documentation: btc-like, eth-like, or oth-like market.

Connection will be closed by server in cause of inactivity after 60s.

JSON Structure of request message:
```
{"method":"method_name","params":[arg_1, arg_2, arg_n],"id":arbitrary_integer}
```

- - -

## Ping and server time query

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
{"method":"server.time","params":[],"id":2}
```

Response example:
```
{
    "error": null,
    "result": 1657618658,   //time in seconds since 1970-01-01
    "id": 2
}
```

## Subscribing/unsubscribing to depth update for market

- - -

### Subscription to depth update for market
> Params: market, limit, interval

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for one market in single-stream   |
|limit  |Integer   |Yes   |The value cannot be less than **1** and more than **100**
|interval   |String   |Yes   |Valid values: 0, 0.00000001, 0.0000001, 0.000001, 0.00001, 0.0001, 0.001, 0.01, 0.1. Interval of precision for order merge.  |

Request example:
```
{"method":"depth.subscribe","params":["BTC_USDT", 10, "0"],"id":3}
```

Update message example:
```
{
    "method": "depth.update",
    "params": [
        false,                          // last depth cleaning is now or not
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

- - -

### Unsubscription to depth update for market
> Params: none

Request example:
```
{"method":"depth.unsubscribe","params":[],"id":4}
```

- - -

## Subscribing/unsubscribing to the last price for markets
Is used to get the last price for the market. Update messages are pushed if the price is updated.
Available subscription for more than one market.
- - -

### Subscription to last price updating for btc-like markets
> Params: btc_like_market1, btc_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |


Request example:
```
{"method":"price.subscribe_btc","params":["ETH_BTC"],"id":5}
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

### Unsubscription to last price updating for btc-like markets
> Params: none

Request example:
```
{"method":"price.unsubscribe_btc","params":[],"id":6}
```

- - -

### Subscription to last price updating for eth-like markets
> Params: eth_like_market1, eth_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"price.subscribe_eth","params":["LTC_ETH"],"id":7}
```

Update message example:
```
{
    "method": "price.update",
    "params": [
        "LTC_ETH",
        "0.04509"
    ],
    "id": null
}
```

- - -

### Unsubscription to last price updating for eth-like markets
> Params: none

Request example:
```
{"method":"price.unsubscribe_eth","params":[],"id":8}
```

- - -

### Subscription to last price updating for oth-like markets
> Params: oth_like_market1, oth_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"price.subscribe_oth","params":["BTC_BUSD"],"id":9}
```

Update message example:
```
{
    "method": "price.update",
    "params": [
        "BTC_BUSD",
        "19639.94"
    ],
    "id": null
}
```

- - -

### Unsubscription to last price updating for oth-like markets
> Params: none

Request example:
```
{"method":"price.unsubscribe_oth","params":[],"id":10}
```

- - -

### Unsubscription to last price updating for all markets types
> Params: none

Request example:
```
{"method":"price.unsubscribe_all","params":[],"id":11}
```

- - -

## Subscribing/unsubscribing to the last kline (candlestick) bars for market

- - -

### Subscription to the last kline (candlestick) bars for btc-like market
> Params: btc_like_market, period

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Market for subscribe. Subscription is possible for one market in single-stream   |
|period   |Integer   |Yes   |Kline/Candlestick chart intervals: 900, 1800, 3600, 86400   |

Request example:
```
{"method":"kline.subscribe_btc","params":["ETH_BTC", 3600],"id":12}
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

### Unsubscription to the last kline (candlestick) bars for btc-like market
> Params: none

Request example:
```
{"method":"kline.unsubscribe_btc","params":[],"id":13}
```

- - -

### Subscription to the last kline (candlestick) bars for eth-like market
> Params: eth_like_market, period

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Market for subscribe. Subscription is possible for one market in single-stream   |
|period   |Integer   |Yes   |Kline/Candlestick chart intervals: 900, 1800, 3600, 86400   |

Request example:
```
{"method":"kline.subscribe_eth","params":["BNB_ETH", 3600],"id":14}
```

Update message example:
```
{
    "method": "kline.update",
    "params": [
        [
            1657656000,
            "0.2135",
            "0.2132",
            "0.2136",
            "0.2125",
            "229.939",
            "48.98320607",
            "BNB_ETH"
        ]
    ],
    "id": null
}
```

- - -

### Unsubscription to the last kline (candlestick) bars for eth-like market
> Params: none

Request example:
```
{"method":"kline.unsubscribe_eth","params":[],"id":15}
```

- - -

### Subscription to the last kline (candlestick) bars for oth-like market
> Params: oth_like_market, period

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Market for subscribe. Subscription is possible for one market in single-stream   |
|period   |Integer   |Yes   |Kline/Candlestick chart intervals: 900, 1800, 3600, 86400   |

Request example:
```
{"method":"kline.subscribe_oth","params":["BTC_USDT",3600],"id":16}
```

Update message example:
```
{
    "method": "kline.update",
    "params": [
        [
            1657656000,
            "19403.12",
            "19410.29",
            "19474.19",
            "19385.5",
            "689.748784",
            "13401735.25736168",
            "BTC_USDT"
        ]
    ],
    "id": null
}
```

- - -

### Unsubscription to the last kline (candlestick) bars for oth-like market
> Params: none

Request example:
```
{"method":"kline.unsubscribe_oth","params":[],"id":17}
```

- - -

### Unsubscription to the last kline (candlestick) bars for all market types
> Params: none

Request example:
```
{"method":"kline.unsubscribe_all","params":[],"id":18}
```

- - -

## Subscribing/unsubscribing to state update
Market status for last 24 hours

- - -

### Subscription to the state update for btc-like markets
> Params: btc_like_market1, btc_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"state.subscribe_btc","params":["ETH_BTC"],"id":19}
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

### Unsubscription to the state update for btc-like markets
> Params: none

Request example:
```
{"method":"state.unsubscribe_btc","params":[],"id":20}
```

- - -

### Subscription to the state update for eth-like markets
> Params: eth_like_market1, eth_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"state.subscribe_eth","params":["BNB_ETH"],"id":21}
```

Update message example:
```
{
    "method": "state.update",
    "params": [
        "BNB_ETH",
        {
            "low": "0.20927",
            "last": "0.2107",
            "period": 86400,
            "close": "0.2107",
            "high": "0.2141",
            "volume": "15189.947",
            "open": "0.2095",
            "deal": "3213.38824163"
        }
    ],
    "id": null
}
```

- - -

### Unsubscription to the state update for eth-like markets
> Params: none

Request example:
```
{"method":"state.unsubscribe_eth","params":[],"id":22}
```

- - -

### Subscription to the state update for oth-like markets
> Params: oth_like_market1, oth_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"state.subscribe_oth","params":["ETH_USDT"],"id":23}
```

Update message example:
```
{
    "method": "state.update",
    "params": [
        "ETH_USDT",
        {
            "deal": "322201138.0683717",
            "low": "1033.46",
            "last": "1073.4",
            "period": 86400,
            "open": "1067.76",
            "volume": "303637.15676",
            "high": "1088.83",
            "close": "1073.4"
        }
    ],
    "id": null
}
```

- - -

### Unsubscription to the state update for oth-like markets
> Params: none

Request example:
```
{"method":"state.unsubscribe_oth","params":[],"id":24}
```

- - -

### Unsubscription to the state update for all markets
> Params: none

Request example:
```
{"method":"price.unsubscribe_all","params":[],"id":25}
```

- - -

## Subscribing/unsubscribing to deals update for markets

- - -

### Subscription to deals update for btc-like markets
> Params: btc_like_market1, btc_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"deals.subscribe_btc","params":["ETH_BTC"],"id":26}
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

### Unsubscription to deals update for btc-like markets
> Params: none

Request example:
```
{"method":"deals.unsubscribe_btc","params":[],"id":27}
```

- - -

### Subscription to deals update for eth-like markets
> Params: eth_like_market1, eth_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"deals.subscribe_eth","params":["BNB_ETH"],"id":28}
```

Update message example:
```
{
    "method": "deals.update",
    "params": [
        "BNB_ETH",
        [
            {
                "id": 3132274915,
                "amount": "0.882",
                "price": "0.2097",
                "time": 1657713307.7137561,
                "type": "sell"
            },
            {
                "id": 3132274890,
                "amount": "1.205",
                "price": "0.2097",
                "time": 1657713307.5918369,
                "type": "sell"
            }
        ]
    ],
    "id": null
}
```

- - -

### Unsubscription to deals update for eth-like markets
> Params: none

Request example:
```
{"method":"deals.unsubscribe_eth","params":[],"id":29}
```

- - -

### Subscription to deals update for oth-like markets
> Params: oth_like_market1, oth_like_market2, ...

|Name  |Type   |Mandatory   |Description     |
|---|---|---|---|
|market   |String   |Yes   |Markets for subscribe. Subscription is possible for several markets in single-stream  |

Request example:
```
{"method":"deals.subscribe_oth","params":["BTC_USDT"],"id":30}
```

Update message example:
```
{
    "method": "deals.update",
    "params": [
        "BTC_USDT",
        [
            {
                "id": 3132383632,
                "price": "19851.09",
                "amount": "0.00016",
                "time": 1657713935.5847681,
                "type": "sell"
            }
        ]
    ],
    "id": null
}
```

- - -

### Unsubscription to deals update for oth-like markets
> Params: none

Request example:
```
{"method":"deals.unsubscribe_oth","params":[],"id":31}
```