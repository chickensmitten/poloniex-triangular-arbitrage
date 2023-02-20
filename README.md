# Poloniex Triangular Arbitrage in Python

## Basic Explanation
- For more explanation on [triangular arbitrage](https://en.wikipedia.org/wiki/Triangular_arbitrage)
- Base is left aka numerator, Quote is right aka denominator. i.e. BTC_USD, BTC us base or numerator, while USD is quote or denominator
- Key concepts to know: 
  - Forward: Base to Quote type calculation
  - Reverse: Quote to Base type calculation
- Even though there the surface rate shows that there is arbitrage opportunity, it is important to also calculate order book depth.
- Real rate is the arbitrage rate calculated after taking into account all prices based upon trading input/exchange capital. Basically, it checks if there is enough liquidity to take advantage of the arbitrage based on the trading pairs at the quoted price.
- Triangle arbitrage opportunity in centralized exchanges is rare
- Lesson 50 to 53. For recap of explanation on the triangle arbitrage code.
- Step 0 and step 1, is to collect data from Poloniex then sort the data so that we can do arbitrage calculation.

## Setup
```
python3 -m venv venv
source venv/bin/activate
pip3 install requirements.txt
<!-- pip3 install requests for api calls-->
python3 main.py
```

## Operations
1. Find arbitrage opportunity of surface rate
  - The code `calc_triangular_arb_surface_rate` is trying to calculate if arbitrage exists for three pairs in `t_pair`. The only way to do it is just calculate and check for profitability. To get started, read the `structured_triangular_pairs.json` file in root directory.
  - There are 4 possible scenarios for the forward method and another 4 scenarios with the reverse method.

2. Once there is an arbitrage opportunity for a surface rate, check if that arbitrage opportunity has depth



