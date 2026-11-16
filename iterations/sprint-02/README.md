# Sprint 2 — Calcular rutas peatonales accesibles

## 1. Estado y fuente de información

- **Estado:** trabajo propuesto en [PR #32](https://github.com/ddavid07/UniMovil/pull/32), abierta hacia `main`; no es incremento aceptado.
- La versión anterior decía “Completado y Verificado”, contradicho por el estado abierto de la PR principal.
- No constan fechas, capacidad, selección acordada ni métricas aceptadas.

## 2. Sprint Goal

> Como persona que se desplaza por Moncloa, quiero elegir origen y destino y consultar una ruta peatonal con información accesible conocida, para planificar el recorrido y entender sus límites.

## 3. Historias candidatas y criterios de aceptación

| Historia candidata | Resultado de valor | Criterio observable y evidencia |
| --- | --- | --- |
| [HU-020 — Introducir origen y destino](../../requirements/user-stories/03-rutas-y-transporte.md#hu-020--introducir-origen-y-destino) | Seleccionar dos puntos válidos. | Búsqueda/mapa permiten elegirlos; se validan entradas incompletas o inválidas. |
| [HU-021 — Consultar una ruta a pie](../../requirements/user-stories/03-rutas-y-transporte.md#hu-021--consultar-una-ruta-a-pie) | Ver trazado, distancia y duración estimadas. | Indicaciones ordenadas; explica si no hay ruta; datos/límites visibles. |
| [HU-023 — Consultar indicaciones](../../requirements/user-stories/03-rutas-y-transporte.md#hu-023--consultar-indicaciones-paso-a-paso) | Seguir recorrido por instrucciones. | Pasos ordenados y vinculados al tramo del mapa. |
| [HU-024 — Consultar una ruta accesible](../../requirements/user-stories/03-rutas-y-transporte.md#hu-024--consultar-una-ruta-accesible) | Evitar barreras conocidas. | Filtra obstáculos verificados; desconocidos no se presentan como accesibles; explica si no existe ruta accesible conocida. |

HU-040/041 se refinan junto a HU-024; un conmutador no las completa si faltan criterios.

## 4. Plan inicial y dependencias

- Depende del mapa/catálogo y una representación peatonal trazable del campus.
- Verificar procedencia y cobertura del grafo, y semántica de accesibilidad antes de llamar a la ruta real.
- Separar cálculo de dominio, contrato API y presentación móvil.
- No afirmar “distancia exacta”, “acceso homologado” o garantía PMR sin medición/fuente.
- Selección y estimación final en Sprint Planning.

## 5. Riesgos — RSGR

| Riesgo | Probabilidad / consecuencia / prioridad inicial | Reducción y seguimiento | Contingencia |
| --- | --- | --- | --- |
| Grafo incompleto/inexacto → ruta insegura o imposible | Probable / Crítica / Alta | Revisar fuente, cobertura, conectividad y límites; registrar zonas sin modelo. | Limitar cobertura, devolver “sin dato” y bloquear garantías PMR. |
| Atributos PMR no verificados → falsa confianza | Probable / Crítica / Alta | No asumir accesible por defecto; validar fuente, fecha y estado. | Retirar indicación de accesibilidad y mostrar limitación. |
| Algoritmo/contrato complejo → regresiones | Ocasional / Seria / Media | Caja blanca en decisiones/caminos; caja negra en equivalencias/fronteras; CI de regresión. | Reducir alcance y replanificar lo restante sin relajar checks. |

## 6. Verificación y Definition of Done

- Caja negra: origen=destino, fuera de cobertura, entradas inválidas, ruta inexistente y preferencia PMR.
- Caja blanca: decisiones/caminos relevantes; documentar cómo se obtiene V(G).
- Integración: selección → contrato → servicio → respuesta → renderizado.
- Regresión de mapa/búsqueda; builds nativos acordados; CI aplicable en verde.
- Trazabilidad a criterios HU-020/021/023/024. PR integrada en `main` antes de Done.

El [diseño QA Sprint 2](../../validation/sprint-02-qa-testing-design.md) y el [plan de validación](../../validation/sprint-02-validation-plan.md) son diseño; actualizar resultados solo tras ejecución comprobada.

## 7. Sprint Review y retrospectiva

Pendientes; no se registra Review ni feedback confirmado.

## 8. Trabajo no terminado y siguiente paso

Resolver CI/aceptación de PR #32 y verificar el grafo y atributos de accesibilidad. Reordenar HU-040/041; no asumir que el trabajo pasa automáticamente al Sprint 3.
