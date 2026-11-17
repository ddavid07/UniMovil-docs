# Sprint 4 — Panel Web Admin, Validación Global del Sistema y Cierre Académico

## 1. Estado y Contexto

* **Estado:** En curso / Incremento móvil de resiliencia sin conexión (HU-094) y accesibilidad universal WCAG 2.1 AA (HU-095) completado y verificado.
* **Objetivo principal:** Integrar el portal web de administración (`apps/admin`) para gestión de avisos y edificios del campus, garantizar la robustez offline de la app móvil, ejecutar la batería de pruebas de sistema y validación (Tema 3) y culminar la memoria académica y el material de la defensa oral.
* **Marco metodológico:** Scrum puro y Gestión Proactiva del Riesgo (Barry Boehm RSGR).
* **Marco de pruebas:** Pruebas Orientadas a Objetos y Validación Integral según el Tema 3 (profesores Antonio Navarro y Gonzalo Méndez).
* **Entregas en GitHub:** Rama `feature/sprint-04-offline-accessibility` (Frontend móvil por Naoufal Kebli).
* **Métricas alcanzadas:** 241 pruebas superadas (176 Vitest + 65 Jest), cobertura >96% en líneas y >92% en ramas, 0 advertencias de ESLint y compilación nativa en Expo (Android e iOS).

---

## 2. Sprint Goal

> Como gestor del campus y como estudiante universitario, quiero disponer de un panel web administrativo para supervisar lugares e incidencias y una aplicación móvil resiliente ante pérdida de cobertura, verificada mediante pruebas completas de validación de sistema y acompañada de una memoria académica rigurosa lista para la defensa final de la asignatura.

---

## 3. Alcance y Elementos del Sprint Backlog

| Historia / Tarea | Puntos (SP) | Resultado Esperado | Criterios de Aceptación Verificables |
| :--- | :---: | :--- | :--- |
| **HU-057** — Publicar un aviso | 5 | Formulario en el panel web admin para emitir alertas. | Permite al gestor publicar avisos urgentes (ej. corte de túnel o examen multitudinario) que se reflejan de inmediato. |
| **HU-070** — Gestionar edificios y lugares | 8 | Módulo CRUD en el panel web administrativo (`apps/admin`). | Permite editar nombres, horarios de apertura y accesibilidad PMR de facultades en el catálogo. |
| **HU-094** — Gestionar errores y falta de conexión | 5 | Modo offline en la app móvil con caché local. | Si se pierde la conexión de datos en el campus, la app sigue mostrando el mapa cacheado y la información básica sin cerrarse ni bloquearse. |
| **HU-095** — Utilizar una interfaz accesible | 5 | Cumplimiento de pautas de accesibilidad WCAG 2.1. | Tamaños mínimos de botón táctil (48x48 dp), contraste de color óptimo y soporte para lectores de pantalla TalkBack y VoiceOver. |
| **Cierre Académico** — Memoria y Defensa | 5 | Documentación completa y diapositivas de exposición. | Memoria con todas las métricas de cobertura, trazabilidad de requisitos a pruebas, y presentación preparada para 5 minutos de defensa. |

---

## 4. Reparto Detallado de Responsabilidades (5 Integrantes)

Para llevar el proyecto a su estado final terminado y listo para evaluación:

### 👤 1. Naoufal Kebli (`@Naoufal33`)

* **Rol Scrum:** Developer.
* **Historias asignadas:** `HU-094` (Modo offline y recuperación de red), `HU-095` (Accesibilidad UI).
* **Entregables técnicos:**
  1. Estrategia de caché local en la app móvil: persistencia de lugares y rutas recientes para consulta sin conexión a internet.
  2. Banner informativo sutil de *"Modo sin conexión"* cuando se pierda la cobertura en el campus, con reconexión automática transparente.
  3. Auditoría de contraste cromático y etiquetas de accesibilidad (*accessibilityLabel*) en todos los botones y modales.
* **Módulos / Archivos principales:** `apps/mobile/src/services/storage/`, `apps/mobile/src/components/NetworkBanner.tsx`.

---

### 👤 2. Daniel David (`@ddavid07`)

