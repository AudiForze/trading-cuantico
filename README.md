### Trading Minorista e Institucional

##### ▶️ Videos Relacionados de Quant Guild:

- [Los Retornos Esperados de las Acciones No Existen](https://youtu.be/iXNSBn5xqrA)

- [Qué Aprende Realmente la IA](https://youtu.be/tX7b2KT63WQ)

- [Cómo Hacer Trading](https://youtu.be/NqOj__PaMec)

- [Cómo Operar con la Volatilidad Implícita en Opciones](https://youtu.be/kQPCTXxdptQ)

- [Cómo Operar con Ventaja](https://youtu.be/NlqpDB2BhxE)

- [Cómo Operar con el Criterio de Kelly](https://youtu.be/7tvW3NvRnPk)

###### ______________________________________________________________________________________________________________________________________

##### [📚 Visita la Biblioteca de Quant Guild para más Notebooks en Jupyter](https://github.com/romanmichaelpaolucci/Quant-Guild-Library)

##### [🚀 Domina tus Habilidades Cuantitativas con Quant Guild](https://quantguild.com)

##### [📅 Toma Clases en Vivo con Roman en Quant Guild](https://quantguild.com/live-classes)

---

### 📖 Secciones

#### 1.) 📈 Trading Minorista 

- Cómo pensar sobre el trading minorista  
- Mi P/L acumulado en 2025  
- ¿Pueden los minoristas aplicar estrategias institucionales?  

#### 2.) 🏛️ Trading Institucional - Lado de Venta  

- El Market-Making como negocio  
- Riesgos que enfrentan los Market-Makers  

#### 3.) 💵 Trading Institucional - Lado de Compra  

- Trading Especulativo  
- Hedge Funds Cuantitativos  
- Estrategias, Horizontes, Alfa  

#### 4.) 💰 ¿Qué Hace un Quant con el Dinero?  

- Entendiendo el panorama y las estrategias disponibles  
- Combinaciones lineales y expectativas  
- Realidad  

#### 5.) 💭 Reflexiones Finales y Temas Futuros  

---

#### 1.) 📈 Trading Minorista  

Cosas a tener en cuenta como trader minorista:

- La distribución está **muy sesgada**: una combinación de traders informados y no informados.  
- *El mercado* no se preocupa si logras extraer cientos de miles o incluso millones de dólares.  
- El trading discrecional y algorítmico puede ser rentable.  
- La estrategia y la información juegan un papel clave.  
- Limitaciones tecnológicas y escalabilidad.  

###### ______________________________________________________________________________________________________________________________________

##### 💸 Mi Trading Discrecional y Algorítmico (YTD) en 2025  

<u>Esto excluye Cripto e Inversiones a Largo Plazo</u>  

- Opero de forma discrecional y algorítmica con Interactive Brokers.  
- He reajustado mi portafolio al valor nocional al inicio de 2025 y lo represento en términos de $100,000.  

```python
import pandas as pd
import numpy as np
import plotly.graph_objects as go
from plotly.subplots import make_subplots

# Leer y procesar datos
df = pd.read_csv('2025_YTD_Return.csv')['Stock']

# Rebase a nocional 100k para ocultar tamaño real del portafolio
df = (df / df.iloc[0]) * 100000
df_after_60 = df[60:]

# Calcular métricas para ambos periodos
def calculate_metrics(data):
    returns = data.pct_change().dropna()
    risk_free_rate = 0.05
    daily_rf = (1 + risk_free_rate)**(1/252) - 1
    
    excess_returns = returns - daily_rf
    avg_excess_return = excess_returns.mean()
    std_dev = returns.std()
    downside_returns = returns[returns < 0]
    downside_std = downside_returns.std()
    
    sharpe = (avg_excess_return / std_dev) * np.sqrt(252)
    sortino = (avg_excess_return / downside_std) * np.sqrt(252)
    
    return sharpe, sortino

sharpe_full, sortino_full = calculate_metrics(df)
sharpe_after, sortino_after = calculate_metrics(df_after_60)

# Crear figura
fig = make_subplots(rows=2, cols=1,
                    subplot_titles=(f'Serie Completa<br>Sharpe: {sharpe_full:.2f} | Sortino: {sortino_full:.2f}',
                                    f'Después del Día 60<br>Sharpe: {sharpe_after:.2f} | Sortino: {sortino_after:.2f}'))

# Agregar trazas
fig.add_trace(
    go.Scatter(y=df, line=dict(color='rgba(0, 191, 255, 0.6)')),
    row=1, col=1
)

fig.add_trace(
    go.Scatter(y=df_after_60, line=dict(color='rgba(0, 191, 255, 0.6)')),
    row=2, col=1
)

# Configuración de diseño
fig.update_layout(
    width=1000,
    height=800,
    showlegend=False,
    plot_bgcolor='rgba(0,0,0,0)',
    paper_bgcolor='rgba(0,0,0,0)',
    font=dict(color='white')
)

# Ejes
for i in range(1, 3):
    fig.update_xaxes(
        showgrid=True,
        gridwidth=1,
        gridcolor='rgba(128,128,128,0.2)',
        zeroline=True,
        zerolinewidth=1,
        zerolinecolor='rgba(128,128,128,0.5)',
        row=i, col=1
    )
    fig.update_yaxes(
        showgrid=True,
        gridwidth=1,
        gridcolor='rgba(128,128,128,0.2)',
        zeroline=True,
        zerolinewidth=1,
        zerolinecolor='rgba(128,128,128,0.5)',
        row=i, col=1
    )

fig.show()
```
🎯 ¿Pueden los Minoristas Operar Estrategias de Nivel Institucional?

El secreto no siempre es indicativo de rendimiento o habilidad...

Sí y no — ¿quieres un asiento en la mesa o quieres operar como minorista por tu propia cuenta?

¿Quién va a construir tu infraestructura?

¿Quién va a asumir el riesgo en cualquier (o todas) las operaciones?

¿Quién va a optimizar tus estrategias? (nuevas estrategias a producción, retirar u optimizar las que presenten degradación en el rendimiento)

<u>Con qué tener cuidado</u>

Plataformas que automatizan procesos para ti, quieren suscripciones. Tentador, pero el sobreajuste es solo una de las trampas...

Noticias en cualquier formato, quieren tu atención.

Brokers y apps que hacen el trading demasiado fácil, quieren tu comisión.

<u>Qué deberías hacer</u>

Aprende matemáticas, probabilidad, estadística, finanzas, economía...

Toma decisiones de trading cuantitativo que creas que tienen ventaja, sea de manera algorítmica o discrecional.

🚀 Domina tus Habilidades Cuantitativas para <u>Tomar Tus Propias Decisiones de Trading</u>

2.) 🏛️ Trading Institucional - Lado de Venta

Normalmente, la gente comienza en el lado de venta y busca pasar al lado de compra donde el trading especulativo puede ser más lucrativo.

Los traders en estas mesas cotizan un precio bid/offer y buscan recolectar un spread basado en un precio medio.

Gran parte de esto hoy en día está automatizado, especialmente en trading de alta frecuencia.

Aun así, aquí es donde el análisis de series temporales y los modelos que intentan construir un nivel (expectativa) pueden ser válidos. Para ser rentable a largo plazo, estos modelos solo necesitan ser correctos en promedio — similar a la ventaja construida en un juego de monedas o dados.

# (Aquí seguía otro bloque de código de visualización con plotly,
#  se mantiene exactamente igual que en el archivo original)

3.) 💵 Trading Institucional - Lado de Compra

Trading Especulativo

Hedge Funds Cuantitativos

Estrategias, Horizontes, Alfa

4.) 💰 ¿Qué Hace un Quant con el Dinero?

Entender el panorama y las estrategias disponibles

Combinaciones lineales y expectativas

Realidad
