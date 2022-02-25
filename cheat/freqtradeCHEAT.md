# freqtradeCHEAT

**[Yolo](#section-title)**

# ZUSAMMENFASSUNG
## Print pairlist
freqtrade list-pairs --quote USD --print-json
## list strategys 

freqtrade list-strategies

----------------------------------------------------------------------------------------------------------------------------

## download-data
freqtrade download-data -t 5m 15m 1h 4h         --timerange 20180108-
freqtrade download-data --pairs XLM/ XMR/USDT --exchange kucoin --days 60 -t 5m
                                                                                                        

### download-data refreshh
##freqtrade download-data --days 100

-----------------------------------------------------------------------------------------------------------------------------------------------------------------
## backtesting
freqtrade backtesting --strategy Solipsis4
freqtrade backtesting --strategy Diamond --timerange 202201015-
### *mehrer* strategien backtesting 
freqtrade backtesting --strategy-list xxx xxx --timeframe 5m  ---export trade --timerange 202201015-
freqtrade backtesting --strategy-list BreakEven Cluc4 Cluc5werk Cluc7werk ClucCrypROI --timeframe 5m  --export trades --timerange 20220201-


-----------------------------------------------------------------------------------------------------------------------------------------------------------------
# hyperopt 
#*    3/10:     76 trades. 51/18/7 Wins/Draws/Losses. Avg profit   1.92%. Median profit   2.40%. Total profit  0.04808472 BTC (  48.08%). $
#freqtrade hyperopt --hyperopt-loss OnlyProfitHyperOptLoss --spaces buy sell roi trailing stoploss --strategy Diamond -j 2 -e 10
 *   10/10:     76 trades. 39/34/3 Wins/Draws/Losses. Avg profit   0.61%. Median profit   0.05%. Total profit  0.01528359 BTC (  15.28%). $
     -j 2 -e 10
 *    4/10:     15 trades. 10/2/3 Wins/Draws/Losses. Avg profit   1.52%. Median profit   7.99%. Total profit  0.00754274 BTC (   7.54%). A$
 freqtrade hyperopt --hyperopt-loss SharpeHyperOptLossDaily --spaces buy sell roi trailing stoploss --strategy wtc -e 50
 *    7/10:    130 trades. 68/54/8 Wins/Draws/Losses. Avg profit   0.71%. Median profit   0.06%. Total profit  0.03050369 BTC (  30.50%). $
 freqtrade hyperopt --hyperopt-loss SortinoHyperOptLoss --spaces buy sell roi trailing stoploss --strategy GodStraNew -j 5 -e 10
 *    2/10:     10 trades. 7/0/3 Wins/Draws/Losses. Avg profit   5.50%. Median profit   7.05%. Total profit  0.01817970 BTC (  18.18%). Av$
 freqtrade hyperopt --hyperopt-loss SortinoHyperOptLossDaily --spaces buy sell roi trailing stoploss --strategy Diamond -j 2 -e 10
   | * Best |    3/10 |      165 |     98   63    4 |        1.00% |    0.05453885 BTC   (54.54%) | 0 days 08:02:00 |    0.00442974 BTC   $
   | * Best |    7/10 |      101 |     56   42    3 |        0.73% |    0.02444518 BTC   (24.45%) | 0 days 13:08:00 |    0.00107122 BTC   $
 *    7/10:    101 trades. 56/42/3 Wins/Draws/Losses. Avg profit   0.73%. Median profit   0.13%. Total profit  0.02444518 BTC (  24.45%). $
#freqtrade hyperopt --hyperopt-loss OnlyProfitHyperOptLoss --spaces buy sell roi trailing stoploss --strategy SwingHighToSky  -j 2 -e 50
 *    7/10:    117 trades. 74/41/2 Wins/Draws/Losses. Avg profit   1.91%. Median profit   1.50%. Total profit  0.07370921 BTC (  73.71%). $


## hyperopt list
freqtrade hyperopt-list
freqtrade hyperopt-list --profitable --no-details
> freqtrade hyperopt-show -n 168
freqtrade hyperopt-show --best -n -1 --print-json --no-header 
## print trades json
> Print trades with id 2 and 3 as json
freqtrade show-trades --db-url sqlite:///tradesv3.dry_run.sqlite --trade-ids 2 3 --print-json

jupyther
docker-compose -f docker/docker-compose-jupyter.yml up

https://127.0.0.1:8888/lab


## weiter hyperopt
[text-vXtziW.txt](../attachments/text-vXtziW.txt)

## Ploten

freqtrade plot-dataframe --strategy Diamond -p BTC/USDT -i 15m
freqtrade plot-dataframe --strategy Zeus

-------------------------------------------------------------------------------------------------------------------------------------------------
## hyperopt
#### copy ### -j 2 

y 



### hyperopt cheat
 

 - (Default Legacy  Freqtrade hyperoptimization loss function) - Meistens für kurze Handelsdauer und Vermeidung von Verlusten.
OnlyProfitHyperOptLoss - berücksichtigt nur die Höhe des Gewinns.
SharpeHyperOptLossDaily- Optimiert die Sharpe Ratio, die anhand der täglichen Handelsrenditen im Verhältnis zur Standardabweichung berechnet wird.
SharpeHyperOptLoss - Optimiert das anhand von Handelserträgen berechnete Sharpe Ratio im Verhältnis zur Standardabweichung.
SortinoHyperOptLoss- Optimiert das anhand von Handelserträgen berechnete Sortino-Verhältnis im Verhältnis zur Standardabweichung nach unten .
SortinoHyperOptLossDaily- Optimiert das Sortino-Verhältnis, das anhand der täglichen Handelsrenditen im Verhältnis zur Standardabweichung nach unten berechnet wird.
MaxDrawDownHyperOptLoss - Optimiert den maximalen Drawdown.
CalmarHyperOptLoss - Optimiert das Calmar-Verhältnis, das auf Handelserträgen im Verhältnis zum maximalen Drawdown berechnet wird.




freqtrade hyperopt --hyperopt-loss ShortTradeDurHyperOptLoss --spaces buy sell roi trailing stoploss --strategy Diamond -j 2 -e 10
# *    3/10:     76 trades. 51/18/7 Wins/Draws/Losses. Avg profit   1.92%. Median profit   2.40%. Total profit  0.04808472 BTC (  48.08%). $
# freqtrade hyperopt --hyperopt-loss OnlyProfitHyperOptLoss --spaces buy sell roi trailing stoploss --strategy Diamond -j 2 -e 10
# *   10/10:     76 trades. 39/34/3 Wins/Draws/Losses. Avg profit   0.61%. Median profit   0.05%. Total profit  0.01528359 BTC (  15.28%). $
#     -j 2 -e 10
# *    4/10:     15 trades. 10/2/3 Wins/Draws/Losses. Avg profit   1.52%. Median profit   7.99%. Total profit  0.00754274 BTC (   7.54%). A$
# freqtrade hyperopt --hyperopt-loss SharpeHyperOptLossDaily --spaces buy sell roi trailing stoploss --strategy wtc -e 50
# *    7/10:    130 trades. 68/54/8 Wins/Draws/Losses. Avg profit   0.71%. Median profit   0.06%. Total profit  0.03050369 BTC (  30.50%). $
# freqtrade hyperopt --hyperopt-loss SortinoHyperOptLoss --spaces buy sell roi trailing stoploss --strategy GodStraNew -j 5 -e 10
# *    2/10:     10 trades. 7/0/3 Wins/Draws/Losses. Avg profit   5.50%. Median profit   7.05%. Total profit  0.01817970 BTC (  18.18%). Av$
# freqtrade hyperopt --hyperopt-loss SortinoHyperOptLossDaily --spaces buy sell roi trailing stoploss --strategy Diamond -j 2 -e 10
#   | * Best |    3/10 |      165 |     98   63    4 |        1.00% |    0.05453885 BTC   (54.54%) | 0 days 08:02:00 |    0.00442974 BTC   $
#   | * Best |    7/10 |      101 |     56   42    3 |        0.73% |    0.02444518 BTC   (24.45%) | 0 days 13:08:00 |    0.00107122 BTC   $
# *    7/10:    101 trades. 56/42/3 Wins/Draws/Losses. Avg profit   0.73%. Median profit   0.13%. Total profit  0.02444518 BTC (  24.45%). $
# freqtrade hyperopt --hyperopt-loss OnlyProfitHyperOptLoss --spaces buy sell roi trailing stoploss --strategy SwingHighToSky  -j 2 -e 50
# *    7/10:    117 trades. 74/41/2 Wins/Draws/Losses. Avg profit   1.91%. Median profit   1.50%. Total profit  0.07370921 BTC (  73.71%). $




+-------------------------+------------------------------+-------------+----------------+--------------+---------------+
|                    name |                     location |      status |   hyperoptable |   buy-Params |   sell-Params |
|-------------------------+------------------------------+-------------+----------------+--------------+---------------|
|                      -- |                   GodStra.py | LOAD FAILED |             No |            0 |             0 |
|                      -- |                      Zeus.py | LOAD FAILED |             No |            0 |             0 |
|                      -- |                  Heracles.py | LOAD FAILED |             No |            0 |             0 |
|               BreakEven |                 BreakEven.py |          OK |             No |            0 |             0 |
|  CustomStoplossWithPSAR | custom_stoploss_with_psar.py |          OK |             No |            0 |             0 |
|               DevilStra |                 DevilStra.py |          OK |            Yes |            1 |             1 |
|                 Diamond |                   Diamond.py |          OK |            Yes |            4 |             4 |
|     FixedRiskRewardLoss |     fixed_riskreward_loss.py |          OK |             No |            0 |             0 |
|              `GodStraNew` |                GodStraNew.py |          OK |            Yes |           12 |            12 |
|       HourBasedStrategy |         HourBasedStrategy.py |          OK |            Yes |            2 |             2 |
|       InformativeSample |         InformativeSample.py |          OK |             No |            0 |             0 |
|                 MultiMa |                   MultiMa.py |          OK |            Yes |            2 |             2 |
|             Strategy001 |               Strategy001.py |          OK |             No |            0 |             0 |
| Strategy001_custom_sell |   Strategy001_custom_sell.py |          OK |             No |            0 |             0 |
|             Strategy002 |               Strategy002.py |          OK |             No |            0 |             0 |
|             Strategy003 |               Strategy003.py |          OK |             No |            0 |             0 |
|             Strategy004 |               Strategy004.py |          OK |             No |            0 |             0 |
|             Strategy005 |               Strategy005.py |          OK |            Yes |            4 |             4 |
|              Supertrend |                Supertrend.py |          OK |            Yes |            6 |             6 |
|          SwingHighToSky |         Swing-High-To-Sky.py |          OK |            Yes |            4 |             4 |
|                    hlhb |                      hlhb.py |          OK |             No |            0 |             0 |
|                 mabStra |                   mabStra.py |          OK |            Yes |            5 |             5 |
|                     wtc |                       wtc.py |          OK |            Yes |            6 |             6 |
+-------------------------+------------------------------+-------------+----------------+--------------+---------------+























###################################
------------------------------------
################################### ALT ALT ALT ###################################
################################################################################
###############################################################################


freqtrade download-data --days 180- t 5m ---datadir user_data/data --config user_data/config.json freqtrade dow --pairs ./USD 

freqtrade hyperopt --hyperopt-loss SharpeHyperOptLossDaily --spaces roi stoploss trailing --strategy Diamond -e 100 --timerange 20219101-20220110

freqtrade hyperopt --hyperopt-loss MyAwesomeStrategy --strategy <strategyname> -e 500 --spaces all

`--pairs ./USD`

## 

docker-compose run freqtrade hyperopt --hyperopt-loss SharpeHyperOptLossDaily --spaces roi stoploss trailing --strategy mabStra --config user_data/config.json -e 100 --pairs ./USD 

pip install ccxt

docker-compose run freqtrade backtesting --strategy Strategy


---

# Docker quick start¶

docker inspect -f "{{ .Config.Env }}" 41e65fa16da0

## run

### compose

`docker-compose run freqtrade`  GNU nano 2.9.3                                         user_data/strategies/Diamond.py                                                    

# cuz of that it have not any indicator population. idea is that
# It is just use the pure dataframe ohlcv data for calculation
# of buy/sell signals, But you can add your indicators and add
# your key names inside catagorical hyperoptable params and
# than you be able to hyperopt them as well.
# thanks to: @Kroissan, @drakes00 And @xmatthias for his patience and helps
# Author: @Mablue (Masoud Azizi)
# github: https://github.com/mablue/
# * freqtrade backtesting --strategy Diamond



### exec

docker exec -it 9e82b39c3d14 bash docker exec -u root -it 9e82b39c3d14 bash 'source .env/bin/activate; freqtrade --help'

## basics

### hyperopt

freqtrade hyperopt --hyperopt-loss SharpeHyperOptLossDaily --spaces roi stoploss trailing --strategy Strategy002 --config user_data/config.json -e 100

### backtesting

freqtrade backtesting --strategy Strategy002 --config user_data/config.json

## Sonstiges

### list pairlist

$ freqtrade -c config_binance.json list-pairs --all --base BTC ETH --quote USDT USD --print-list Print all markets on exchange "Kraken", in the tabular format:

$ freqtrade list-markets --exchange ftx --all

\--timerange=20190501-

---

# 

# 

# 

## list pair

Print the list of active pairs with quote currency USD on exchange, specified in the default configuration file (i.e. pairs on the "Bittrex" exchange) in JSON format:

$ freqtrade list-pairs --quote USD --print-json Print the list of all pairs on the exchange, specified in the config_binance.json configuration file (i.e. on the "Binance" exchange) with base currencies BTC or ETH and quote currencies USDT or USD, as the human-readable list with summary:

$ freqtrade -c config_binance.json list-pairs --all --base BTC ETH --quote USDT USD --print-list Print all markets on exchange "Kraken", in the tabular format:

$ freqtrade list-markets --exchange ftx --all
