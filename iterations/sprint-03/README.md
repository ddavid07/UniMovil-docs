# Sprint 3 — Multimodalidad EMT y Gestión de Incidencias en Campus

## 1. Estado y Contexto

* **Estado:** Planificado / Siguiente iteración de aceleración.
* **Objetivo principal:** Integrar el transporte público interno del campus (líneas de autobús G y F de la EMT) con cálculo comparativo de tiempos respecto a la caminata, e implementar el sistema de reporte y consulta de incidencias y obras en viales de Moncloa.
* **Marco metodológico:** Scrum puro y Gestión Proactiva del Riesgo (Barry Boehm RSGR).
* **Marco de pruebas:** Pruebas Orientadas a Objetos y TDD según el Tema 3 (profesores Antonio Navarro y Gonzalo Méndez).

---

## 2. Sprint Goal

> Como estudiante que se desplaza por Ciudad Universitaria, quiero consultar las líneas y paradas de los autobuses universitarios de la EMT (Líneas G y F) para comparar si me compensa caminar o tomar el autobús, y poder reportar y visualizar avisos de obras o incidencias en los caminos del campus, contando con una aplicación verificada y contrastada mediante pruebas de integración y caja negra.

---

## 3. Alcance y Elementos del Sprint Backlog

| Historia / Tarea | Puntos (SP) | Resultado Esperado | Criterios de Aceptación Verificables |
| :--- | :---: | :--- | :--- |
| **HU-022** — Consultar rutas con diferentes medios | 8 | Comparador multimodal en la tarjeta de ruta. | Muestra conjuntamente el tiempo a pie y el tiempo en autobús; resalta la opción más rápida según la distancia. |
| **HU-026** — Consultar una línea de autobús | 5 | Catálogo y trazado de las líneas G y F de la EMT. | Visualiza el recorrido oficial de las líneas universitarias y el sentido de circulación (Moncloa - Paraninfo). |
| **HU-027** — Consultar una parada de autobús | 3 | Marcadores de paradas EMT en el mapa con información. | Al pulsar una parada, muestra su denominación oficial, líneas que paran en ella y frecuencia estimada. |
| **HU-050** — Comunicar una incidencia | 5 | Formulario en la app móvil para reportar obstáculos. | Permite seleccionar el tipo de incidencia (obra, desvío, rampa averiada, acera cortada), geolocalizarla y enviar una descripción breve. |
| **HU-053** — Consultar incidencias públicas | 5 | Marcadores de aviso de obras y cortes en el mapa. | Señaliza en el mapa los viales cortados para que el estudiante evite caminos intransitables. |

---

## 4. Reparto Detallado de Responsabilidades (5 Integrantes)

Para mantener la autonomía y el avance simétrico de los cinco miembros del equipo:

### 👤 1. Naoufal Kebli (`@Naoufal33`)

* **Rol Scrum:** Developer — Frontend Móvil & Componentes Multimodales.
* **Historias asignadas:** `HU-022` (Comparativa multimodal), `HU-026` (Visualización de líneas en mapa).
* **Entregables técnicos:**
  1. Componente de tarjeta comparativa (`MultimodalComparisonCard.tsx`): selector de pestañas *"🚶 A pie (14 min)"* vs. *"🚌 Bus G (6 min)"*.
  2. Capas de renderizado de las líneas de autobús sobre el mapa de MapLibre con los colores oficiales de la EMT (azul EMT).
  3. Integración fluida entre la pantalla de rutas y el selector de medios de transporte.
* **Módulos / Archivos principales:** `apps/mobile/src/features/transit/`, `apps/mobile/src/features/routing/components/`.

---

### 👤 2. Daniel David (`@ddavid07`)

* **Rol Scrum:** Developer / Arquitecto — Backend NestJS y Datos de Transporte EMT.
* **Historias asignadas:** Soporte API a `HU-026`, `HU-027`, `HU-072` (Gestión de transporte y paradas).
* **Entregables técnicos:**
  1. Definición formal de contratos TypeScript en `@unimovil/contracts` (`TransitLine`, `TransitStop`, `MultimodalRouteOption`).
  2. Catálogo estructurado de las paradas oficiales de la EMT en Moncloa (Paraninfo, Metro Ciudad Universitaria, Filosofía, Medicina).
  3. Módulo de transporte en NestJS (`apps/api/src/transit/`): endpoints `GET /transit/lines` y `GET /transit/stops`.
