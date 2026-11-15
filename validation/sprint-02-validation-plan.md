# Plan de validación — Sprint 2

**Estado:** Pruebas unitarias, de integración y de cobertura completadas localmente con 141 pruebas aprobadas y 99,27 % de cobertura de código. Pendiente de integración nativa en dispositivos y aprobación de Pull Request.

Relacionado con [Sprint 2 — Motor de Rutas Peatonales y Accesibilidad PMR](../iterations/sprint-02/README.md) y con las historias `HU-020`, `HU-021`, `HU-023`, `HU-024`, `HU-040` y `HU-094`.

---

## 1. Prerrequisitos

- Monorepositorio con entorno Node.js v24 y TypeScript 6 configurado.
- Dependencias de `@unimovil/contracts`, `@unimovil/api` y `@unimovil/mobile` instaladas.
- Definición formal del grafo peatonal de viales y sendas de Ciudad Universitaria (`campus-graph.ts`).
- Límites geográficos del campus de Moncloa fijados (Bounding Box: latitud $[40.440, 40.460]$, longitud $[-3.738, -3.715]$).
- Parámetros de velocidad de caminata calibrados a velocidad media peatonal ($4,5\text{ km/h} = 1,25\text{ m/s}$).

---

## 2. Escenarios Previstos de Validación

| ID | Escenario | Resultado esperado | Criterio de Aceptación / HU |
| :--- | :--- | :--- | :--- |
| **V2-01** | Selección de origen y destino válidos dentro del campus de Moncloa. | El sistema valida las coordenadas, ubica los nodos más cercanos y devuelve un itinerario con distancia y tiempo estimado. | `HU-020` / `HU-021` |
| **V2-02** | Cálculo de ruta peatonal estándar con conmutador PMR desactivado. | Devuelve el camino más corto en metros/tiempo, permitiendo el paso por escalinatas si acortan el recorrido. | `HU-021` |
| **V2-03** | Activación del conmutador de accesibilidad PMR (`accessibleOnly: true`). | El algoritmo excluye o penaliza aristas con escaleras sin rampa adaptada, recalculando por sendas accesibles con rampa homologada. | `HU-024` / `HU-040` |
| **V2-04** | Solicitud de ruta hacia un destino inaccesible para PMR (ej. mirador con solo escaleras). | El sistema devuelve error controlado `NO_ACCESSIBLE_ROUTE` con mensaje claro y sugerencia de desactivar PMR o elegir acceso alternativo. | `HU-024` / `HU-094` |
| **V2-05** | Introducción de puntos de origen y destino idénticos o separados por menos de 5 metros. | El sistema detecta coincidencia y rechaza la petición con código `IDENTICAL_POINTS`, solicitando puntos distintos sin bloquear la app. | `HU-020` / `HU-094` |
| **V2-06** | Introducción de un origen fuera de los límites de Moncloa. | Error `ORIGIN_OUT_OF_BOUNDS`, indicando al usuario que seleccione un punto dentro de Ciudad Universitaria. | `HU-020` / `HU-094` |
| **V2-07** | Introducción de un destino fuera de los límites de Moncloa. | Error `DESTINATION_OUT_OF_BOUNDS`, indicando al usuario que seleccione un destino dentro de Ciudad Universitaria. | `HU-020` / `HU-094` |
| **V2-08** | Despliegue de indicaciones paso a paso (`HU-023`). | Cada tramo del itinerario dispone de instrucción en lenguaje natural, distancia en metros y tiempo en segundos. | `HU-023` |
| **V2-09** | Simulación de pérdida de conectividad durante el cálculo de ruta (Offline). | Clasificación inmediata en categoría `OFFLINE`, mensaje accesible, recomendación de revisar Wi-Fi/datos y habilitación de botón de reintento. | `HU-094` (Crit. 1, 2, 3) |
| **V2-10** | Caída temporal del servidor backend (HTTP 500/503 o timeout). | Clasificación en `SERVER_ERROR`, mensaje sin jerga técnica y ejecución de reintento con backoff automático. | `HU-094` (Crit. 1, 2, 3) |
| **V2-11** | Preservación del estado del formulario tras un fallo de red o validación. | Los textos de origen, destino y la posición del conmutador PMR se mantienen intactos; no se borra la entrada del usuario. | `HU-094` (Crit. 4) |
| **V2-12** | Sanitización de registros de error (Seguridad en logs). | Los objetos de error registrados en depuración eliminan automáticamente tokens de autenticación, contraseñas y claves privadas. | `HU-094` (Crit. 5) |
| **V2-13** | Generación de polilínea GeoJSON para renderizado en mapa. | Se emite un Feature LineString con coordenadas en orden estándar GeoJSON `[longitud, latitud]` y metadatos de accesibilidad. | `HU-021` / MapLibre |
| **V2-14** | Partición en valores límite en la frontera exacta del Bounding Box. | Las coordenadas situadas exactamente en la frontera geográfica son aceptadas; las situadas a $0,0001^\circ$ por fuera son rechazadas. | Tema 3 (Caja Negra) |
| **V2-15** | Cobertura de todos los caminos independientes del algoritmo (McCabe $V(G) = 7$). | El conjunto básico de 7 caminos independientes se ejecuta al 100 % en la batería de pruebas unitarias con Vitest. | Tema 3 (Caja Blanca) |

---

## 3. Umbrales de Aceptación (Quality Gates)

| Métrica / Control | Umbral Exigido | Resultado Obtenido en Sprint 2 | Estado |
| :--- | :--- | :--- | :---: |
| **Cobertura de sentencias (Statements)** | $\ge 90\,\%$ | **$99,32\,\%$** | ✅ Superado |
| **Cobertura de ramas (Branches)** | $\ge 85\,\%$ | **$98,31\,\%$** | ✅ Superado |
| **Cobertura de funciones (Functions)** | $\ge 90\,\%$ | **$100,00\,\%$** | ✅ Superado |
| **Cobertura de líneas (Lines)** | $\ge 90\,\%$ | **$99,27\,\%$** | ✅ Superado |
| **Tiempo de cálculo de ruta en API** | $p95 \le 30\text{ ms}$ | **$< 10\text{ ms}$** (grafo de Moncloa) | ✅ Superado |
| **Seguridad de errores (HU-094)** | Cero credenciales en logs | **$100\,\%$ sanitizado** con regex de seguridad | ✅ Superado |
| **Cumplimiento de tipado estricto** | 0 errores TypeScript | **0 errores** en monorepo (`tsc --noEmit`) | ✅ Superado |
| **Calidad de código y linteo** | 0 errores ESLint (`--max-warnings=0`) | **0 errores, 0 avisos** | ✅ Superado |

---

## 4. Registro de Evidencias Automatizadas

- **Suite de pruebas ejecutada:** 10 suites de test, 141 pruebas unitarias e integradas (Vitest v5.0.3).
- **Módulos auditados:**
  - `packages/contracts/src/routes.ts`: Validación de límites, error codes y contratos.
  - `apps/api/src/routes/routes.service.ts`: Motor de Dijkstra, cálculo de tiempos y filtro PMR.
  - `apps/api/src/routes/routes.controller.ts`: Mapeo de códigos HTTP y excepciones REST.
  - `apps/mobile/src/features/routing/domain/routing.ts`: Formateo de unidades y GeoJSON.
  - `apps/mobile/src/features/routing/domain/routing-errors.ts`: Clasificador de errores, reintentos y sanitizador de logs de `HU-094`.
- **Resultado final:** 141 tests superados satisfactoriamente, 0 fallos.