* **Rol Scrum:** Developer.
* **Historias asignadas:** `HU-090` (Protección de datos), `HU-091` (Control de acceso), `HU-075` (Métricas de estado).
* **Entregables técnicos:**
  1. Endpoints de salud y métricas de producción en NestJS (`GET /health`, `GET /metrics`).
  2. Securización estricta de cabeceras HTTP mediante Helmet y configuración restrictiva de CORS en `apps/api`.
  3. Verificación de políticas de seguridad en dependencias (Scorecard de OpenSSF, escaneo de licencias Apache 2.0).
* **Módulos / Archivos principales:** `apps/api/src/main.ts`, `.github/workflows/scorecard.yml`.

---

### 👤 3. Pablo Palacios (`@pablopr06`)

* **Rol Scrum:** Developer.
* **Historias asignadas:** `HU-070` (Gestión de edificios), `HU-071` (Gestión de categorías), `HU-057` (Publicación de avisos).
* **Entregables técnicos:**
  1. Pantalla de administración en React + Vite (`apps/admin/src/pages/PlacesAdmin.tsx`) con tabla filtrable y formulario de edición.
  2. Interfaz para publicar avisos generales que se propagan a la aplicación móvil.
  3. Estilo visual profesional alineado con la identidad corporativa de la Universidad Complutense de Madrid.
* **Módulos / Archivos principales:** `apps/admin/src/pages/`, `apps/admin/src/components/`.

---

### 👤 4. Pedro Cespón (`@pcespon`)

* **Rol Scrum:** Developer.
* **Historias asignadas:** Validación integral del sistema y cierre de calidad.
* **Entregables técnicos (alineados con el Tema 3 de teoría):**
  1. **Pruebas de Sistema Basadas en Casos de Uso:** Verificación de extremo a extremo de los flujos principales (desde búsqueda hasta navegación y reporte de incidencias).
  2. **Pruebas de Recuperación:** Verificación de que el software se recupera airosamente ante pérdidas forzadas de conexión o respuestas lentas de la API.
  3. **Pruebas de Seguridad:** Validación de que los endpoints administrativos no admiten inyecciones ni parámetros corruptos.
  4. **Matriz de Trazabilidad:** Documento formal que vincula cada Historia de Usuario con su prueba unitaria o de integración correspondiente.
* **Módulos / Archivos principales:** `packages/testing/`, `apps/api/test/`, `apps/mobile/__tests__/system/`.

---

### 👤 5. Charlie Fox (`@charliefox06`)

