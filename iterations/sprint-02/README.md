# Sprint 2 — Motor de Rutas Peatonales y Accesibilidad PMR

## 1. Estado y Contexto

* **Estado:** Planificado / En preparación para inicio tras aprobación de la PR #23.
* **Objetivo principal:** Diseñar y desarrollar el motor de cálculo de rutas peatonales entre facultades del campus de Moncloa con filtro estricto de accesibilidad para personas con movilidad reducida (PMR).
* **Marco metodológico:** Scrum puro y Gestión Proactiva del Riesgo (Barry Boehm RSGR).
* **Marco de pruebas:** Pruebas Orientadas a Objetos y TDD según el Tema 3 (profesores Antonio Navarro y Gonzalo Méndez).

---

## 2. Sprint Goal

> Como estudiante o visitante del campus de Moncloa, quiero seleccionar un origen y un destino para calcular la ruta a pie más eficiente, disponiendo de un conmutador de accesibilidad PMR que garantice un itinerario sin escaleras ni barreras arquitectónicas, respaldado por una batería rigurosa de pruebas automáticas con Vitest y Jest.

---

## 3. Alcance y Elementos del Sprint Backlog

| Historia / Tarea | Puntos (SP) | Resultado Esperado | Criterios de Aceptación Verificables |
| :--- | :---: | :--- | :--- |
| **HU-020** — Introducir origen y destino | 5 | Selector dual táctil y predictivo en la app móvil. | Permite marcar dos puntos en el mapa o elegirlos desde el buscador; valida que origen y destino no sean idénticos; muestra pines distintivos de salida y llegada. |
| **HU-021** — Consultar una ruta a pie | 8 | Motor de rutas que devuelve el camino mínimo en el campus. | Calcula el itinerario óptimo entre edificios; calcula la distancia exacta en metros y el tiempo estimado en minutos a pie (velocidad media 4,5 km/h). |
| **HU-023** — Consultar indicaciones paso a paso | 5 | Ficha desplegable con el desglose del recorrido. | Muestra la secuencia de tramos (ej. *"Avanza 120 m por Av. Complutense y gira a la derecha hacia Medicina"*). |
| **HU-024 / HU-040** — Ruta accesible PMR | 8 | Filtro estricto que elimina barreras arquitectónicas. | Al activar el conmutador PMR, el algoritmo penaliza o bloquea aristas con escaleras o desniveles no adaptados, garantizando acceso por rampas homologadas. |

---

## 4. Reparto Detallado de Responsabilidades (5 Integrantes)

Para asegurar la autonomía, evitar conflictos de ramas en Git y estructurar el trabajo en equipo:

### 👤 1. Naoufal Kebli (`@Naoufal33`)

* **Rol Scrum:** Developer — Frontend Móvil & Experiencia de Usuario.
* **Historias asignadas:** `HU-020` (Origen y destino), `HU-021` (Ruta a pie en móvil), `HU-023` (Indicaciones paso a paso).
* **Entregables técnicos:**
  1. Componente de selección de origen y destino (`RouteSelector.tsx`) integrado en la cabecera de la app móvil.
  2. Dibujo de la línea de ruta (*polyline*) sobre el visor cartográfico (`CampusMap.tsx`) mediante capas GeoJSON.
  3. Ficha inferior flotante (`RouteSheet.tsx`) con distancia, tiempo y lista desplegable de giros y pasos.
* **Módulos / Archivos principales:** `apps/mobile/src/features/routing/`, `apps/mobile/src/features/campus/components/`.

---

### 👤 2. Daniel David (`@ddavid07`)

* **Rol Scrum:** Developer / Arquitecto — Backend NestJS y Contratos Compartidos.
* **Historias asignadas:** Soporte API a `HU-020` y `HU-021`, `HU-075` (Estado de los datos).
* **Entregables técnicos:**
  1. Definición formal de contratos TypeScript en `@unimovil/contracts` (`RouteRequest`, `RouteResponse`, `RouteSegment`, `Coordinates`).
  2. Modelado del grafo de viales y sendas peatonales del campus de Moncloa (coordenadas de cruces y distancias euclídeas reales).
  3. Implementación del algoritmo de Dijkstra/A* en NestJS (`routes.service.ts`) para resolver el camino más corto.
  4. Endpoints REST `POST /routes/calculate` y `GET /routes/health`.
* **Módulos / Archivos principales:** `packages/contracts/src/routes.ts`, `apps/api/src/routes/`.

