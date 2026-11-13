# Sprint 2 y Plan de Cierre — Motor de Rutas, Accesibilidad PMR, Multimodalidad y Pruebas OO

## 1. Estado y Contexto

* **Estado:** En curso (Planificación acordada para aceleración del proyecto).
* **Horizonte temporal:** 3 semanas para alcanzar la versión de entrega final del proyecto (cierre de Sprint 2 y consolidación en Sprint 3).
* **Marco metodológico:** Scrum puro y Gestión Proactiva de Riesgos (Barry Boehm RSGR).
* **Marco de pruebas:** Pruebas Orientadas a Objetos y TDD según las directrices teóricas del Tema 3 (profesores Antonio Navarro y Gonzalo Méndez).

---

## 2. Sprint Goal

> Como estudiante o visitante del campus de Moncloa, quiero calcular rutas peatonales entre facultades pudiendo activar filtros estrictos de accesibilidad para personas con movilidad reducida (PMR) y comparar alternativas con el autobús universitario (Líneas G y F de la EMT), disponiendo de una aplicación fiable y verificada mediante una suite rigurosa de pruebas automáticas.

---

## 3. Calendario de 3 Semanas hacia la Entrega Final

```text
┌─────────────────────────────────────────────────────────────────────────────────┐
│ SEMANA 1: Núcleo de Enrutamiento Peatonal y Suite de Pruebas TDD Inicial        │
│ • Integrar la PR #23 en main para desbloquear el mapa base.                     │
│ • Modelar el grafo de viales del campus en backend y contratos de rutas.        │
│ • Implementar pantalla de selección Origen/Destino en app móvil.                │
│ • Desplegar primeras pruebas unitarias (Vitest/Jest) con cobertura de ramas.   │
├─────────────────────────────────────────────────────────────────────────────────┤
│ SEMANA 2: Accesibilidad PMR, Integración EMT e Incidencias                      │
│ • Algoritmo de rutas sin barreras arquitectónicas (evitar tramos con escaleras).│
│ • Paradas y tiempos estimados de paso de autobuses EMT (Líneas G y F).          │
│ • Pruebas de caja negra: particiones equivalentes y análisis de valores límite. │
│ • Formulario básico de notificación de incidencias (obras y cortes de paso).    │
├─────────────────────────────────────────────────────────────────────────────────┤
│ SEMANA 3: Panel de Administración, Pruebas de Sistema y Cierre Académico        │
│ • Panel web administrativo (React + Vite) para supervisión de datos y avisos.   │
│ • Pruebas de integración basadas en hilos y pruebas de validación de sistema.   │
│ • Cierre de DoD: cobertura de código, auditoría de seguridad y dependencias.    │
│ • Actualización final de la memoria del proyecto y guion de la defensa oral.   │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## 4. Reparto Detallado de Responsabilidades (5 Integrantes)

Para garantizar la autonomía, evitar colisiones en Git y maximizar el rendimiento del equipo, las responsabilidades se distribuyen formalmente entre los cinco miembros:

### 👤 1. Naoufal Kebli (`@Naoufal33`)

* **Rol Scrum:** Developer — Frontend Móvil & Experiencia de Usuario.
* **Historias asignadas:**
  * [`HU-020 — Introducir origen y destino`](../../requirements/user-stories/03-rutas-y-transporte.md)
  * [`HU-021 — Consultar una ruta a pie`](../../requirements/user-stories/03-rutas-y-transporte.md)
  * [`HU-023 — Consultar indicaciones paso a paso`](../../requirements/user-stories/03-rutas-y-transporte.md)
* **Entregables técnicos:**
  1. Selector reactivo de origen y destino en la app móvil (selección táctil en mapa o mediante buscador con autocompletado).
  2. Renderizado del trazado de la ruta sobre el mapa (`CampusMapView` / `CampusMap`) con polyline/capas GeoJSON.
  3. Tarjeta inferior flotante con la distancia en metros, tiempo estimado en minutos y lista plegable de indicaciones.
* **Módulos / Archivos principales:** `apps/mobile/src/features/campus/`, `apps/mobile/src/components/routing/`.

---

### 👤 2. Daniel David (`@ddavid07`)

* **Rol Scrum:** Developer & Arquitecto — Backend NestJS y Contratos.
* **Historias asignadas:**
  * Soporte backend a `HU-020` y `HU-021`.
  * [`HU-075 — Consultar el estado de los datos`](../../requirements/user-stories/07-administracion-y-datos.md)
* **Entregables técnicos:**
  1. Definición formal de contratos TypeScript en `@unimovil/contracts` (`RouteRequest`, `RouteResponse`, `RouteSegment`, `TransportMode`).
  2. Modelado del grafo de viales y sendas de Moncloa (coordenadas de cruces, distancias y transitabilidad).
  3. Implementación del servicio de rutas en NestJS (`routes.service.ts`) aplicando el algoritmo de Dijkstra/A* con pesos según distancia física.
  4. Endpoint REST `POST /routes/calculate` y endpoint de estado `GET /health`.
* **Módulos / Archivos principales:** `packages/contracts/src/routes.ts`, `apps/api/src/routes/`.

---

### 👤 3. Pablo Palacios (`@pablopr06`)

* **Rol Scrum:** Developer — Movilidad Especializada, Accesibilidad e Integración EMT.
* **Historias asignadas:**
  * [`HU-022 — Consultar rutas con diferentes medios`](../../requirements/user-stories/03-rutas-y-transporte.md)
  * [`HU-024 — Consultar una ruta accesible`](../../requirements/user-stories/03-rutas-y-transporte.md)
  * [`HU-026 — Consultar una línea de autobús`](../../requirements/user-stories/03-rutas-y-transporte.md)
  * [`HU-040 — Configurar preferencias de accesibilidad`](../../requirements/user-stories/04-accesibilidad-y-recursos.md)
* **Entregables técnicos:**
  1. Conmutador de "Ruta Accesible (PMR)": penalización o bloqueo en el grafo de aristas que contengan escaleras o desniveles no adaptados.
  2. Catálogo de paradas y trazados de las líneas universitarias de la EMT (Línea G: Moncloa - Ciudad Universitaria; Línea F: Cuatro Caminos - Ciudad Universitaria).
  3. Lógica comparativa multimodal: presentación conjunta de tiempo a pie vs. tiempo en autobús.
* **Módulos / Archivos principales:** `apps/mobile/src/features/accessibility/`, `apps/api/src/transit/`.

---

### 👤 4. Pedro Cespón (`@pcespon`)

* **Rol Scrum:** Developer & Responsable de Calidad (QA) — Batería de Pruebas y TDD.
* **Historias asignadas:**
  * [`HU-094 — Gestionar errores y falta de conexión`](../../requirements/user-stories/08-seguridad-privacidad-y-calidad.md)
  * [`HU-095 — Utilizar una interfaz accesible`](../../requirements/user-stories/08-seguridad-privacidad-y-calidad.md)
  * Verificación transversal de la suite de pruebas.
* **Entregables técnicos (alineados con el Tema 3 de teoría):**
  1. **Pruebas de Caja Blanca:** Cálculo de caminos básicos y complejidad ciclomática de McCabe sobre los algoritmos de enrutamiento y normalización de texto; garantía de cobertura de ramas y condiciones.
  2. **Pruebas de Caja Negra:** Definición formal de particiones de equivalencia (clases válidas e inválidas) y análisis de valores límite (coordenadas extremas, consultas vacías, entradas de más de 100 caracteres).
  3. **Adopción de TDD (Uncle Bob):** Aplicación de las 3 reglas de TDD (*Red-Green-Refactor*) para los nuevos servicios.
  4. **Automatización:** Ejecución de Vitest y Jest en GitHub Actions (`ci.yml`), verificando que los tests sean Automáticos, Completos, Repetibles, Independientes y Profesionales.
* **Módulos / Archivos principales:** `packages/testing/`, `apps/mobile/__tests__/`, `apps/api/src/**/*.spec.ts`.

---

### 👤 5. Charlie Fox / Carlos (`@yoespain`)

* **Rol Scrum:** Scrum Master & Developer — Panel Web Admin e Incidencias.
* **Historias asignadas:**
  * [`HU-050 — Comunicar una incidencia`](../../requirements/user-stories/05-incidencias-y-comunicaciones.md)
  * [`HU-057 — Publicar un aviso`](../../requirements/user-stories/05-incidencias-y-comunicaciones.md)
  * [`HU-070 — Gestionar edificios y lugares`](../../requirements/user-stories/07-administracion-y-datos.md)
* **Entregables técnicos:**
  1. Portal web en `apps/admin` (React + Vite) con interfaz para gestores del campus: visualización de incidencias reportadas (obras, cortes de paso, ascensores averiados).
  2. Formulario de reporte de incidencias desde la aplicación móvil.
  3. Gestión del proceso Scrum: seguimiento diario, elaboración de los gráficos Burndown de cada Sprint, actas de planificación y retrospectiva.
  4. Sincronización continua de la memoria del proyecto en [`UniMovil-docs`](../../memory/memoria-del-proyecto.md).
* **Módulos / Archivos principales:** `apps/admin/src/`, `apps/mobile/src/features/incidents/`, `UniMovil-docs/meetings/`.

---

## 5. Estrategia de Pruebas Orientadas a Objetos (Tema 3)

De acuerdo con el documento `03-Pruebas orientadas a objetos.pdf` (profesores Antonio Navarro y Gonzalo Méndez), la verificación del software no se deja al azar ni se limita a pruebas manuales, sino que se organiza por niveles rigurosos:

### 5.1. Pruebas Unitarias (Clases y Operaciones)

* Unidad mínima de prueba: la clase.
* Se probarán para cada operación crítica: interfaz, estructuras de datos locales, condiciones límite, caminos independientes y manejo de excepciones (`assertThrows` / `rejects`).
* **Estructura paralela:** directorios de test replicando fielmente la estructura de paquetes de código de producción.

### 5.2. Pruebas de Integración

* **Pruebas basadas en hilos (encadenamiento de mensajes):** Verificación de las secuencias de interacción entre cliente móvil, contratos de datos y controladores de la API REST.
* **Pruebas de regresión:** Ejecución automatizada de la suite ante cada Pull Request para garantizar que la incorporación de nuevas funciones no introduce efectos colaterales indeseados.

### 5.3. Pruebas de Caja Blanca y Caja Negra

* **Caja Blanca (Estructural):** Método del camino básico a partir del grafo de flujo de los métodos de búsqueda y enrutamiento, asegurando que cada sentencia y decisión lógica se ejercite al menos una vez.
* **Caja Negra (Funcional):** Partición equivalente de entradas (tipos de vías transitables vs. intransitables) y análisis de valores frontera en coordenadas geográficas del campus (dentro del perímetro de Moncloa, en el límite exacto y fuera de rango).

### 5.4. Las Tres Reglas de TDD (Uncle Bob)

1. No se permite escribir código de producción a menos que sea para hacer pasar una prueba unitaria que falla.
2. No se permite escribir más de una prueba unitaria de lo que sea suficiente para fallar (los errores de compilación cuentan como fallos).
3. No se permite escribir más código de producción del necesario para hacer pasar la prueba unitaria que fallaba.

---

## 6. Definition of Done (DoD) Específica

Para considerar un elemento del Sprint Backlog formalmente "Terminado", debe satisfacer:

1. **Código:** Escrito en TypeScript bajo configuración estricta, sin errores de tipado (`npm run typecheck`) ni avisos de linter (`npm run lint`).
2. **Pruebas:** Pruebas unitarias asociadas creadas con Vitest o Jest, pasando en verde de forma reproducible e independiente.
3. **Revisión por pares:** Pull Request en GitHub con al menos una aprobación formal de otro integrante del equipo.
4. **Integración:** Integrado en la rama `main` tras validar que el pipeline de GitHub Actions finaliza con éxito.
5. **Documentación:** Contratos reflejados en `@unimovil/contracts` y cambios registrados en `UniMovil-docs`.
