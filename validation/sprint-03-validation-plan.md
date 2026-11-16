# Plan de validación — Sprint 3

**Estado:** Pruebas unitarias, de caja negra, de integración basadas en hilos y de regresión completadas localmente con 210 pruebas aprobadas (100 %) y más del 98 % de cobertura de código. Pendiente de integración y aprobación de Pull Request.

Relacionado con [Sprint 3 — Multimodalidad EMT y Gestión de Incidencias en Campus](../iterations/sprint-03/README.md) y con las historias `HU-022`, `HU-026`, `HU-027`, `HU-050`, `HU-053` y `HU-094`.

---

## 1. Prerrequisitos

* Monorepositorio con entorno Node.js v24 y TypeScript 6 configurado.
* Dependencias de `@unimovil/contracts`, `@unimovil/api` y `@unimovil/mobile` instaladas y compiladas.
* Definición formal de contratos para incidencias ciudadanas/universitarias (`packages/contracts/src/incidents.ts`) y transporte multimodal (`packages/contracts/src/transit.ts`).
* Catálogo estructurado de paradas y trazados de las líneas G y F de la EMT en Ciudad Universitaria (`transit-data.ts`).
* Almacén de incidencias reactivo con soporte de suscripciones cartográficas (`IncidentStore`).
* Límites geográficos del campus de Moncloa fijados (Bounding Box: latitud $[40.440, 40.460]$, longitud $[-3.738, -3.715]$).

---

## 2. Escenarios Previstos de Validación

| ID | Escenario | Resultado esperado | Criterio de Aceptación / HU |
| :--- | :--- | :--- | :--- |
| **V3-01** | Comparativa multimodal simultánea (a pie vs. autobús). | El sistema calcula en paralelo el tiempo a pie y el tiempo en autobús EMT (Líneas G o F), mostrando ambas alternativas en la tarjeta de ruta. | `HU-022` |
| **V3-02** | Recomendación inteligente de medio de transporte según distancia. | Para distancias cortas ($\le 500\text{ m}$) se recomienda ir a pie; para distancias mayores se destaca el autobús si ahorra tiempo de trayecto. | `HU-022` |
| **V3-03** | Visualización del recorrido y paradas de las líneas EMT en el mapa. | Se renderizan las polilíneas con el color corporativo oficial de la EMT y los marcadores de parada con sentido de circulación (Moncloa - Paraninfo). | `HU-026` |
| **V3-04** | Consulta interactiva de una parada de autobús universitaria. | Al pulsar sobre una parada, la ficha muestra su denominación oficial, código EMT, líneas asociadas y estimación de próximos pasos. | `HU-027` |
| **V3-05** | Partición de equivalencia válida (CE-V) en reporte de incidencia. | El formulario acepta títulos con caracteres acentuados, tipos normalizados (`obra`, `desvio`, `rampa_averiada`, `acera_cortada`), severidades válidas y coordenadas interiores. | `HU-050` / Pruebas de Caja Negra |
| **V3-06** | Partición de equivalencia no válida (CE-NV) por textos vacíos o XSS. | El sistema rechaza títulos vacíos, caracteres de script malicioso (`<script>`, `javascript:`) y tipos de incidencia desconocidos. | `HU-050` / Pruebas de Caja Negra |
| **V3-07** | Análisis de valores límite (VL) en longitud de título y descripción. | Títulos de 2 caracteres son rechazados (límite inferior no válido); 3 caracteres son aceptados (límite inferior válido); 80 son aceptados (límite superior válido); 81 son rechazados. | `HU-050` / Valores Límite |
| **V3-08** | Análisis de valores límite (VL) en coordenadas geográficas de campus. | Puntos situados en la frontera exacta del Bounding Box de Moncloa son admitidos; puntos desplazados $0,0001^\circ$ hacia el exterior son rechazados con error de fuera de campus. | `HU-050` / Valores Límite |
| **V3-09** | Hilo de integración principal: Secuencia completa de reporte. | La secuencia móvil interactiva (Formulario móvil $\rightarrow$ Validación de contrato $\rightarrow$ Persistencia temporal en almacén $\rightarrow$ Emisión y refresco de GeoJSON para MapLibre) se ejecuta sin pérdidas. | `HU-050` / `HU-053` / Pruebas por Hilos |
| **V3-10** | Hilo de interrupción por fallo de validación de datos. | Al introducir datos corruptos, la validación intercepta la petición, no altera el almacén de datos y evita repintados falsos en el mapa. | `HU-050` / Pruebas por Hilos |
| **V3-11** | Hilo de ciclo de vida: Resolución y retirada de marcadores. | Una incidencia que pasa a estado `resuelta` se actualiza en el almacén y se excluye automáticamente de la capa de incidencias activas del mapa. | `HU-053` / Pruebas por Hilos |
| **V3-12** | Degradación elegante ante indisponibilidad del servicio de la EMT. | Si la red de la EMT no responde o experimenta caídas, la app no se bloquea y ofrece la ruta a pie calculada localmente como alternativa funcional garantizada. | `HU-094` (Resiliencia) |
| **V3-13** | Reintento con retroceso exponencial ante anomalías transitorias de transporte. | Las consultas de estimación de llegada se reintentan hasta 3 veces con demoras crecientes ($10\text{ ms}$, $20\text{ ms}$) antes de catalogar el servicio como inaccesible. | `HU-094` (Criterio 3) |
| **V3-14** | Sanitización estricta de credenciales en errores de transporte. | Se eliminan claves privadas, tokens y cabeceras de autorización de las respuestas de error antes de persistir trazas de depuración técnica. | `HU-094` (Criterio 5) |
| **V3-15** | Pruebas de regresión y rendimiento sin degradación de cálculos previos. | La incorporación de las líneas de la EMT no altera las rutas peatonales del sprint anterior y la conversión a GeoJSON de 50 repintados se ejecuta en menos de $200\text{ ms}$. | Pruebas de Regresión |

---

## 3. Umbrales de Aceptación (Quality Gates)

| Métrica / Control | Umbral Exigido | Resultado Obtenido en Sprint 3 | Estado |
| :--- | :--- | :--- | :---: |
| **Cobertura de sentencias (Statements)** | $\ge 90\,\%$ | **$98,31\,\%$** | ✅ Superado |
| **Cobertura de ramas (Branches)** | $\ge 85\,\%$ | **$94,95\,\%$** | ✅ Superado |
| **Cobertura de funciones (Functions)** | $\ge 90\,\%$ | **$98,03\,\%$** | ✅ Superado |
| **Cobertura de líneas (Lines)** | $\ge 90\,\%$ | **$98,42\,\%$** | ✅ Superado |
| **Tasa de éxito de pruebas automáticas** | $100\,\%$ | **$100\,\%$** (210 tests pasados, 0 fallos) | ✅ Superado |
| **Tiempo de conversión GeoJSON de transporte** | $\le 50\text{ ms}$ | **$< 5\text{ ms}$** por ciclo cartográfico | ✅ Superado |
| **Seguridad de datos técnicos (HU-094)** | Cero credenciales expuestas | **$100\,\%$ sanitizado** mediante políticas de ofuscación | ✅ Superado |
