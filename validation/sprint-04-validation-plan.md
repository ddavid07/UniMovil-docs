# Plan de validación — Sprint 4

**Estado:** Pruebas de sistema basadas en casos de uso, pruebas de recuperación, pruebas de seguridad de endpoints y matriz de trazabilidad completadas con 250 pruebas aprobadas (100 %) y más del 98 % de cobertura de código.

Relacionado con [Sprint 4 — Panel Web Admin, Validación Global del Sistema y Cierre Académico](../iterations/sprint-04/README.md) y con las historias `HU-001` a `HU-098`, con foco técnico en `HU-090`, `HU-091`, `HU-094` y `HU-095`.

---

## 1. Prerrequisitos

* Monorepositorio configurado con Node.js v24 y TypeScript 6 en modo estricto.
* Dependencias y paquetes transversales `@unimovil/contracts`, `@unimovil/testing`, `@unimovil/api` y `@unimovil/mobile` instalados y compilados.
* Grafo topológico peatonal del campus de Moncloa con nodos clave (Metro Ciudad Universitaria, facultades, paradas de autobús) y atributos de accesibilidad PMR.
* Módulos de almacenamiento reactivo de incidencias (`IncidentStore`) y persistencia local en caché (`OfflineCache`).
* Servicios de clasificación de errores técnicos y ofuscación de credenciales (`routing-errors.ts`).
* Bounding Box geográfico de Ciudad Universitaria delimitado ($[40.440, 40.460]$ latitud, $[-3.738, -3.715]$ longitud).
* Matriz formal de trazabilidad vinculando el catálogo íntegro de 68 historias de usuario con sus suites de prueba.

---

## 2. Escenarios Previstos de Validación

| ID | Escenario | Resultado esperado | Criterio de Aceptación / HU |
| :--- | :--- | :--- | :--- |
| **V4-01** | Búsqueda de edificio y navegación peatonal completa (CU-SYS-01). | El usuario localiza la facultad en el buscador, consulta sus datos, solicita la ruta a pie y recibe el itinerario óptimo con instrucciones paso a paso y GeoJSON para MapLibre. | `HU-010`, `HU-013`, `HU-020`, `HU-021` |
| **V4-02** | Navegación accesible PMR con filtro de barreras (CU-SYS-02). | El itinerario adaptado excluye tramos con escaleras, prioriza rampas y pasos llanos, garantizando accesibilidad total a personas de movilidad reducida. | `HU-024`, `HU-040`, `HU-041`, `HU-095` |
| **V4-03** | Comparativa multimodal simultánea con líneas EMT (CU-SYS-03). | El sistema evalúa en paralelo el tiempo a pie y en autobús (Líneas G y F), presentando la recomendación óptima según la distancia del trayecto. | `HU-022`, `HU-025`, `HU-026`, `HU-027` |
| **V4-04** | Reporte ciudadano de incidencia y refresco cartográfico (CU-SYS-04). | El reporte supera la validación de contrato, se almacena en el registro reactivo y se refleja en el mapa con el marcador del color correspondiente a su severidad. | `HU-050`, `HU-053` |
| **V4-05** | Ciclo de vida y retirada tras resolución de incidencia (CU-SYS-04). | Al cambiar el estado de la incidencia a `resuelta`, el almacén actualiza su estado y la capa de incidencias activas del mapa la retira de inmediato. | `HU-053`, `HU-055` |
| **V4-06** | Persistencia y consulta de rutas frecuentes en caché LRU (CU-SYS-05). | Las rutas calculadas se guardan en la caché local del dispositivo, permitiendo su consulta instantánea sin necesidad de nueva petición a la red. | `HU-029`, `HU-060`, `HU-061` |
| **V4-07** | Recuperación ante pérdida forzada de conectividad (REC-01). | Ante un corte de red durante la navegación, el sistema clasifica el error como `OFFLINE`, informa al usuario con una acción clara y recupera la ruta desde la caché local. | `HU-094` (Criterios 1, 2 y 4) |
| **V4-08** | Recuperación con retroceso exponencial ante latencia de API (REC-02). | Peticiones que sufren demoras o fallos transitorios se reintentan automáticamente hasta 3 veces con intervalos crecientes antes de desistir. | `HU-094` (Criterio 3) |
| **V4-09** | Preservación de formularios ante fallo permanente de servidor (REC-02). | Si la API no responde tras agotar reintentos, el estado del formulario se preserva intacto para que el usuario no pierda los datos introducidos. | `HU-094` (Criterio 4) |
| **V4-10** | Degradación elegante ante indisponibilidad del transporte EMT (REC-03). | Si la red externa de la EMT sufre una caída, la aplicación no se bloquea y garantiza la ruta a pie calculada localmente. | `HU-094` (Resiliencia) |
| **V4-11** | Autocuración ante corrupción del almacenamiento local (REC-04). | Cargas con cadenas JSON sintácticamente corruptas en la memoria del dispositivo se recuperan sin excepciones no controladas, reseteando a un estado seguro. | `HU-094` (Robustez) |
| **V4-12** | Protección contra inyección SQL/NoSQL en coordenadas (SEC-01). | Peticiones con cadenas alfanuméricas maliciosas, operadores de consulta o tipos no numéricos en `POST /routes/calculate` son rechazadas con HTTP 400. | `HU-090`, `HU-091` / Pruebas de Seguridad |
| **V4-13** | Neutralización de ataques XSS y HTML en reportes de incidencias (SEC-02). | Cargas con etiquetas `<script>`, manejadores de eventos (`onerror`, `onload`) o esquemas `javascript:` son interceptadas y rechazadas por el validador de contrato. | `HU-090`, `HU-091` / Pruebas de Seguridad |
| **V4-14** | Enmascaramiento estricto de secretos y trazas en respuestas y logs (SEC-03). | Las respuestas de error de la API y los registros de depuración ocultan contraseñas, claves y tokens de autorización, cumpliendo con RFC 7807. | `HU-094` (Criterio 5) |
| **V4-15** | Integridad y cobertura total de la Matriz de Trazabilidad (RTM). | Se comprueba formalmente que las 68 historias de usuario cuentan con pruebas asociadas, identificadores unívocos y calidad en estado `PASSED`. | `HU-097` / Matriz de Trazabilidad |

---

## 3. Umbrales de Aceptación (Quality Gates)

| Métrica / Control | Umbral Exigido | Resultado Obtenido en Sprint 4 | Estado |
| :--- | :--- | :--- | :---: |
| **Cobertura de sentencias (Statements)** | $\ge 90\,\%$ | **$98,06\,\%$** | ✅ Superado |
| **Cobertura de ramas (Branches)** | $\ge 85\,\%$ | **$95,18\,\%$** | ✅ Superado |
| **Cobertura de funciones (Functions)** | $\ge 90\,\%$ | **$98,31\,\%$** | ✅ Superado |
| **Cobertura de líneas (Lines)** | $\ge 90\,\%$ | **$98,14\,\%$** | ✅ Superado |
| **Tasa de éxito de pruebas automáticas** | $100\,\%$ | **$100\,\%$** (250 tests pasados, 0 fallos) | ✅ Superado |
| **Advertencias de linter (ESLint)** | $0$ advertencias | **$0$ advertencias** (`--max-warnings=0`) | ✅ Superado |
| **Cobertura de trazabilidad de requisitos** | $100\,\%$ | **$100\,\%$** (68 de 68 historias trazadas) | ✅ Superado |
| **Protección de secretos y credenciales** | Cero fugas | **$100\,\%$ sanitizado** en logs y respuestas RFC 7807 | ✅ Superado |
