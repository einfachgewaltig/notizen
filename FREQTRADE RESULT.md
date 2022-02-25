FREQTRADE RESULT
========================

## Diamond
+--------+---------+----------+------------------+--------------+------------------------------+-----------------+-------------+------------------------------+                                                                            
|   Best |   Epoch |   Trades |    Win Draw Loss |   Avg profit |                       Profit |    Avg duration |   Objective |          Max Drawdown (Acct) |
|--------+---------+----------+------------------+--------------+------------------------------+-----------------+-------------+------------------------------|
| * Best |    2/15 |       22 |     15    2    5 |        0.91% |         7.833 USD    (3.92%) | 0 days 01:31:00 |     1.90715 |         2.655 USD    (1.32%) |
| * Best |    4/15 |      392 |    212   12  168 |        0.48% |        88.040 USD   (44.02%) | 0 days 00:45:00 |     1.19907 |        18.948 USD    (7.19%) |
 [Epoch 15 of 15 (100%)] ||                                                                                                                                                                       | [Time:  0:00:33, Elapsed Time: 0:00:33]
2022-02-11 06:18:17,872 - freqtrade.optimize.hyperopt - INFO - 15 epochs saved to '/freqtrade/user_data/hyperopt_results/strategy_Diamond_2022-02-11_06-17-24.fthypt'.
2022-02-11 06:18:17,879 - freqtrade.resolvers.iresolver - WARNING - Could not import /freqtrade/user_data/strategies/Zeus.py due to 'No module named 'ta''
2022-02-11 06:18:17,890 - freqtrade.resolvers.iresolver - WARNING - Could not import /freqtrade/user_data/strategies/Heracles.py due to 'No module named 'ta''
2022-02-11 06:18:17,895 - freqtrade.resolvers.iresolver - WARNING - Could not import /freqtrade/user_data/strategies/GodStra.py due to 'No module named 'ta''
2022-02-11 06:18:17,939 - freqtrade.optimize.hyperopt_tools - INFO - Dumping parameters to /freqtrade/user_data/strategies/Diamond.json

Best result:

*    4/15:    392 trades. 212/12/168 Wins/Draws/Losses. Avg profit   0.48%. Median profit   0.26%. Total profit 88.03966149 USD (  44.02%). Avg duration 0:45:00 min. Objective: 1.19907


    # Buy hyperspace params:
    buy_params = {
        "buy_fast_key": "close",
        "buy_horizontal_push": 4,
        "buy_slow_key": "low",
        "buy_vertical_push": 1.042,
    }

    # Sell hyperspace params:
    sell_params = {
        "sell_fast_key": "close",
        "sell_horizontal_push": 10,
        "sell_slow_key": "low",
        "sell_vertical_push": 1.051,
    }

    # ROI table:
    minimal_roi = {
        "0": 0.095,
        "22": 0.062,
        "48": 0.012,
        "70": 0
    }

    # Stoploss:
    stoploss = -0.313

    # Trailing stop:
    trailing_stop = True
    trailing_stop_positive = 0.266
    trailing_stop_positive_offset = 0.365
    trailing_only_offset_is_reached = True
