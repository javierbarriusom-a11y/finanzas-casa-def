# Sistema de diseño E19 — origen y catálogo de pantallas

Este documento es el que `design-tokens.css` cita desde su cabecera ("extraídos a un
lenguaje de tokens reutilizable en docs/E19_SISTEMA_DISENO.md") y que hasta ahora no
existía en el repositorio. Recoge de dónde sale el sistema de diseño E19, qué tokens y
componentes ya están construidos, y el catálogo completo de las 15 pantallas mockup que
lo originaron — migradas o pendientes.

## 1. Origen

El sistema E19 nace de un documento de mockups aportado por el usuario ("Finanzas Casa ·
Mockups"), un canvas de diseño con tres bloques de exploración ("turns") y 15 variantes de
pantalla en total. El archivo original se conserva en
`docs/mockups/finanzas-casa-mockups.dc.html` (formato canvas de diseño; las capturas
estáticas por pantalla están en `docs/mockups/screens/`). Es material de referencia
interno del repositorio, no se sirve desde `index.html` ni se enlaza al sitio público.

El propio mockup usa Inter como tipografía, fondo `#F0EEE9`, azul de acento `#0072E3` y
la paleta semántica (verde éxito, ámbar aviso, terracota deuda, rojo peligro) que
`design-tokens.css` reproduce exactamente — confirmando que los tokens ya en el repo
vienen literalmente de este documento, no de una interpretación libre.

## 2. Tokens (ya implementados en `design-tokens.css`)

### Superficies y bordes
| Token | Valor | Uso |
|---|---|---|
| `--e19-canvas` | `#f0eee9` | Fondo de página |
| `--e19-surface` | `#ffffff` | Tarjetas, tablas |
| `--e19-surface-soft` | `#fbfcf7` | Superficies secundarias (mockup: fondo de `.dv-card`) |
| `--e19-surface-sunken` | `#f6f4ee` | Cabeceras de tabla, fondos hundidos |
| `--e19-border` / `--e19-border-strong` | `#e8ecf1` / `#d8dde5` | Bordes suaves / marcados |

### Texto
| Token | Valor | Uso |
|---|---|---|
| `--e19-ink` | `#0b1220` | Texto principal |
| `--e19-heading` | `#293e5e` | Títulos |
| `--e19-muted` | `#5b6578` | Texto secundario |
| `--e19-faint` | `#a9b1bf` | Texto terciario / metadatos |
| `--e19-eyebrow` | `#049ff9` | Etiquetas "eyebrow" en mayúsculas (p. ej. "DECIDIR · ESCENARIOS DE VIDA") |

### Acento y semántica
| Token | Valor | Significado, siempre el mismo en toda la app |
|---|---|---|
| `--e19-accent` / `--e19-accent-hover` | `#0072e3` / `#005bb8` | Acción primaria |
| `--e19-accent-strong` | `#0b1a30` | Fondo oscuro (barra de impacto, tarjetas "recomendada") |
| `--e19-success` | `#1f9d55` | Positivo (aplicada, holgado, sube) |
| `--e19-warning` | `#c78b12` | Alerta suave (justo, roza el límite) |
| `--e19-debt` | `#ad725b` | Deuda (terracota, distinto de `danger`) |
| `--e19-danger` | `#c13b3b` | Rechazado, bajo reserva, rompe un límite |

### Tipografía y forma
Escala: `--e19-text-eyebrow` (11px) → `--e19-text-display` (28px), familia Inter con
fallback de sistema. Radios: `--e19-radius-sm` (8px, botones/inputs) → `--e19-radius-lg`
(14px, tarjetas) → `--e19-radius-pill` (badges/pills). Sombras: `--e19-shadow-card` sutil,
`--e19-shadow-pop` para estados hover/foco.

## 3. Componentes ya construidos

`.e19-card`, `.e19-card-strong`, `.e19-card-accent-soft` (superficies) · `.e19-btn-primary
/-secondary/-dark` (botones) · `.e19-kpi` con modificadores `.is-warn`/`.is-danger` y
`.e19-kpi-delta.is-up/-down/-warn` (métricas con highlight de estado) · `.e19-insight`
(lectura destacada con borde de color) · `.e19-badge-*` y `.e19-pill-*` (estado puntual vs.
histórico) · `.e19-table` (jerarquía por fila, alineación numérica) · `.e19-impact-bar`
(barra fija oscura para el resumen de impacto, ver mockup 3a) · `.e19-stepper`,
`.e19-route-card`, `.e19-explainer`, `.e19-next-step` (patrones de flujo guiado, de
`update-hub`/`data-entry`).

Patrón de aplicación: cada pantalla migrada añade una clase de ámbito propia
(`.e19-home`, `.e19-update-hub`, `.e19-data-entry`, `.e19-forecast`, `.e19-prevision`,
`.e19-escenario-motor`) y dentro de ella redefine solo lo que necesita — nunca toca una
clase o variable ya usada por otra pantalla. Es el mismo principio de "envolver, no
sustituir" que rige el resto del código (E14, E20): la piel visual se añade capa a capa,
nunca se reescribe.

## 4. Catálogo de las 15 pantallas del mockup

Los tres bloques ("turns") del documento y sus variantes, con la pantalla real de la app
a la que corresponden y su estado de migración a día de hoy.

### Turno 1 — Finanzas Casa · rediseño de escritorio (1280px)

| # | Título del mockup | Pantalla real | Estado |
|---|---|---|---|
| 1a | Hoy · navegación reducida a cuatro verbos, una lectura y tres decisiones | `#home` | ✅ Migrada (E19-2) |
| 1b | Plan de deuda · ruta como línea de tiempo (dataviz A) | `#deuda-ruta` | ✅ Migrada (E20-2) |
| 1c | Plan de deuda · comparador de estrategias (dataviz B) | `#deuda-comparar` | ✅ Migrada (E20-2, parcial — ver nota) |
| 1d | Asesor ejecutivo · una decisión abierta a la vez | `#executive-advisor` | ⏳ Pendiente |
| 1e | Simulación nueva vida · simular → comparar → aplicar en una sola vista | `#escenario-simular` | ✅ Migrada (E20-1) |
| 1f | Actualizar mis datos · hub ordenado por lo que tienes delante | `#update-hub` | ✅ Migrada (E19-3) |
| 1g | Conciliación · las diferencias como tareas, no como tablas | `#conciliar` | ✅ Migrada (E20-2) |

### Turno 2 — Entrada y actualización de datos · previsión · aplicación de escenarios

| # | Título del mockup | Pantalla real | Estado |
|---|---|---|---|
| 2a | Registrar el mes · una fila por partida, guardado automático | `#update-data` | ⏳ Pendiente |
| 2b | Importar extracto · bandeja previa con cuatro pasos | `#data-entry` | ✅ Migrada (E19-4) |
| 2c | Previsión · el año como una banda, desglose del mes al clic | `#prevision` / `#forecast` | ✅ Migrada (E19-5) |
| 2d | Aplicar escenario · diferencia línea a línea antes de tocar el plan | `#escenario-aplicar` | ✅ Migrada (E20-1) |
| 2e | Escenarios guardados · cuál está aplicado, cuál caduca | `#escenario-guardados` | ✅ Migrada (E20-1, parcial — ver nota) |

### Turno 3 — Cuadro de mandos con impacto

| # | Título del mockup | Pantalla real | Estado |
|---|---|---|---|
| 3a | Editas una celda y el impacto aparece abajo, antes de guardar | *(no existe todavía)* | ⏳ Pendiente |
| 3b | Bandeja de cambios · efecto conjunto de todo lo tocado en la sesión | *(no existe todavía)* | ⏳ Pendiente |
| 3c | Mapa de calor · dónde duele cada cambio, sin leer una cifra | *(no existe todavía)* | ⏳ Pendiente |

## 5. Escenario: simular → aplicar → guardados (1e/2d/2e)

Los mockups 1e, 2d y 2e definen el flujo de decisión como **tres pantallas encadenadas**,
implementadas así desde E20-1: `#escenario-simular` (panel de controles a la izquierda,
gráfico plan-actual-vs-simulación con línea de reserva, KPIs de liquidez final / caja
mínima / libre de deuda, aviso si la simulación rompe un límite con botón "ajustar
automáticamente" que reintenta con `planificacion.modo: "optimo"` del motor real),
`#escenario-aplicar` (diff línea a línea, motivo obligatorio antes de confirmar) y
`#escenario-guardados` (lista de escenarios con estado y KPIs recalculados al vuelo sobre
el estado actual, nunca cifras congeladas).

Dos simplificaciones deliberadas frente al mockup, documentadas en vez de fabricadas:

- **Solo dos estados, no cuatro.** El mockup 2e muestra `aplicado / recomendado / guardado
  / caducado`. Aquí solo existen `aplicado`/`guardado`: "recomendado" necesitaría un motor
  de recomendación que no existe, y "caducado" un concepto de oferta con vencimiento que
  tampoco. Añadir esos dos con datos falsos habría sido peor que no tenerlos.
- **"Aplicar" no muta las deudas reales.** `DEBT_PORTFOLIO` es una constante del código
  fuente; no hay ni ha habido nunca, en ninguna pantalla de la app, un mecanismo para
  reescribirla desde la interfaz. "Confirmar y aplicar" registra el escenario como el
  aplicado en `#escenario-guardados` (con motivo y fecha, en `localStorage`) — no escribe
  en ningún dato real. Es honesto y reversible por construcción, pero no es literalmente
  el "commit al plan" que el mockup insinúa.

Alcance de tipos de decisión: igual que en E20-1 día 1, solo `amortizacion` está
conectada a estas tres pantallas. El resto de tipos que ya soporta el motor
(`canonical-scenario-engine.js`: refinanciación, reunificación, compra, imprevisto…) se
añadirán a los mismos tres controles en próximas fases, sin tener que rediseñar el flujo.

## 6. Deuda: comparar estrategias → ruta (1b/1c)

Los mockups 1b y 1c definen dos vistas del mismo plan de deuda: una comparación de
estrategias con nombre (1c) y el detalle cronológico de la elegida (1b). Implementadas en
E20-2 como `#deuda-comparar` y `#deuda-ruta`, construidas sobre el mismo motor que
Escenario (`resolveEscenario`) en vez de sobre el pipeline heredado de
`debt-liquidation-plan` (`DEBT_LIQUIDATION_ASSUMPTIONS`, entidades hardcodeadas): cada
estrategia es una lista de decisiones `amortizacion` (pago total, `planificacion.modo:
"optimo"`) sobre la cartera real (`canonicalDebtContractRows`), ordenada según el
criterio de la estrategia, y resuelta de verdad por el motor — nunca un número inventado.

**Solo tres estrategias, no cuatro.** El mockup 1c muestra "Quita + avalancha", "Bola de
nieve", "Reunificación" y "No tocar nada". Aquí solo hay **avalancha** (ordena por TAE
descendente), **bola de nieve** (ordena por saldo ascendente) y **no tocar nada** (sin
decisiones, referencia). "Reunificación" como estrategia hipotética exigiría inventar
unas condiciones de préstamo (TAE, plazo) que no existen todavía como oferta real en los
datos — documentado en la propia pantalla en vez de fabricar una cifra. El día que exista
una oferta de reunificación real registrada (como ya permite el flujo de ofertas de
`#debt-roadmap`/E14b), puede añadirse como estrategia comparable de verdad.

**Recomendada** = la estrategia viable (todas sus decisiones resueltas como "aplicada")
con la fecha de libre de deuda más temprana; en empate, la de menor coste total
ejecutado. `escenarioMotorLibreDeDeuda` no siempre devuelve una fecha real — puede
devolver "sin deuda pendiente", "sin fecha estimable" (queda un registro sin cuota activa,
p. ej. una reunificación histórica) o "fuera de horizonte"; comparar esos textos como
cadenas ordenaría mal, así que se traduce cada caso a un rango explícito antes de
comparar en vez de fiarse de una coincidencia alfabética.

**"Deuda a cero" ambas pantallas la reutilizan.** "Ver ruta"/"Aplicar la recomendada"
cargan las decisiones de la estrategia elegida directamente en
`escenarioMotorDecisions` y navegan a `#escenario-aplicar` — el mismo diff línea a línea
con motivo obligatorio de E20-1, sin reconstruir esa lógica. El gráfico de `#deuda-ruta`
("deuda viva vs. liquidez") recorta la ventana temporal a los ~6 meses tras saldarse la
última deuda (o 36 meses si no llega a saldarse en este horizonte): con el horizonte
completo del motor (hasta 10 años) la liquidez crece muy por encima del principal de
deuda y la aplana en un hilo invisible en una escala compartida.

**Reserva mínima con suelo por defecto.** El motor solo busca mes viable si se declara un
guardarraíl positivo; sin ninguno, "modo óptimo" no comprueba nada y todo cae en el
primer mes del horizonte sin importar cuánto quede la caja en negativo. Si el usuario no
ha configurado una reserva (aquí, o en Presupuesto de riesgo, `state.operatingReserve`),
se usa un suelo de 0 € por defecto — nunca "sin comprobar nada" en silencio — y el
checklist "antes de aplicar" deja explícito si la cifra es una reserva real configurada o
el suelo por defecto.

## 7. Conciliación (1g)

El mockup 1g reduce la conciliación a "qué falta para cerrar el mes": un título con el
número de tareas, KPIs de cobertura, una lista de tareas por causa ordenadas por impacto,
un checklist de qué implica cerrar y el histórico de meses anteriores. Implementado como
`#conciliar` (E20-2), es **puro reskin**: no reimplementa ni un cálculo — llama
literalmente a las mismas funciones que ya usaba la pantalla heredada `#reconciliation`
(`refreshCanonicalLedger`, `E11bInbox.reconciliationTasks`,
`FinanceCanonicalE5.latestMonthOperation`, `closeCurrentMonthTransaction`,
`downloadCanonicalLedger`) y solo cambia qué se muestra y cómo. `#reconciliation` sigue
intacta, sin tocar, para quien necesite el panel operativo completo (paridad histórica,
auditoría diaria, barrera de publicación) que el mockup no pide y `#conciliar`
deliberadamente no reproduce.

"Meses anteriores" deriva su estado (cerrado / reabierto N veces) de `monthClosures`, el
registro real de operaciones de cierre — no hay estados fabricados como "revisar" o
similar que no tengan un operación real detrás.
