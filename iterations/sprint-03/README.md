# Sprint 3 — Consultar transporte público del campus

## 1. Estado y fuente de información

- **Estado:** propuesta de Sprint. La PR #34 de transporte está cerrada y el trabajo se relacionó con la rama de Sprint 2; la PR principal #32 hacia `main` sigue abierta.
- No declarar las funciones integradas hasta comprobarlas en `main`. Métricas de una rama no son resultados aceptados.

## 2. Sprint Goal

> Como estudiante o visitante, quiero consultar líneas/paradas de autobús del campus y comparar una alternativa disponible con caminar, para elegir un medio con información y límites claros.

## 3. Historias candidatas y criterios de aceptación

| Historia candidata | Resultado de valor | Criterio observable y evidencia |
| --- | --- | --- |
| [HU-022 — Comparar medios](../../requirements/user-stories/03-rutas-y-transporte.md#hu-022--consultar-rutas-con-diferentes-medios) | Consultar alternativas disponibles. | Cada medio indica duración/distancia, tramos a pie y disponibilidad; se puede abrir el detalle. |
| [HU-026 — Consultar una línea](../../requirements/user-stories/03-rutas-y-transporte.md#hu-026--consultar-una-línea-de-autobús) | Ver recorrido y paradas ordenadas. | Horarios solo si la fuente los proporciona; operador, procedencia y fecha visibles. |
| [HU-027 — Consultar una parada](../../requirements/user-stories/03-rutas-y-transporte.md#hu-027--consultar-una-parada) | Consultar servicios de una parada y ruta hasta ella. | Nombre, líneas y estado de actualización; próximos horarios solo con fuente vigente. |

HU-028 (tiempo real) queda fuera hasta disponer de fuente compatible y autorizada.

## 4. Plan inicial y dependencias

- Depende de rutas peatonales y geometría trazable de Sprint 2.
- Confirmar operador, fuente autorizada, licencia, horarios y fecha de actualización.
- Diferenciar horario planificado, estimación local y dato en tiempo real.
- Comparar medios solo con supuestos visibles; no garantizar tiempos estimados.
- Incidencias se planifican después de resolver autenticación y privacidad.

## 5. Riesgos — RSGR

| Riesgo | Probabilidad / consecuencia / prioridad inicial | Reducción y seguimiento | Contingencia |
| --- | --- | --- | --- |
| Datos de línea/parada sin fuente clara → información errónea | Ocasional / Seria / Media | Registrar operador, licencia, fecha, método y revisión. | Ocultar datos no verificables o etiquetarlos como aproximados. |
| Feed real inexistente/no autorizado → falsa actualidad | Probable / Seria / Alta | No planificar HU-028 como entregable; verificar feed y términos. | Mantener horarios publicados con fecha o retirar capa. |
| Estimaciones poco realistas → mala decisión | Ocasional / Seria / Media | Documentar supuestos y validar ejemplos; marcar como estimación. | Mostrar opciones disponibles sin ranking o posponer comparación. |

## 6. Verificación y Definition of Done

- Caja negra: línea/parada desconocida, sin horario, dato vencido y alternativa no disponible.
- Integración: ruta a pie hasta parada, alternativa de bus y recorrido en mapa.
- Validar atribución, operador, licencia, fecha y términos.
- Regresión de búsqueda/mapa/routing y pruebas UI en plataformas acordadas.
- Integración en `main` y evidencia reproducible antes de declarar Done.

## 7. Sprint Review y retrospectiva

Pendientes. Inspeccionar el recorrido y registrar feedback real; la PR cerrada de una rama no sustituye una Review.

## 8. Trabajo no terminado y siguiente paso

La integración depende del estado de PR #32. HU-028 permanece en backlog hasta confirmar una fuente autorizada. HU-050/053 no se dan por iniciadas por aparecer en una propuesta previa.
