# Skill cryptos · jeto1337

[English](README.md) · **Español**

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
`api.coingecko.com`, `query1.finance.yahoo.com` y `query2.finance.yahoo.com`
(y `www.theguardian.com`, `rss.nytimes.com` y `feeds.bbci.co.uk` para las
noticias).

## Las skills

| comando | qué hace |
| --- | --- |
| `/crypto-scanner` | Qué cripto rompe el rango de apertura de **Europa** o de **Wall Street**, para arriba o para abajo, y los setups del gráfico diario (rupturas de 20 días, banderas, media de 20, sobreventa y sobrecompra). |
| `/crypto-entry` | El **temporizador de entrada**: vigila vela por vela y avisa el momento exacto en que una cripto cierra afuera del rango de apertura (o de un nivel), en largo o en corto. |
| `/crypto-exit` | El **plan de salida**: stop, objetivo y hora de salida antes de entrar, con el R neto de comisiones de Binance y el chequeo de liquidación según el apalancamiento. |
| `/crypto-risk` | El **gestor de riesgo**: revisa el plan contra tus límites (riesgo por operación, apalancamiento, liquidación, pérdidas del día), calcula la cantidad y arma la orden para cargar a mano en Binance. |
| `/crypto-alerts` | Las **alertas**: avisa cuando un precio pasa un nivel, y sigue tu operación (entrada, stop, objetivo, orden que no se llenó, hora de salir). |
| `/crypto-social-info` | La **información social y política**: verifica rumores y noticias con 5 fuentes confiables (diarios conocidos, voceros oficiales, economistas; X solo con tilde gris o dorado y nunca como confirmación), mide cómo se movió el precio con prohibiciones, leyes, elecciones, aranceles, adopción y escándalos desde 2017, y arma el calendario de eventos que vienen. |
| `/crypto-timemachine` | La **máquina del tiempo**: repite 10.000 veces el resto del día con las velas reales de 5 minutos de esa cripto en los últimos 60 días, prueba la regla en cada día pasado y te dice si el plan tiene ventaja o es tirar una moneda. |
| `/crypto-scalp` | Lee el mercado, elige las mejores criptos para scalping, calcula el tamaño de la posición según tu capital y tu riesgo (con apalancamiento, margen aislado y comisiones de Binance) y simula operaciones en papel con avisos. |

## Lo que mostraron los datos

Con 36 eventos sociales y políticos verificados, de 2017 a 2026
(`/crypto-social-info`). Son pocos casos y los eligieron personas: sirven de
pista, no son reglas.

- **Las malas noticias pesan más que las buenas.** Después de una mala
  noticia, bitcoin bajó durante la semana siguiente en 10 de 12 casos (5 de 5
  desde 2023). Después de una buena, subió en solo 10 de 21: menos que una
  semana cualquiera.
- **Se compra el rumor, se vende la noticia.** Lo que se esperaba hacía meses
  (aprobación de los ETF, el decreto de la reserva de bitcoin, la salida a
  bolsa de Coinbase) subió antes y bajó después.
- **Las sorpresas positivas sí empujan** (Xi Jinping y el blockchain en 2019,
  Tesla en 2021, la elección de EE.UU. en 2024).
- **Las prohibiciones dan caídas que en un mes se recuperan.**
- **Si la noticia nombra una cripto, esa se mueve mucho más** que bitcoin (XRP
  +73 % el día del fallo a favor de Ripple).

## Cómo se verifican las noticias

| veredicto | cuándo |
| --- | --- |
| **VERIFICADA** | un documento oficial la confirma, o al menos 4 fuentes confiables confirman los mismos datos (quién, qué, cuándo, cuánto) y son el 80 % o más de las que hablan del tema, con al menos 2 diarios independientes y sin desmentido |
| **DUDOSA** | le falta poco para eso, datos que no coinciden, un desmentido de una fuente confiable, o tiene menos de una hora |
| **FALSA** | desmentido oficial, o 2 confirmaciones o menos |

Las noticias de alto impacto (aprobación de un ETF, una prohibición, un
gobierno que compra o vende bitcoin) piden 6 confirmaciones, 85 %, de 2
regiones o más, con una agencia internacional (Reuters, AP, AFP, Bloomberg...)
o un documento oficial.

