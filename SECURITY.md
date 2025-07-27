Check https://termux.dev/security for info on Termux security policies and how to report vulnerabilities.
pkg update && pkg upgrade
pkg install python git
pip install --upgrade pip
pip install python-binance
from binance.client import Client
import time

# ТВОИ API КЛЮЧИ
api_key = 'ТВОЙ_API_KEY'
api_secret = 'ТВОЙ_SECRET_KEY'

client = Client(api_key, api_secret)

# Торговая стратегия
buy_price = 110000
sell_price = 120000
quantity = 0.001  # Кол-во BTC для торговли

while True:
    ticker = client.get_symbol_ticker(symbol="BTCUSDT")
    price = float(ticker['price'])
    print(f"Текущая цена BTC: {price}")

    if price <= buy_price:
        order = client.order_market_buy(symbol='BTCUSDT', quantity=quantity)
        print(f"✅ Куплено BTC по цене: {price}")
    elif price >= sell_price:
        order = client.order_market_sell(symbol='BTCUSDT', quantity=quantity)
        print(f"✅ Продано BTC по цене: {price}")
    else:
        print("⏳ Ждём сигнал...")

    time.sleep(300)  # Проверка каждые 5 минут
