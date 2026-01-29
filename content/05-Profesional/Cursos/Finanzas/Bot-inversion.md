---
title: "requirements: pandas, numpy, yfinance, pandas_ta (opcional)"
date: 2026-01-26
tags:
  - profesional
  - cursos
  - finanzas
---
Perfecto. Te doy un plan claro para levantar un bot de inversión desde cero, con un MVP que puedas ejecutar en paper-trading y luego pasar a real.

Primero necesitas tres piezas: una fuente de datos de mercado, un bróker con API y una estrategia con gestión de riesgo. Para datos en el MVP puedes usar yfinance para backtests rápidos; para producción conviene un feed más robusto (por ejemplo, el propio del bróker). Como bróker con API y entorno de simulación funciona bien Alpaca; Interactive Brokers es más potente pero algo más complejo. La estrategia del MVP puede ser un cruce de medias simple sobre acciones líquidas o ETFs, con reglas de entrada/salida y límites de riesgo por operación. La gestión de riesgo no es opcional: fija un máximo de capital por operación (por ejemplo, 1-2%), un stop loss y, si procede, un take profit. Antes de tocar dinero real, valida con backtesting y luego con paper-trading.

Te dejo un esqueleto mínimo en Python. Hace backtest con una señal sencilla (SMA 10 cruza SMA 50), reporta métricas básicas y muestra cómo conectar después con un bróker. El foco es la arquitectura: separo adquisición de datos, señales, ejecución y control de riesgo.

```python
# requirements: pandas, numpy, yfinance, pandas_ta (opcional)

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[01-Ciberseguridad/Herramientas/HTTP-Parameter-Pollution-HPP|HTTP Parameter Pollution HPP]]. [[01-Ciberseguridad/Herramientas/Modulo-de-python3-httpserver|Modulo de python3 httpserver]].

import pandas as pd, numpy as np, yfinance as yf
from datetime import datetime, timedelta

# --- 1) Universo y parámetros
TICKER = "SPY"              # ETF amplio para el MVP
START  = "2018-01-01"
CASH   = 10_000
RISK_PCT_PER_TRADE = 0.02   # 2% del capital por trade
SMA_FAST, SMA_SLOW = 10, 50

# --- 2) Datos
data = yf.download(TICKER, start=START, auto_adjust=True)
data["sma_fast"] = data["Close"].rolling(SMA_FAST).mean()
data["sma_slow"] = data["Close"].rolling(SMA_SLOW).mean()
data.dropna(inplace=True)

# --- 3) Señal
data["long_signal"]  = (data["sma_fast"] > data["sma_slow"]) & (data["sma_fast"].shift(1) <= data["sma_slow"].shift(1))
data["flat_signal"]  = (data["sma_fast"] < data["sma_slow"]) & (data["sma_fast"].shift(1) >= data["sma_slow"].shift(1))

# --- 4) Backtest vectorizado simple (solo posiciones largas, 100% del sizing permitido)
position = 0 #indica si estás fuera (0) o dentro (1) del mercado
cash = CASH
shares = 0 # número de titulos en cartera
equity_curve = [] #evolución del patrimonio para calcular métricas

for date, row in data.iterrows():
    price = row["Close"]

    # Señales
    if row["long_signal"] and position == 0:
        risk_amount = cash * RISK_PCT_PER_TRADE
        # stop loss a 2 x ATR o 5% por simplicidad; aquí usamos 5%
        stop_loss = price * 0.95
        per_share_risk = price - stop_loss
        #la cantidad de acciones que vas a jugar
        qty = int(risk_amount / max(per_share_risk, 0.01))
        qty = max(qty, 0)
        cost = qty * price
        if qty > 0 and cost <= cash:
            shares += qty
            cash   -= cost
            position = 1

    elif row["flat_signal"] and position == 1:
        cash   += shares * price
        shares  = 0
        position = 0
	
    equity = cash + shares * price #valor total de tu cuenta 
    # Equity = efectivo disponible + valor de tus acciones
    equity_curve.append((date, equity))

# Cierra cualquier posición al final
if shares > 0:
    cash   += shares * data["Close"].iloc[-1]#`.iloc` significa _integer location_, es decir, selección por posición (0 = primera fila, 1 = segunda, etc.).
    shares  = 0
equity_curve = pd.DataFrame(equity_curve, columns=["date","equity"]).set_index("date")

# Métricas básicas
ret_total = (equity_curve["equity"].iloc[-1] / CASH) - 1
dd = (equity_curve["equity"] / equity_curve["equity"].cummax() - 1).min()
daily = equity_curve["equity"].pct_change().dropna()
sharpe = np.sqrt(252)*daily.mean()/daily.std() if daily.std() != 0 else 0

print(f"Retorno total: {ret_total:.2%}")
print(f"Máx. drawdown: {dd:.2%}")
print(f"Sharpe aprox.: {sharpe:.2f}")
```

Cuando el backtest sea razonable, pasa a paper-trading. Cambias el módulo de “ejecución” para enviar órdenes al bróker en lugar de simular. El patrón es: calcular señal, consultar posiciones, decidir tamaño, enviar orden limitada/market, y registrar en un log. Como ejemplo ilustrativo de la parte de ejecución (pseudocódigo, porque cada API cambia):

