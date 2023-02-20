# Poloniex Triangular Arbitrage in Python

## Basic Explanation
- For more explanation on [triangular arbitrage](https://en.wikipedia.org/wiki/Triangular_arbitrage)
- Base is left aka numerator, Quote is right aka denominator. i.e. BTC_USD, BTC us base or numerator, while USD is quote or denominator
- Key concepts to know: 
  - Forward Direction: Base to Quote type calculation
  - Reverse Direction: Quote to Base type calculation
- It is insufficient to just get the right 3 trading pairs to complete an arbitrage. The directions in which the trading pairs are calculated is important too.
- Even though there the surface rate shows that there is arbitrage opportunity, it is important to also calculate order book depth.
- Real rate is the arbitrage rate calculated after taking into account all prices based upon trading input/exchange capital. Basically, it checks if there is enough liquidity to take advantage of the arbitrage based on the trading pairs at the quoted price.
- Lesson 50 to 53. For recap of explanation on the triangle arbitrage code.
- Lesson 64 to 66. For recap to calculate orderbook depth.
- Step 0 and step 1, is to collect data from Poloniex then sort the data so that we can do arbitrage calculation.

## Caution: Reasons for tirangle arbitrage failure
- Exchange: Bad prices from the exchange or just bad code from exchange
- Trade Frequency and Call limits: Reaching exchange call limits. The more often you can sample the exchange data, the better it is.
- Code and Internet Latency: How often the price are updated and also how long does it take for your to calculate.
- Human error: There is an error in your code like getting the conversion wrong
- Orderbook depth: If the arbitrage opportunity doesn't have enough "depth", you can't make enough profit, after deducting the fees. See next point.
- Starting amount: Do you have the right amount of liquidity to take advantage of the arbitrage? Too much starting amount can be bad. This is because the orderbook might not have enough liquidity for the trade volume you have in mind.
- Competition: Other participants are also competiting with you for the arbitrage.
**Therefore, triangle arbitrage opportunities in centralized exchanges are rare.**

## Setup
```
python3 -m venv venv
source venv/bin/activate
pip3 install requirements.txt
<!-- pip3 install requests for api calls-->
python3 main.py
```

## Operation
1. Find arbitrage opportunity of surface rate
  - The `calc_triangular_arb_surface_rate` code is trying to calculate if arbitrage exists for three pairs in `t_pair`. The only way to do it is just calculate and check for profitability. To get started, read the `structured_triangular_pairs.json` file in root directory.
  - There are 4 possible scenarios for the forward method and another 4 scenarios with the reverse method.
  - The `calc_triangular_arb_surface_rate` code also take notes of the directionality.

2. Check if the arbitrage opportunity has depth
  - Get the first trading pairs that has the arbitrage opportunity with the right direction, then loop through the orderbook levels of that trading pair to acquire as much coin as the trading balance allows.
  - Then take the acquired coins and loop through the second trading pair and do the same as the previous step before going to the third trading pair and loop through it similarly
  - In the end, the total coins acquired will be more than the total starting coins

## To Dos
- Write tests to ensure refactoring doesn't break code


