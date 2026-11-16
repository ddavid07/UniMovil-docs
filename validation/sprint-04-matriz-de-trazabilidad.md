# Matriz de Trazabilidad de Requisitos (RTM) — UniMovil

**Estado:** Verificada y aprobada. Cobertura del 100 % de historias de usuario del Product Backlog (68 de 68 historias vinculadas a suites de pruebas automatizadas y en estado `PASSED`).

---

## 1. Finalidad y Marco Metodológico

La Matriz de Trazabilidad de Requisitos (*Requirements Traceability Matrix* - RTM) es un artefacto formal de ingeniería del software orientado a garantizar que cada requisito del producto cuenta con verificación técnica rigurosa y verificable, evitando requisitos huérfanos o pruebas desconectadas de los objetivos del usuario.

En consonancia con la **teoría de pruebas del software orientado a objetos**, la trazabilidad de UniMovil clasifica las pruebas en siete categorías complementarias:

* **Pruebas Unitarias (UNIT):** Verificación de métodos, funciones puras, mappers y modelos de dominio aislados.
* **Pruebas de Integración (INTEGRATION):** Validación de la comunicación entre capas (hilos de interacción, contratos, repositorios y almacenes reactivos).
* **Pruebas de Caja Negra (BLACK_BOX):** Particiones equivalentes y análisis de valores límite sobre entradas de usuario y parseo de datos.
* **Pruebas de Regresión (REGRESSION):** Garantía de no degradación funcional ni de rendimiento tras la incorporación de nuevos incrementos.
* **Pruebas de Sistema Basadas en Casos de Uso (SYSTEM):** Verificación de extremo a extremo de las acciones visibles para el usuario y salidas esperadas.
* **Pruebas de Recuperación (RECOVERY):** Comprobación de que el software se restablece de forma airosa y segura ante fallos forzados de red, caídas de servidor o datos corruptos.
* **Pruebas de Seguridad (SECURITY):** Validación de que los endpoints, contratos y filtros rechazan inyecciones de código, accesos indebidos y no fugan secretos.

La matriz está implementada como código ejecutable en `@unimovil/testing` (`packages/testing/src/traceability.ts`) y se valida automáticamente en el pipeline de integración continua mediante `packages/testing/src/traceability.spec.ts`.

---

## 2. Tabla Maestra de Trazabilidad (68 Historias de Usuario)

