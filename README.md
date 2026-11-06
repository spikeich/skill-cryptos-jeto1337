# Skill cryptos · jeto1337

Skills de Claude para operar cripto en el corto plazo: encontrar qué rompe,
probar el plan antes de arriesgar un dólar, calcular cuánto abrir y simular la
operación con precios en vivo.

Gratis, MIT, sin registro y sin API key. Son scripts de Python, solo librería
estándar, que leen datos públicos de CoinGecko y Yahoo Finance.

**Nada de esto opera por vos.** Ninguna skill manda órdenes a una exchange.
Vos decidís y cargás la orden en tu app.

## Instalar

En Claude Code, como plugin:

```
/plugin marketplace add spikeich/skill-cryptos-jeto1337
/plugin install skill-cryptos-jeto1337@skill-cryptos-jeto1337
```

O copiando las carpetas:

```bash
git clone https://github.com/spikeich/skill-cryptos-jeto1337.git
cp -r skill-cryptos-jeto1337/crypto-* ~/.claude/skills/
```

Para un solo proyecto, copialas en `.claude/skills/` de ese repo.

Necesitan Python 3.8 o más nuevo y salida a internet hacia
`api.coingecko.com`, `query1.finance.yahoo.com` y `query2.finance.yahoo.com`.

## Las skills

| comando | qué hace |
| --- | --- |
| `/crypto-scanner` | Qué cripto rompe el rango de apertura de **Europa** o de **Wall Street**, para arriba o para abajo, y los setups del gráfico diario (rupturas de 20 días, banderas, media de 20, sobreventa y sobrecompra). |
| `/crypto-entry` | El **temporizador de entrada**: vigila vela por vela y avisa el momento exacto en que una cripto cierra afuera del rango de apertura (o de un nivel), en largo o en corto. |
| `/crypto-exit` | El **plan de salida**: stop, objetivo y hora de salida antes de entrar, con el R neto de comisiones de Binance y el chequeo de liquidación según el apalancamiento. |
| `/crypto-timemachine` | La **máquina del tiempo**: repite 10.000 veces el resto del día con las velas reales de 5 minutos de esa cripto en los últimos 60 días, prueba la regla en cada día pasado y te dice si el plan tiene ventaja o es tirar una moneda. |
| `/crypto-scalp` | Lee el mercado, elige las mejores criptos para scalping, calcula el tamaño de la posición según tu capital y tu riesgo (con apalancamiento, margen aislado y comisiones de Binance) y simula operaciones en papel con avisos. |

## Cómo se usan juntas

```
/crypto-scanner      qué rompió en la apertura
/crypto-entry        el momento exacto de entrar      -> trader/entry.json
/crypto-exit         stop, objetivo y hora de salida  -> trader/plan.json
/crypto-timemachine  ¿ese plan tiene ventaja?
/crypto-scalp        cuánto abrir, y simularla antes de hacerla de verdad
```

Cada skill lee lo que escribió la anterior en la carpeta `trader/` de tu
proyecto.

## Sesiones

Cripto no cierra nunca, así que "la sesión" sigue el horario de las bolsas,
que es cuando cripto mueve más volumen. Cada día se calcula con su propio
horario de verano o de invierno.

| sesión | abre | UTC (invierno del norte) | Argentina |
| --- | --- | --- | --- |
| `europa` | 08:00 Londres | 08:00 | 05:00 |
| `wallstreet` | 09:30 Nueva York | 14:30 | 11:30 |
| `europa-wallstreet` | Londres hasta el cierre de Nueva York | 08:00-21:00 | 05:00-18:00 |

## Créditos

`crypto-scanner`, `crypto-entry`, `crypto-exit` y `crypto-timemachine` son
adaptaciones a cripto de `trader-scanner`, `trader-entry`, `trader-exit` y
`trader-timemachine` del repo
[Jakeschincariol/day-trader-skill](https://github.com/Jakeschincariol/day-trader-skill),
con licencia MIT. Su aviso de copyright está en `LICENSE-day-trader-skill`.

## Aviso

Esto es análisis de datos, no consejo de inversión. Una simulación hecha con
los últimos 60 días no predice el futuro: noticias, liquidaciones en cadena o
la caída de una exchange pueden hacer cosas que esos días nunca hicieron.
Operar con apalancamiento puede hacerte perder todo lo que pusiste. Practicá
primero en el modo demo de tu exchange.