* **Módulos / Archivos principales:** `packages/contracts/src/transit.ts`, `apps/api/src/transit/`.

---

### 👤 3. Pablo Palacios (`@pablopr06`)

* **Rol Scrum:** Developer — Módulo Móvil de Incidencias y Avisos.
* **Historias asignadas:** `HU-050` (Comunicar incidencia), `HU-051` (Evidencias de incidencia), `HU-053` (Consultar incidencias).
* **Entregables técnicos:**
  1. Formulario interactivo en la app móvil (`ReportIncidentScreen.tsx`): selector de tipo de problema, selector de ubicación en mapa y campo de observaciones.
  2. Capa cartográfica de incidencias en el mapa: marcadores de advertencia en color naranja con ficha informativa de obras activas.
  3. Validación de campos obligatorios para evitar reportes vacíos o mal formados.
* **Módulos / Archivos principales:** `apps/mobile/src/features/incidents/`, `packages/contracts/src/incidents.ts`.

---

### 👤 4. Pedro Cespón (`@pcespon`)

* **Rol Scrum:** QA Lead / Developer — Pruebas de Integración y Validación de Caja Negra (Tema 3).
* **Historias asignadas:** `HU-094` (Manejo de errores de transporte), verificación transversal del Sprint 3.
* **Entregables técnicos (alineados con el Tema 3 de teoría):**
  1. **Pruebas de Caja Negra (Particiones Equivalentes):** Verificación de las entradas de incidencias (reportes válidos, textos con caracteres especiales, coordenadas fuera de límites de la universidad).
  2. **Pruebas de Integración Basadas en Hilos:** Validación de la secuencia completa: reporte de incidencia en móvil $\rightarrow$ validación de contrato $\rightarrow$ persistencia temporal $\rightarrow$ refresco en la capa cartográfica.
  3. **Pruebas de Regresión:** Verificación de que la incorporación de las líneas EMT no degrade el rendimiento de renderizado del mapa ni el cálculo de rutas peatonales.
* **Módulos / Archivos principales:** `apps/mobile/src/features/transit/__tests__/`, `apps/mobile/src/features/incidents/__tests__/`.

---

### 👤 5. Charlie Fox / Carlos (`@yoespain`)

* **Rol Scrum:** Scrum Master & Developer — Panel Web Admin e Incidencias en `apps/admin`.
* **Historias asignadas:** `HU-054` (Gestionar incidencias), `HU-055` (Actualizar estado de incidencia).
* **Entregables técnicos:**
  1. Vista básica en el portal web de administración (`apps/admin`) en React + Vite para visualizar la tabla de incidencias enviadas por los estudiantes.
  2. Botón de moderación para que el gestor pueda marcar una obra como *"En curso"* o *"Resuelta"*.
  3. Redacción del acta de planificación en `meetings/sprint-03-planificacion-y-reparto.md` y actualización del *Burndown Chart*.
* **Módulos / Archivos principales:** `apps/admin/src/features/incidents/`, `UniMovil-docs/meetings/`.

---

## 5. Estrategia de Pruebas Orientadas a Objetos (Tema 3)

* **Pruebas de Unidad:** Clases `TransitService`, `IncidentValidator` y `ScheduleEstimator`.
* **Pruebas de Integración basadas en usos:** Se comprueban primero las clases independientes (`GeoPoint`, `Contracts`) y a continuación las clases dependientes por capas (`IncidentController` $\rightarrow$ `IncidentService`).
* **Pruebas de Regresión en CI:** Ejecución automática de todos los tests de Sprint 1, Sprint 2 y Sprint 3 en GitHub Actions sin permitir regresiones.

---

## 6. Definition of Done (DoD) del Sprint 3

1. Las líneas G y F se muestran correctamente sobre el mapa con sus paradas oficiales.
2. El formulario de incidencias permite enviar y reflejar un corte de paso en el mapa.
3. Se ejecutan con éxito las pruebas automáticas con Vitest y Jest en el monorepo.
4. Código formateado con Prettier y sin advertencias de ESLint ni errores de TypeScript.
5. Pull Request revisada y aprobada por los Codeowners.