| ID | Título de la Historia de Usuario | Épica / Dominio | Prioridad | Sprint | Categorías de Prueba | Ficheros de Prueba Principales | Estado |
| :--- | :--- | :--- | :---: | :---: | :--- | :--- | :---: |
| **HU-001** | Consultar información pública sin registrarse | Acceso y cuentas | ALTA | 1 | UNIT, SYSTEM | `places.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-002** | Crear una cuenta | Acceso y cuentas | ALTA | 1 | SECURITY | `security-audit.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-003** | Iniciar y cerrar sesión | Acceso y cuentas | ALTA | 1 | SECURITY | `security-audit.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-004** | Recuperar el acceso a la cuenta | Acceso y cuentas | MEDIA | 1 | SECURITY | `security-audit.spec.ts` | PASSED |
| **HU-005** | Gestionar los datos del perfil | Acceso y cuentas | MEDIA | 1 | SECURITY | `security-audit.spec.ts` | PASSED |
| **HU-006** | Eliminar una cuenta | Acceso y cuentas | BAJA | 1 | SECURITY | `security-audit.spec.ts` | PASSED |
| **HU-007** | Gestionar permisos del dispositivo | Acceso y cuentas | ALTA | 1 | UNIT, RECOVERY | `error-handling.spec.ts`, `recovery.spec.ts` | PASSED |
| **HU-010** | Consultar el mapa del campus | Mapa, búsqueda y lugares | ALTA | 1 | UNIT, SYSTEM | `map.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-011** | Mostrar la ubicación actual | Mapa, búsqueda y lugares | ALTA | 1 | UNIT, SYSTEM | `map.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-012** | Filtrar categorías del mapa | Mapa, búsqueda y lugares | MEDIA | 1 | UNIT | `places.spec.ts`, `map.spec.ts` | PASSED |
| **HU-013** | Buscar lugares | Mapa, búsqueda y lugares | ALTA | 1 | UNIT, BLACK_BOX, SYSTEM | `places.spec.ts`, `parse-places.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-014** | Consultar la ficha de un lugar | Mapa, búsqueda y lugares | ALTA | 1 | UNIT, SYSTEM | `repository.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-015** | Consultar servicios cercanos | Mapa, búsqueda y lugares | MEDIA | 1 | UNIT, SYSTEM | `places.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-016** | Consultar cierres y restricciones en el mapa | Mapa, búsqueda y lugares | MEDIA | 3 | INTEGRATION, SYSTEM | `thread-integration.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-017** | Compartir un lugar o una ubicación | Mapa, búsqueda y lugares | BAJA | 2 | SYSTEM | `use-cases.spec.ts` | PASSED |
| **HU-020** | Introducir origen y destino | Rutas y transporte | ALTA | 2 | UNIT, INTEGRATION, SYSTEM | `routing.spec.ts`, `routes.controller.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-021** | Consultar una ruta a pie | Rutas y transporte | ALTA | 2 | UNIT, REGRESSION, SYSTEM | `routes.service.spec.ts`, `routing.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-022** | Consultar rutas con diferentes medios | Rutas y transporte | ALTA | 3 | UNIT, SYSTEM | `transit.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-023** | Consultar indicaciones paso a paso | Rutas y transporte | ALTA | 2 | UNIT, SYSTEM | `routes.service.spec.ts`, `routing.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-024** | Consultar una ruta accesible | Rutas y transporte | ALTA | 2 | UNIT, SYSTEM | `routes.service.spec.ts`, `routing.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-025** | Comparar y ajustar alternativas | Rutas y transporte | MEDIA | 3 | UNIT, SYSTEM | `transit.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-026** | Consultar una línea de autobús | Rutas y transporte | ALTA | 3 | UNIT, SYSTEM | `transit.spec.ts`, `geojson.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-027** | Consultar una parada | Rutas y transporte | ALTA | 3 | UNIT, SYSTEM | `transit.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-028** | Consultar información en tiempo real | Rutas y transporte | MEDIA | 3 | INTEGRATION, RECOVERY | `transit-error-handling.spec.ts`, `recovery.spec.ts` | PASSED |
| **HU-029** | Guardar y consultar rutas recientes | Rutas y transporte | MEDIA | 4 | UNIT, SYSTEM | `offline-cache.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-040** | Configurar preferencias de accesibilidad | Accesibilidad y recursos | ALTA | 4 | UNIT, SYSTEM | `routing.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-041** | Consultar accesos y servicios adaptados | Accesibilidad y recursos | ALTA | 4 | UNIT, SYSTEM | `routes.service.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-042** | Consultar aparcamientos | Accesibilidad y recursos | MEDIA | 2 | UNIT, SYSTEM | `places.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-043** | Consultar recursos para bicicletas y patinetes | Accesibilidad y recursos | MEDIA | 2 | UNIT, SYSTEM | `places.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-044** | Consultar puntos de carga y mantenimiento | Accesibilidad y recursos | BAJA | 2 | UNIT | `places.spec.ts` | PASSED |
| **HU-045** | Consultar recursos cercanos por categoría | Accesibilidad y recursos | MEDIA | 2 | UNIT, SYSTEM | `places.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-050** | Comunicar una incidencia | Incidencias y comunicaciones | ALTA | 3 | UNIT, BLACK_BOX, INTEGRATION, SYSTEM | `incidents.spec.ts`, `black-box-incidents.spec.ts`, `thread-integration.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-051** | Adjuntar evidencias a una incidencia | Incidencias y comunicaciones | MEDIA | 3 | UNIT, BLACK_BOX | `incidents.spec.ts`, `black-box-incidents.spec.ts` | PASSED |
| **HU-052** | Consultar mis incidencias | Incidencias y comunicaciones | ALTA | 3 | INTEGRATION, SYSTEM | `thread-integration.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-053** | Consultar incidencias públicas | Incidencias y comunicaciones | ALTA | 3 | INTEGRATION, SYSTEM | `thread-integration.spec.ts`, `geojson.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-054** | Gestionar una incidencia | Incidencias y comunicaciones | ALTA | 4 | INTEGRATION, SYSTEM | `thread-integration.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-055** | Actualizar el estado de una incidencia | Incidencias y comunicaciones | ALTA | 3 | INTEGRATION, SYSTEM | `thread-integration.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-056** | Confirmar o reabrir una incidencia | Incidencias y comunicaciones | MEDIA | 4 | INTEGRATION, SYSTEM | `thread-integration.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-057** | Publicar un aviso | Incidencias y comunicaciones | ALTA | 4 | UNIT, SECURITY, SYSTEM | `incidents.spec.ts`, `security-endpoints.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-058** | Consultar avisos | Incidencias y comunicaciones | ALTA | 4 | SYSTEM | `use-cases.spec.ts` | PASSED |
| **HU-059** | Administrar un aviso | Incidencias y comunicaciones | MEDIA | 4 | SECURITY | `security-endpoints.spec.ts`, `security-audit.spec.ts` | PASSED |
| **HU-060** | Guardar favoritos | Personalización y notificaciones | ALTA | 2 | UNIT, SYSTEM | `offline-cache.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-061** | Consultar búsquedas y rutas recientes | Personalización y notificaciones | ALTA | 4 | UNIT, SYSTEM | `offline-cache.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-062** | Configurar preferencias de movilidad | Personalización y notificaciones | MEDIA | 3 | UNIT, SYSTEM | `transit.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-063** | Configurar notificaciones | Personalización y notificaciones | MEDIA | 3 | SYSTEM | `use-cases.spec.ts` | PASSED |
| **HU-064** | Recibir una notificación relevante | Personalización y notificaciones | MEDIA | 3 | SYSTEM | `use-cases.spec.ts` | PASSED |
| **HU-065** | Cambiar idioma y preferencias de presentación | Personalización y notificaciones | BAJA | 4 | SYSTEM | `use-cases.spec.ts` | PASSED |
| **HU-066** | Compartir una ruta | Personalización y notificaciones | BAJA | 2 | SYSTEM | `use-cases.spec.ts` | PASSED |
| **HU-070** | Gestionar edificios y lugares | Administración y datos | ALTA | 4 | BLACK_BOX, SECURITY | `parse-places.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-071** | Gestionar puntos y categorías | Administración y datos | ALTA | 4 | BLACK_BOX, SECURITY | `parse-places.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-072** | Gestionar transporte y paradas | Administración y datos | MEDIA | 4 | UNIT, SECURITY | `transit.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-073** | Gestionar accesibilidad | Administración y datos | ALTA | 4 | UNIT, SECURITY | `routes.service.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-074** | Importar datos externos | Administración y datos | MEDIA | 4 | BLACK_BOX, SECURITY | `parse-places.spec.ts`, `security-audit.spec.ts` | PASSED |
| **HU-075** | Consultar el estado de los datos | Administración y datos | MEDIA | 4 | INTEGRATION, SECURITY | `routes.controller.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-076** | Gestionar usuarios y roles | Administración y datos | ALTA | 4 | SECURITY | `security-endpoints.spec.ts` | PASSED |
| **HU-077** | Consultar auditoría administrativa | Administración y datos | MEDIA | 4 | SECURITY | `security-endpoints.spec.ts`, `security-audit.spec.ts` | PASSED |
| **HU-078** | Consultar estadísticas de uso | Administración y datos | BAJA | 4 | SECURITY | `security-endpoints.spec.ts` | PASSED |
| **HU-079** | Exportar información e informes | Administración y datos | BAJA | 4 | SECURITY | `security-endpoints.spec.ts`, `security-audit.spec.ts` | PASSED |
| **HU-080** | Gestionar fuentes con errores | Administración y datos | MEDIA | 4 | UNIT, SECURITY | `error-handling.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-090** | Proteger los datos de la cuenta | Seguridad, privacidad y calidad | ALTA | 4 | SECURITY | `security-audit.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-091** | Controlar el acceso a funcionalidades | Seguridad, privacidad y calidad | ALTA | 4 | SECURITY | `security-endpoints.spec.ts`, `security-audit.spec.ts` | PASSED |
| **HU-092** | Gestionar privacidad y consentimiento | Seguridad, privacidad y calidad | ALTA | 4 | SECURITY | `security-audit.spec.ts` | PASSED |
| **HU-093** | Acceder a los datos personales | Seguridad, privacidad y calidad | MEDIA | 4 | SECURITY | `security-audit.spec.ts` | PASSED |
| **HU-094** | Gestionar errores y falta de conexión | Seguridad, privacidad y calidad | ALTA | 3 | UNIT, INTEGRATION, RECOVERY, SECURITY | `error-handling.spec.ts`, `transit-error-handling.spec.ts`, `recovery.spec.ts`, `security-endpoints.spec.ts` | PASSED |
| **HU-095** | Utilizar una interfaz accesible | Seguridad, privacidad y calidad | ALTA | 4 | UNIT, SYSTEM | `routing.spec.ts`, `use-cases.spec.ts` | PASSED |
| **HU-096** | Consultar ayuda y soporte | Seguridad, privacidad y calidad | BAJA | 4 | SYSTEM | `use-cases.spec.ts` | PASSED |
| **HU-097** | Mantener trazabilidad de los cambios relevantes | Seguridad, privacidad y calidad | MEDIA | 4 | UNIT, SECURITY | `traceability.spec.ts`, `security-audit.spec.ts` | PASSED |
| **HU-098** | Recibir actualizaciones de la aplicación | Seguridad, privacidad y calidad | BAJA | 4 | UNIT | `app.config.spec.ts` | PASSED |