---

### 👤 3. Pablo Palacios (`@pablopr06`)

* **Rol Scrum:** Developer — Lógica de Accesibilidad PMR.
* **Historias asignadas:** `HU-024` (Ruta accesible), `HU-040` (Preferencias de accesibilidad), `HU-041` (Accesos adaptados).
* **Entregables técnicos:**
  1. Etiquetado de accesibilidad en el grafo de caminos: identificación de tramos con escaleras (ej. escalinatas de Medicina u Odontología) y tramos con rampas.
  2. Lógica de exclusión de barreras en el algoritmo de enrutamiento cuando el parámetro `accessibleOnly: true` esté activo.
  3. Conmutador accesible accesible en la interfaz móvil (`AccessibilityToggle.tsx`) con avisos auditivos y lectores de pantalla.
* **Módulos / Archivos principales:** `apps/mobile/src/features/accessibility/`, `packages/contracts/src/routes.ts`.

---

### 👤 4. Pedro Cespón (`@pcespon`)

* **Rol Scrum:** QA Lead / Developer — Batería de Pruebas Unitarias y TDD (Tema 3).
* **Historias asignadas:** `HU-094` (Manejo de errores), verificación transversal de calidad del Sprint 2.
* **Entregables técnicos (alineados con el Tema 3 de teoría):**
  1. **Pruebas de Caja Blanca:** Cálculo de caminos básicos y complejidad ciclomática de McCabe sobre el algoritmo de enrutamiento; garantía de cobertura de todas las decisiones lógicas y ramas.
  2. **Pruebas de Caja Negra:** Partición en clases de equivalencia (rutas directas, rutas con transbordo peatonal, rutas imposibles) y análisis de valores límite (origen y destino idénticos, coordenadas en el borde del campus).
  3. **TDD (The Three Rules of Uncle Bob):** Conducción del desarrollo del motor de rutas siguiendo el ciclo *Red $\rightarrow$ Green $\rightarrow$ Refactor*.
* **Módulos / Archivos principales:** `apps/mobile/src/features/routing/__tests__/`, `apps/api/src/routes/*.spec.ts`.

---

### 👤 5. Charlie Fox / Carlos (`@yoespain`)

* **Rol Scrum:** Scrum Master & Developer — Coordinación y Seguimiento.
* **Historias asignadas:** `HU-097` (Trazabilidad de cambios), gestión del Sprint Backlog.
* **Entregables técnicos:**
  1. Facilitar los eventos de Scrum: Sprint Planning, Daily Scrum asíncrono y preparación de la Sprint Review.
  2. Mantenimiento del *Product Backlog* y cálculo de la velocidad del equipo en Story Points.
  3. Redacción del acta de planificación en `meetings/sprint-02-reparto-de-trabajo.md` y actualización de la memoria técnica en `UniMovil-docs`.
* **Módulos / Archivos principales:** `UniMovil-docs/meetings/`, `UniMovil-docs/memory/memoria-del-proyecto.md`.

---

## 5. Estrategia de Pruebas Orientadas a Objetos (Tema 3)

Conforme a las diapositivas de la asignatura (profesores Antonio Navarro y Gonzalo Méndez):

* **Pruebas de Unidad:** Aislamiento de las clases `RouteService`, `GraphBuilder` y `RoutePresenter`.
* **Pruebas de Integración basadas en hilos:** Secuencia completa: selección de coordenadas en móvil $\rightarrow$ serialización contra `@unimovil/contracts` $\rightarrow$ cálculo en servicio $\rightarrow$ respuesta y renderizado de la polilínea.
* **Pruebas de Regresión:** Verificación automática en el pipeline de GitHub Actions (`ci.yml`) para garantizar que la incorporación de rutas no altere la búsqueda ni el catálogo de lugares existente.

---

## 6. Definition of Done (DoD) del Sprint 2

El incremento se considerará formalmente terminado si:

1. El cálculo de ruta peatonal y el filtro PMR funcionan en emulador Android nativo.
2. Todo el código TypeScript compila sin errores (`npm run typecheck`) y sin avisos de ESLint (`npm run lint`).
3. La cobertura de pruebas supera el 80% de líneas y 70% de ramas en los nuevos módulos.
4. Los contratos están documentados y publicados en `@unimovil/contracts`.
5. Se ha realizado Pull Request con al menos una aprobación formal de otro integrante.