* **Rol Scrum:** Developer.
* **Historias asignadas:** `HU-021`/`HU-022` (Visualización y filtrado de categorías en campus interactivo), `HU-031`/`HU-032`/`HU-034` (Planificación de rutas accesibles PMR y multimodales EMT/Bicicleta), `HU-057`/`HU-058` (Avisos y Alertas en Web Admin), `HU-097` (Trazabilidad auditable), Documentación académica, actas de cierre y presentación final.
* **Entregables técnicos completados y verificados:**
  1. ✅ **Conclusiones, Métricas y Trabajo Futuro:** Redacción formal de la Sección 7 y actualización de la Sección 6.5 en `memory/memoria-del-proyecto.md`, incluyendo cierre de la matriz de riesgos Barry Boehm RSGR (10/10 riesgos resueltos) y métricas globales de testing.
  2. ✅ **Presentación de la Defensa Final y Guión de Demo:** Elaboración de las diapositivas oficiales en `presentations/presentacion-del-proyecto.md` y estructura de la demo técnica en vivo (5 minutos) cubriendo panel web, contratos e incidencias.
  3. ✅ **Acta de Retrospectiva Final del Proyecto:** Redacción formal en `meetings/sprint-04-retrospectiva-y-cierre.md` con lecciones aprendidas, balance metodológico Scrum vs. Cascada y verificación de la Definition of Done.
  4. ✅ **Módulo de Avisos y Alertas en Web Admin:** Implementación en `apps/admin` (`AnnouncementsView.tsx`, `admin-service.ts`) con tipado estricto, métricas y emisión automática de logs de auditoría para trazabilidad inmutable.
  5. ✅ **Navegación Web y Móvil Campus Completa (Paridad Web & Móvil, HU-021, HU-022, HU-031, HU-032, HU-034):**
     * **Visor Dual Web / Móvil:** Implementación de vistas adaptativas (`CampusScreen.web.tsx`, `CampusMap.web.tsx`, `RouteSheet.web.tsx`) con alternador de vista (`Vista Web` / `Vista Móvil`).
     * **Mapa a Pantalla Completa:** Expansión del mapa interactivo Leaflet/OpenStreetMap a todo el panel derecho con controles flotantes superpuestos (`Centrar campus`, zoom `+` / `−`, insignia de licencia OpenStreetMap).
     * **Filtros por Categoría en Tarjetas:** Checkboxes en dos columnas (Edificios, Aparcamientos, Servicios, Transporte, Bicicletas, Accesos) integradas bajo el mapa en vista móvil y en el panel lateral en web.
     * **Flujo Completo de Rutas Interactivas:** Botón *"Aceptar y ver en el mapa"*, panel colapsable del planificador, hoja de itinerario detallado paso a paso y eliminación de controles redundantes.
     * **Integración Multimodal y Extracción de Sub-polilíneas:** Selección dinámica de modos Peatonal (estándar y PMR accesible), Autobús EMT y Bicicleta, coloreado diferenciado (ámbar para bicis, azul para peatón), extracción de sub-polilíneas para eliminar bucles de ruta en autobuses y fallback automático a ruta a pie cuando las paradas carecen de línea compartida.
     * **Ampliación de Coordenadas del Campus:** Ajuste del bounding box sur para incluir Bellas Artes y Gregorio del Amo.
  6. ✅ **Ampliación de Pruebas Unitarias y TDD Riguroso:**
     * 3 rondas sucesivas de TDD (Test-Driven Development) con detección y corrección de bugs en rutas de bus inconexas, coloreado de polilíneas de bicicletas y etiquetas de tiempo multimodal.
     * Nuevas suites de pruebas unitarias (`MapStatus.test.tsx`, `ExplorerControls.test.tsx`, `RouteLayer.test.tsx`, `RouteSheet.test.tsx`, `transit.spec.ts`).
     * Elevación del conjunto de pruebas a **420 tests verdes** (312 en Vitest y 108 en Jest), cumpliendo umbrales de cobertura (>80% líneas, >70% ramas) y 0 errores de TypeScript.
* **Módulos / Archivos principales:** `UniMovil-docs/memory/`, `UniMovil-docs/presentations/`, `UniMovil-docs/meetings/`, `UniMovil/apps/admin/`, `UniMovil/apps/mobile/src/features/campus/`, `UniMovil/apps/mobile/src/features/routing/`, `UniMovil/apps/mobile/src/features/transit/`.

---

## 5. Estrategia de Pruebas de Sistema y Validación (Tema 3)

Según las diapositivas de la asignatura (profesores Antonio Navarro y Gonzalo Méndez, páginas 13-17 de `03-Pruebas orientadas a objetos.pdf`):

* **Pruebas de Sistema:** A nivel de sistema los detalles de conexiones de clases desaparecen; la validación se centra en las acciones visibles al usuario y salidas reconocibles mediante los casos de uso.
* **Pruebas de Recuperación:** Fuerza el fallo del software (ej. corte súbito de red) y verifica que la recuperación se realiza de forma satisfactoria.
* **Pruebas de Seguridad:** Verifica que los mecanismos de protección incorporados protegen de accesos indebidos y manipulación de datos.

---

## 6. Definition of Done (DoD) de la Entrega Final

Para dar por cerrado y finalizado el proyecto:

1. El monorepo compila íntegramente (`npm run build` en móvil, backend y web admin).
2. La suite completa de pruebas (más de 120 tests) pasa en verde de forma automatizada en el pipeline de GitHub Actions (`ci.yml`).
3. La aplicación móvil está desplegada y lista para demostración en emulador Android o dispositivo físico.
4. La memoria del proyecto está terminada y con todas sus secciones revisadas.
5. El material de la presentación está sincronizado para la defensa oral de la asignatura.
