# Instrucciones del proyecto

## Publicación: un único sitio, esta rama

Todo el desarrollo y despliegue de este dashboard vive **únicamente** en este
repositorio (`javierbarriusom-a11y/finanzas-casa-def`), publicado en
**`https://javierbarriusom-a11y.github.io/finanzas-casa-def/`** vía
`.github/workflows/pages.yml` (despliegue automático en cada push a `main`).

Existe una copia paralela, `javierbarriusom-a11y/contabilidadcasa`
(`https://javierbarriusom-a11y.github.io/contabilidadcasa/`), creada el 9 de
agosto de 2026 como **foto fija de un momento dado** (E19 completo + E20-0
días 1-4), a petición explícita del usuario. Esa copia **no se mantiene**:
no recibe pushes automáticos, no tiene el chequeo de disponibilidad
recurrente (se quitó deliberadamente de ese repo) y no debe tratarse como un
segundo entorno de desarrollo.

**Por defecto, y salvo instrucción explícita en contra en la conversación:**
- Todo cambio de código, commit y push va a este repositorio y a la rama de
  trabajo en curso — nunca a `contabilidadcasa`.
- No sincronizar, replicar ni desplegar nada hacia `contabilidadcasa`.
- No crear más copias/espejos en otras URLs de GitHub Pages sin que el
  usuario lo pida de nuevo explícitamente.
- Esta decisión no necesita repetirse en cada sesión: ya quedó tomada aquí.

## Commit y push: sin pedir permiso cada vez

Decisión del usuario del **10 de agosto de 2026**, que **anula el paso 4 del Modo
Cierre** de la skill `finanzas-casa-workflow` (el que exigía un «sí» explícito en
cada turno antes de `git add`/`commit`/`push`):

> «En adelante hazlos directamente en cada tarea si están listos para publicar.»

Es decir: cuando una tarea está terminada y **la validación ha pasado de verdad**,
se hace commit y push a la rama de trabajo en curso sin preguntar, y se abre el PR
en borrador. Sigue vigente todo lo demás del Modo Cierre:

- Validar primero (`npm run verify`, o como mínimo `npm test` diciéndolo). **Si algo
  falla, no se publica**: se informa del fallo y se ofrece corregirlo.
- Actualizar `PROJECT_STATE.md` (y `BACKLOG_STATUS.md` si cambia el estado de una
  entrega) con las cifras reales de esa validación, nunca inventadas.
- Nunca push directo a `main`, y nunca a `contabilidadcasa`.

Esta autorización tampoco necesita repetirse en cada sesión: ya quedó tomada aquí.