```python
# ejecución en paper con Alpaca (esquema, no credenciales reales)
import requests, os

ALPACA_KEY = os.getenv("ALPACA_KEY")
ALPACA_SEC = os.getenv("ALPACA_SEC")
BASE_URL   = "https://paper-api.alpaca.markets"

def place_order(symbol, qty, side, type="market", tif="day"):
    endpoint = f"{BASE_URL}/v2/orders"
    payload = {"symbol": symbol, "qty": qty, "side": side, "type": type, "time_in_force": tif}
    r = requests.post(endpoint, json=payload, headers={
        "APCA-API-KEY-ID": ALPACA_KEY, "APCA-API-SECRET-KEY": ALPACA_SEC
    })
    r.raise_for_status()
    return r.json()
```

Para robustecer el sistema, añade validaciones de datos, control de desconexiones, límites de pérdida diarios, reinicio automático y alertas por correo o Telegram. En Europa asegúrate de cumplir con MiFID II y con las condiciones de tu bróker, y comienza siempre con cuentas demo o paper-trading antes de comprometer capital real.

Si te parece, en el siguiente paso te preparo un repo mínimo con estructura de carpetas, un `.env` de ejemplo, un scheduler para ejecutar el bot a una hora concreta en tu zona (Europe/Madrid) y un segundo par de estrategias básicas (momentum y mean-reversion) para que puedas comparar rápidamente. También puedo adaptarlo a tu stack favorito (por ejemplo, FastAPI + Docker) o integrarlo con tus flujos actuales.

 
# Qué es el repo y cómo se orquesta

La idea es separar responsabilidades. En `src/` vive todo lo “de mercado”: carga de datos, señales, backtest y ejecución. En `scheduler/` está el reloj que dispara el bot a la hora que tú digas en **Europe/Madrid**. Con esto puedes comparar estrategias, ejecutar la que elijas cada día y, si quieres, pasar de simulación a órdenes reales con un interruptor.

# El `.env`: configuración sin tocar código

El archivo `.env` guarda parámetros cambiantes: estrategia, ticker, fecha de inicio, hora local, y si ejecutas órdenes reales. Lo lees con `python-dotenv` en `src/config.py`. Así puedes probar, por ejemplo, SPY con momentum desde 2010 y, sin cambiar código, pasar a QQQ con mean-reversion, o mover la hora a las 16:30 Madrid. También están las credenciales de Alpaca (vacías por defecto). Cuando `EXECUTE_ORDERS=false`, nunca se manda nada al bróker; al ponerlo `true`, el bot ya puede llamar a `broker/alpaca.py`.

# Las estrategias: dos sabores complementarios

El “momentum” usa un cruce de medias rápidas (10/50) filtrado por una media de régimen (200). En castellano: sólo toma riesgo cuando hay tendencia de fondo y la rápida va por encima de la lenta. El “mean-reversion” busca retrocesos controlados: en régimen alcista, compra cuando el precio cae hasta una zona de soporte estadístico (SMA20 menos 1,5×ATR) y sale cuando el precio recupera la media. Con estas dos tienes perfiles distintos: uno persigue tendencia y el otro compra “rebajas” dentro de una tendencia.

# La comparación rápida

`compare_strategies.py` carga precios con `yfinance`, calcula pesos diarios de cada estrategia (0 fuera, 1 dentro) y simula la curva de capital con un backtest sencillo basado en pesos. Añade un buy & hold de referencia. Con esas tres curvas mide retorno total, drawdown y Sharpe. Sirve para responder “cuál me compensa ahora mismo” sin enredarte en detalles operativos.

# El bot diario

`run_daily.py` recalcula la señal con datos hasta el último cierre y te imprime: fecha, último precio y peso recomendado. Esto ya es suficiente para operar manualmente si quieres. Si activas `EXECUTE_ORDERS=true`, aquí es donde engancharías la lógica de órdenes: ver el peso de ayer vs. hoy, calcular el ajuste y llamar a `broker/alpaca.place_order(...)`. El módulo de Alpaca está preparado con la llamada REST estándar y cabeceras con tus claves.

# El scheduler en zona Europe/Madrid

`scheduler/schedule.py` usa APScheduler con un `CronTrigger` “lunes a viernes a HH:MM en TZ=Europe/Madrid”. El scheduler ejecuta la función del bot a esa hora cada día hábil, con la zona horaria correcta (no te peleas con DST ni UTC). Los valores los controlas desde el `.env`. Esto te permite dejar el proceso corriendo en un servidor (o en tu máquina) y olvidarte: cuando toque, calcula la señal y, si lo has activado, lanza órdenes.

# Camino a producción y adaptaciones

Si quieres FastAPI: se envuelve la lógica de “decidir señal” en un endpoint (`/signal`, `/run`) y el scheduler pasa a un job interno o a un servicio externo (systemd/cron). Para Docker: se añade un `Dockerfile` y quizá `docker-compose.yml` con dos servicios, `bot` y `scheduler`, compartiendo el mismo `.env` como secretos. La ventaja es desplegarlo idéntico en tu servidor o en la nube y versionar la config.

# Qué tocar si quieres afinar

Si buscas más “realismo”, añade comisiones y deslizamiento al backtest basado en pesos, un control de riesgo por volatilidad (peso objetivo = vol_target / vol_realizada), y stops/trailing en una simulación con posiciones. Si persistes la curva y las señales (CSV/SQLite), tendrás auditoría y gráficos históricos. Y si vas a órdenes reales, añade validaciones: estado del mercado, posición actual, límites diarios de pérdida y reintentos ante fallos de red.

Si te apetece, lo siguiente que hago es añadirte Docker y un endpoint FastAPI básico encima de este repo para que puedas desplegarlo en un VPS y consultar la señal del día con una URL.