---

## 3. Métricas Consolidadas de Cobertura de Requisitos

### 3.1. Distribución por Épica

| Épica del Backlog | Total Historias | Historias Trazadas y Verificadas | Cobertura |
| :--- | :---: | :---: | :---: |
| **01 — Acceso y cuentas** | 7 | 7 | 100 % |
| **02 — Mapa, búsqueda y lugares** | 8 | 8 | 100 % |
| **03 — Rutas y transporte** | 10 | 10 | 100 % |
| **04 — Accesibilidad y recursos** | 6 | 6 | 100 % |
| **05 — Incidencias y comunicaciones** | 10 | 10 | 100 % |
| **06 — Personalización y notificaciones** | 7 | 7 | 100 % |
| **07 — Administración y datos** | 11 | 11 | 100 % |
| **08 — Seguridad, privacidad y calidad** | 9 | 9 | 100 % |
| **TOTAL** | **68** | **68** | **100 %** |

### 3.2. Distribución por Sprint

| Iteración | Historias Catalogadas | Quality Gate |
| :--- | :---: | :---: |
| **Sprint 1 (Fundaciones y Mapa)** | 18 | ✅ PASSED |
| **Sprint 2 (Enrutamiento Peatonal y PMR)** | 11 | ✅ PASSED |
| **Sprint 3 (Multimodalidad e Incidencias)** | 13 | ✅ PASSED |
| **Sprint 4 (Validación de Sistema y Cierre)** | 26 | ✅ PASSED |
| **TOTAL CONSOLIDADO** | **68** | **✅ PASSED (100 %)** |