Las fuentes confiables están ordenadas por país (26 países, entre ellos donde
más se compra cripto: EE.UU., Rusia, Reino Unido, Alemania, Ucrania, Francia,
Pakistán, Vietnam, Brasil, Nigeria, Indonesia, Corea del Sur, Japón e India), y
cada verificación se muestra agrupada por país. Los medios estatales (TASS,
Xinhua, VNA, Antara...) cuentan como la voz de su gobierno, nunca como
confirmación independiente.

Fuentes confiables: diarios y agencias conocidos, voceros oficiales de los
países y economistas reconocidos. Los medios cripto y los blogs no cuentan. De
X solo se toman cuentas con tilde gris o dorado, y nunca como confirmación.

La fecha: que sea verdad no quiere decir que sea de hoy. La edad se cuenta
desde la primera nota confiable: **NUEVA** (menos de 24 horas, se puede operar),
**RECIENTE** (24 a 72 horas, buena parte ya está en el precio) o **VIEJA** (más
de 72 horas: contexto, no una razón para operar). Una confirmación más de 7
días anterior a las demás habla de otro hecho y no cuenta, y una noticia que
vuelve a circular más de un día después de la primera nota se marca
**RECICLADA**. Cada medio cuenta una sola vez.

Tres controles más:

- **Fuentes anónimas** ("según fuentes cercanas") cuentan todas juntas como una
  sola confirmación: cinco diarios que citan a "una persona al tanto" pueden
  estar citando a la misma persona.
- **Prueba en la blockchain.** Los hackeos, las ballenas y las ventas de un
  gobierno se ven en la cadena. `--onchain "btc|TXID|4259"` lee la transacción
  en mempool.space (Bitcoin) o eth.blockscout.com (Ethereum): el monto correcto
  en la cadena más 2 diarios independientes que digan de quién es queda
  verificada; una transacción que no existe es falsa. La cadena prueba que se
  movió la plata, nunca de quién es la dirección.
- **¿Ya está en el precio?** `--dir -` (noticia mala) o `--dir +` mide cuánto se
  movió la cripto desde la primera nota contra lo normal. Dos veces lo normal o
  más a favor de la noticia: no persigas el movimiento.

`chain` suma el estado de la red a la revisión del mercado: las comisiones de
Bitcoin contra los últimos 15 bloques, el mempool, cada movimiento de 1.000 BTC
o más en los últimos 6 bloques y el gas de Ethereum. Es contexto, no una señal:
un movimiento grande no es una venta.

Por qué una noticia de menos de una hora nunca queda verificada: en enero de
2024 hackearon la cuenta de la SEC en X y publicaron que aprobaban los ETF de
bitcoin. Muchos medios lo repitieron en minutos, y el precio saltó y cayó antes
del desmentido.

## Cómo se usan juntas

```
/crypto-social-info  ¿qué noticias hay? ¿son verdad? ¿qué se viene?
/crypto-scanner      qué rompió en la apertura
/crypto-entry        el momento exacto de entrar      -> trader/entry.json
/crypto-exit         stop, objetivo y hora de salida  -> trader/plan.json
/crypto-timemachine  ¿ese plan tiene ventaja?
/crypto-risk         ¿entra en mis límites? cuánto abrir y la orden para Binance
/crypto-alerts       vigila la operación mientras está abierta
```

Cada skill lee lo que escribió la anterior en la carpeta `trader/` de tu
proyecto.

**Regla: `/crypto-social-info` va siempre primero.** Antes de buscar una
ruptura, mirá el calendario y las noticias del día, y verificá lo importante.
Una noticia mala verificada y nueva (de las últimas 24 horas): preferí cortos y achicá
los largos; si es vieja, ya está en el precio. Un evento
grande en las próximas horas (inflación, la Fed, una votación, un fallo): menos
tamaño o esperar. Una noticia dudosa no decide nada hasta que se verifique.

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

`crypto-scanner`, `crypto-entry`, `crypto-exit`, `crypto-timemachine`,
`crypto-risk` y `crypto-alerts` son adaptaciones a cripto de las skills
`trader-*` equivalentes del repo
[Jakeschincariol/day-trader-skill](https://github.com/Jakeschincariol/day-trader-skill),
con licencia MIT. Su aviso de copyright está en `LICENSE-day-trader-skill`.

## Aviso

Esto es análisis de datos, no consejo de inversión. Una simulación hecha con
los últimos 60 días no predice el futuro: noticias, liquidaciones en cadena o
la caída de una exchange pueden hacer cosas que esos días nunca hicieron.
Operar con apalancamiento puede hacerte perder todo lo que pusiste. Practicá
primero en el modo demo de tu exchange.
