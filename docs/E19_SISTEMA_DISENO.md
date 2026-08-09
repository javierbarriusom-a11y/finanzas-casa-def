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
| 1b | Plan de deuda · ruta como línea de tiempo (dataviz A) | `#debt-roadmap` | ⏳ Pendiente |
| 1c | Plan de deuda · comparador de estrategias (dataviz B) | `#debt-roadmap` / `#debt-liquidation-plan` | ⏳ Pendiente |
| 1d | Asesor ejecutivo · una decisión abierta a la vez | `#executive-advisor` | ⏳ Pendiente |
| 1e | Simulación nueva vida · simular → comparar → aplicar en una sola vista | `#escenario-motor` (en construcción, E20-1) | ⚠️ Ver nota E20-1 abajo |
| 1f | Actualizar mis datos · hub ordenado por lo que tienes delante | `#update-hub` | ✅ Migrada (E19-3) |
| 1g | Conciliación · las diferencias como tareas, no como tablas | `#reconciliation` | ⏳ Pendiente |

### Turno 2 — Entrada y actualización de datos · previsión · aplicación de escenarios

| # | Título del mockup | Pantalla real | Estado |
|---|---|---|---|
| 2a | Registrar el mes · una fila por partida, guardado automático | `#update-data` | ⏳ Pendiente |
| 2b | Importar extracto · bandeja previa con cuatro pasos | `#data-entry` | ✅ Migrada (E19-4) |
| 2c | Previsión · el año como una banda, desglose del mes al clic | `#prevision` / `#forecast` | ✅ Migrada (E19-5) |
| 2d | Aplicar escenario · diferencia línea a línea antes de tocar el plan | *(no existe todavía)* | ⚠️ Ver nota E20-1 abajo |
| 2e | Escenarios guardados · cuál está aplicado, cuál caduca | *(no existe todavía)* | ⚠️ Ver nota E20-1 abajo |

### Turno 3 — Cuadro de mandos con impacto

| # | Título del mockup | Pantalla real | Estado |
|---|---|---|---|
| 3a | Editas una celda y el impacto aparece abajo, antes de guardar | *(no existe todavía)* | ⏳ Pendiente |
| 3b | Bandeja de cambios · efecto conjunto de todo lo tocado en la sesión | *(no existe todavía)* | ⏳ Pendiente |
| 3c | Mapa de calor · dónde duele cada cambio, sin leer una cifra | *(no existe todavía)* | ⏳ Pendiente |

## 5. Nota E20-1: el mockup real de "Escenario" es más amplio que el día 1 construido

Los mockups 1e, 2d y 2e definen el flujo completo de decisión como **tres pantallas
encadenadas**, no una: **1e** "simular" (panel de controles a la izquierda — sliders y
selects por tipo de decisión —, gráfico plan-actual-vs-simulación con línea de reserva,
KPIs de liquidez final / caja mínima / mes libre de deuda, aviso si la simulación rompe un
límite con botón "ajustar automáticamente"); **2d** "aplicar" (diff línea a línea de lo
que cambiaría, con motivo obligatorio antes de confirmar); **2e** "guardados" (lista de
escenarios con su estado — aplicado / recomendado / guardado / caducado — y comparador).

La pantalla `#escenario-motor` construida en E20-1 día 1 (formulario + tabla de
decisiones + dos KPIs) resuelve el mismo problema de fondo — conectar
`canonical-scenario-engine.js` a la interfaz con datos reales — pero con una interacción
mucho más simple que la diseñada, y sin las tres pantallas separadas (simular, aplicar,
guardar). Se construyó así porque el mockup no había llegado todavía a la sesión cuando
se implementó el día 1. Pendiente de decisión del usuario: rediseñar `#escenario-motor`
hacia este mockup real ahora, o seguir sumando tipos de decisión con el patrón actual y
reconciliar visualmente más adelante.