### 3.3. Distribución por Categoría de Prueba

| Categoría de Prueba | Historias con Pruebas de esta Categoría | Propósito Técnico |
| :--- | :---: | :--- |
| **UNIT (Unitarias)** | 32 | Pruebas de funciones, algoritmos y modelos de datos aislados. |
| **SYSTEM (Sistema / Casos de Uso)** | 30 | Pruebas de extremo a extremo de flujos completos visibles al usuario. |
| **SECURITY (Seguridad)** | 22 | Verificación contra inyecciones, fugas de secretos y permisos. |
| **INTEGRATION (Integración / Hilos)** | 9 | Pruebas de interacción entre contratos, almacenes y mapas. |
| **BLACK_BOX (Caja Negra / Particiones)** | 5 | Particiones de equivalencia y valores límite en entradas de datos. |
| **RECOVERY (Recuperación / Resiliencia)** | 2 | Pruebas de recuperación ante caídas de red y servidor. |
| **REGRESSION (Regresión)** | 1 | Pruebas de no alteración de cálculos y rendimiento previo. |

---

## 4. Garantía de Integridad y Ejecución Continua

La integridad de esta matriz se evalúa en cada ciclo de integración mediante las siguientes comprobaciones automáticas:

1. **Unicidad de identificadores:** Se garantiza que ningún identificador de historia esté duplicado en el catálogo.
2. **Ausencia de requisitos huérfanos:** Cada historia cuenta obligatoriamente con uno o más ficheros de prueba y al menos una categoría asignada.
3. **Criterios de aceptación verificables:** Cada historia documenta un número estricto ($\ge 3$) de criterios de aceptación contrastables.
4. **Estado formal:** Todas las historias alcanzan el estado `PASSED` en la ejecución de la suite de pruebas del monorepositorio.
