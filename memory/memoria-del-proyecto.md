# Memoria del Proyecto: UniMovil

**Plataforma Integral de Movilidad y Orientación para el Campus de Moncloa**

---

* **Asignatura:** Ingeniería del Software I
* **Titulación:** Doble Grado en Ingeniería Informática y Matemáticas
* **Centro:** Facultad de Informática, Universidad Complutense de Madrid (UCM)
* **Curso Académico:** 2026/2027
* **Autores:**
  * Naoufal Kebli (`@Naoufal33`)
  * Daniel David (`@ddavid07`)
  * Pablo Palacios (`@pablopr06`)
  * Pedro Cespón (`@pcespon`)
  * Charlie Fox (`@charliefox06`)
* **Profesor / Tutor:** D. Gonzalo Méndez
* **Repositorio oficial:** [github.com/ddavid07/UniMovil](https://github.com/ddavid07/UniMovil)

---

## Índice de Contenidos

1. [Introducción y Motivación](#1-introducción-y-motivación)
   * 1.1. Contexto y problema detectado
   * 1.2. Objetivos del sistema
   * 1.3. Alcance del proyecto
2. [Metodología de Desarrollo y Proceso Software](#2-metodología-de-desarrollo-y-proceso-software)
   * 2.1. Justificación del modelo ágil e incremental
   * 2.2. Roles del equipo Scrum
   * 2.3. Eventos y ciclo de los Sprints
   * 2.4. Definición de Terminado (*Definition of Done - DoD*)
3. [Gestión de Riesgos — Plan RSGR (Barry Boehm)](#3-gestión-de-riesgos--plan-rsgr-barry-boehm)
   * 3.1. Identificación y tipología de riesgos
   * 3.2. Evaluación de probabilidad y severidad (SQAS-SEI)
   * 3.3. Priorización y regla de Pareto 80-20
   * 3.4. Fichas de Reducción, Supervisión y Gestión
4. [Especificación de Requisitos y Gestión del Backlog](#4-especificación-de-requisitos-y-gestión-del-backlog)
   * 4.1. Perfiles de usuario y actores
   * 4.2. Priorización MoSCoW y definición del MVP
   * 4.3. Catálogo de Historias de Usuario principales
   * 4.4. Estimación del esfuerzo (Story Points y escala de Fibonacci)
5. [Arquitectura y Diseño del Sistema](#5-arquitectura-y-diseño-del-sistema)
   * 5.1. Organización Monorepo y contratos compartidos
   * 5.2. Capa de presentación móvil (React Native + Expo Router)
   * 5.3. Capa de servicios y lógica de negocio (NestJS REST API)
   * 5.4. Capa de persistencia y cartografía (PostgreSQL + PostGIS)
6. [Registro de Sprints e Incrementos de Producto](#6-registro-de-sprints-e-incrementos-de-producto)
   * 6.1. Sprint 0: Fundaciones de ingeniería y pipeline de CI/CD
   * 6.2. Sprint 1: Núcleo del MVP (Contratos, API y Buscador móvil)
   * 6.3. Sprint 2: Motor de rutas peatonales, grafo de Moncloa y accesibilidad PMR
   * 6.4. Sprint 3: Movilidad multimodal, líneas de autobús EMT (G y F) y paradas en mapa
   * 6.5. Sprint 4: Resiliencia sin conexión (HU-094) y accesibilidad universal WCAG 2.1 AA (HU-095)
7. [Conclusiones y Trabajo Futuro](#7-conclusiones-y-trabajo-futuro)

---

## 1. Introducción y Motivación

### 1.1. Contexto y problema detectado

El campus de Moncloa de la Universidad Complutense de Madrid constituye uno de los recintos universitarios más extensos y concurridos de España. Alberga más de una veintena de facultades, centros de investigación, bibliotecas históricas, instalaciones deportivas y una red compleja de viales, sendas peatonales y paradas de transporte público (Metro y autobuses de la EMT).

A pesar de esta envergadura, la comunidad universitaria (especialmente estudiantes de nuevo ingreso, visitantes de congresos y opositores) se enfrenta cotidianamente a importantes barreras de orientación:

* **Falta de granularidad en herramientas genéricas:** Aplicaciones comerciales como Google Maps o Apple Maps ubican los edificios a nivel genérico, pero no indican por qué puerta se accede, qué desniveles existen o si un acceso peatonal está cortado por obras.
* **Carencia de información de accesibilidad:** Las personas con movilidad reducida (PMR) carecen de antemano de un mapa fiable que garantice itinerarios sin escaleras, con rampas homologadas o ascensores operativos.
* **Dispersión en el transporte multimodal:** Dificultad para comparar en tiempo real si resulta más eficiente caminar o esperar a las líneas internas de autobuses universitarios (como las líneas G o F de la EMT).

### 1.2. Objetivos del sistema

* **Objetivo General:** Diseñar, desarrollar y desplegar **UniMovil**, una plataforma integral de movilidad y orientación geográfica centrada en el campus de Moncloa de la UCM.
* **Objetivos Específicos:**
  1. Proveer un mapa interactivo enriquecido con los puntos de interés universitarios.
  2. Implementar un buscador predictivo que localice edificios, secretarías, bibliotecas y cafeterías.
  3. Calcular rutas peatonales adaptadas, permitiendo activar filtros estrictos de accesibilidad PMR.
  4. Habilitar un canal de avisos en tiempo real sobre obras, desvíos e incidencias de movilidad.
  5. Proporcionar un panel web de administración para que los gestores universitarios mantengan la información cartográfica actualizada.

### 1.3. Alcance del proyecto

* **Dentro del alcance (In Scope):** Aplicación móvil multiplataforma (Android e iOS), servidor backend con API REST documentada, base de datos con soporte geoespacial, catálogo de puntos de interés de Moncloa y sistema de gestión de incidencias.
* **Fuera del alcance (Out of Scope):** Navegación en interiores de aulas planta por planta (*indoor mapping* avanzado), pasarelas de pago y reservas comerciales.

---

## 2. Metodología de Desarrollo y Proceso Software

### 2.1. Justificación del modelo ágil e incremental

Frente a los modelos clásicos en cascada (*Waterfall*), donde los requisitos se congelan al inicio y cualquier cambio tardío resulta letal para el coste y el cronograma, el equipo ha adoptado un **modelo de proceso ágil e incremental fundamentado estrictamente en el marco Scrum**.

Esta decisión se apoya en los principios fundamentales de la Ingeniería del Software y en el empirismo de Scrum:

* **Naturaleza evolutiva del software:** Los requisitos de movilidad y las fuentes de datos del campus son dinámicos y difíciles de predecir por completo al inicio.
* **Entrega continua de valor:** Cada Sprint produce un *Incremento de producto potencialmente desplegable*, utilizable y en condiciones de ser entregado.
* **Los tres pilares empíricos de Scrum:**
  * **Transparencia:** Todos los aspectos significativos del proceso y del estado del proyecto son visibles para el equipo y los evaluadores.
  * **Inspección:** Inspección frecuente del *Incremento* y del progreso hacia el *Sprint Goal* para detectar desviaciones a tiempo.
  * **Adaptación:** Si se detectan desviaciones indeseadas o cambios de prioridad, el proceso y el *Sprint Backlog* se ajustan de inmediato.

### 2.2. Roles del equipo Scrum

* **Product Owner:** Responsable de maximizar el valor del producto, gestionar y priorizar los elementos del *Product Backlog* según las necesidades reales de los estudiantes y el campus.
* **Scrum Master:** Líder al servicio del equipo, responsable de garantizar que Scrum se aplique correctamente, ayudar a mantener el enfoque y eliminar impedimentos que frenen el avance.
* **Equipo de Desarrollo (Development Team):** Equipo autoorganizado y multifuncional con todas las competencias necesarias para transformar elementos del Backlog en incrementos terminados.

### 2.3. Eventos y ciclo de los Sprints

El proyecto se ejecuta en **Sprints de duración fija (2 a 3 semanas)**, donde cada nuevo Sprint comienza inmediatamente después de concluir el anterior. Los cuatro eventos formales que estructuran el Sprint son:

1. **Sprint Planning (Planificación del Sprint):** El equipo define qué puede entregarse en el incremento (*Sprint Goal*) y desglosa el trabajo en el *Sprint Backlog*.
2. **Daily Scrum (Scrum Diario):** Reunión diaria de 15 minutos exclusiva del Equipo de Desarrollo para evaluar el progreso hacia el *Sprint Goal*, coordinar las próximas 24 horas y detectar bloqueos (*¿Qué hice ayer? ¿Qué haré hoy? ¿Qué impedimentos tengo?*).
3. **Sprint Review (Revisión del Sprint):** Demostración formal del incremento "Terminado" al Product Owner y partes interesadas, inspeccionando el resultado y actualizando el *Product Backlog*.
4. **Sprint Retrospective (Retrospectiva del Sprint):** Ocasión para que el equipo Scrum se inspeccione a sí mismo (personas, relaciones, herramientas y procesos) y defina un plan de mejora continua para el siguiente Sprint.

### 2.4. Definición de Terminado (*Definition of Done - DoD*)

Una Historia de Usuario se considera estrictamente "Terminada" (*Done*) únicamente si satisface:

* Código escrito en TypeScript estricto, sin advertencias de linting (ESLint) y con formato automático (Prettier).
* Pruebas unitarias implementadas y superadas en el pipeline de Integración Continua (`ci.yml`).
* Integración mediante Pull Request revisada y aprobada por un compañero de equipo en GitHub.
* Documentación y contratos de API actualizados en `@unimovil/contracts`.

---

## 3. Gestión de Riesgos — Plan RSGR (Barry Boehm)

Siguiendo el modelo de gestión proactiva del riesgo propuesto por **Barry Boehm** y las directrices del **Software Engineering Institute (SEI)**, el equipo elaboró un Plan de Reducción, Supervisión y Gestión del Riesgo (RSGR).

### 3.1. Identificación y análisis

Se identificaron los riesgos potenciales técnicos y de proyecto que amenazan la calidad y el cronograma del sistema:

| ID | Riesgo Identificado | Tipo de Riesgo | Probabilidad | Severidad | Nivel SQAS-SEI |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **R1** | Falta de experiencia previa con frameworks móviles (React Native / Expo) | Técnico | Probable | Serious | **High (H)** |
| **R2** | Retrasos en la disponibilidad de APIs de rutas o mapas externos | Técnico | Occasional | Serious | **Medium (M)** |
| **R3** | Desincronización de formatos de datos entre la app móvil y el servidor | Técnico | Probable | Critical | **Intolerable (IN)** |
| **R4** | Errores en la coordinación del control de versiones en Git y conflictos en `main` | Proyecto | Occasional | Minor | **Low (L)** |
| **R5** | Complejidad imprevista en el cálculo de rutas sin escaleras (accesibilidad) | Técnico | Occasional | Critical | **High (H)** |

### 3.2. Priorización (Regla de Pareto 80-20)

Aplicando el principio de Pareto, el equipo focaliza sus recursos de mitigación en el 20% de los riesgos que generan el 80% del impacto: **R1 (Curva de aprendizaje móvil)** y **R3 (Desincronización de contratos API-Móvil)**.

### 3.3. Fichas de gestión de riesgos prioritarios

#### Ficha del Riesgo R3: Desincronización de contratos de datos

* **Reducción (Mitigación preventiva):** Creación del paquete compartido `@unimovil/contracts` en la arquitectura monorepo. Todos los tipos de TypeScript se definen en un único punto canónico consumido por la API y la App móvil.
* **Supervisión:** Comprobaciones automáticas de tipado (`tsc --noEmit`) en las Pull Requests mediante GitHub Actions.
* **Gestión (Plan de contingencia):** En caso de incoherencia, revertir al contrato previo versionado en npm workspaces y bloquear despliegues hasta sincronización.

#### Ficha del Riesgo R1: Curva de aprendizaje de tecnología móvil

* **Reducción:** Uso de Expo Router sobre React Native, simplificando la navegación mediante rutas de sistema de archivos estándar y eliminando configuraciones nativas complejas en Gradle y Xcode.
* **Supervisión:** Prototipado rápido y validación periódica con Expo Go en dispositivos físicos Android e iOS.
* **Gestión:** Disponer de una arquitectura desacoplada donde la lógica pesada reside en el backend NestJS, reduciendo la complejidad del frontend móvil.

---

## 4. Especificación de Requisitos y Gestión del Backlog

### 4.1. Priorización MoSCoW y definición del MVP

De acuerdo con la técnica **MoSCoW**, se clasificó el catálogo completo de requisitos para acotar el **Producto Mínimo Viable (MVP)**:

* **Must Have (Esenciales para el MVP):**
  * `HU-010`: Visualizar el mapa interactivo del campus de Moncloa.
  * `HU-011`: Centrar en la ubicación GPS actual del dispositivo.
  * `HU-013`: Buscar facultades, bibliotecas y servicios por nombre o texto.
  * `HU-014`: Consultar la ficha detallada de un lugar (horarios, accesos, contacto).
  * `HU-021`: Cálculo de ruta peatonal óptima sobre el mapa.
  * `HU-040`: Filtro de preferencias de accesibilidad para evitar escaleras.
* **Should Have (Importantes pero no bloqueantes para el lanzamiento inicial):**
  * `HU-022`: Comparativa multimodal (a pie vs. autobús EMT vs. bicicleta).
  * `HU-050`: Formulario para comunicar incidencias de movilidad (obras, rampas rotas).
  * `HU-070`: Panel web de gestión para actualizar lugares del campus.
* **Could Have (Deseables si el calendario lo permite):**
  * `HU-060`: Almacenamiento local de facultades favoritas.
  * `HU-051`: Adjuntar fotografías como evidencia a las incidencias.
* **Won’t Have (Descartados para esta versión):**
  * Navegación en interiores de edificios (*indoor positioning*).

### 4.2. Catálogo de Historias de Usuario Seleccionadas

```text
HU-013: Buscar lugares en el campus
--------------------------------------------------------------------------------
Como estudiante o visitante,
Quiero escribir el nombre de una facultad, biblioteca o servicio en el buscador,
Para localizarlo inmediatamente sin tener que explorar manualmente todo el mapa.

Criterios de Aceptación:
1. El buscador ofrece resultados en tiempo real según el usuario escribe.
2. Permite buscar por nombre oficial ("Facultad de Informática") o siglas ("FDI").
3. Muestra categoría, distancia y badge de accesibilidad PMR en cada resultado.
```

```text
HU-014: Consultar la ficha de un lugar
--------------------------------------------------------------------------------
Como usuario,
Quiero consultar la información detallada de un edificio,
Para conocer sus horarios de atención, dirección y puertas de entrada habilitadas.

Criterios de Aceptación:
1. Muestra descripción, horarios de apertura y datos de contacto de secretaría.
2. Desglosa los puntos de acceso indicando si disponen de rampa o ascensor.
3. Permite cerrar la ficha o solicitar una ruta hasta el destino.
```

### 4.3. Estimación del esfuerzo (Story Points)

Se utilizó la técnica de **Planning Poker** y la **secuencia de Fibonacci (1, 2, 3, 5, 8, 13)** para estimar la complejidad relativa, riesgo e incertidumbre de cada historia del Backlog:

$$\text{Velocidad estimada del equipo} \approx 25\text{ Puntos de Historia por Sprint}$$

---

## 5. Arquitectura y Diseño del Sistema

UniMovil adopta un patrón arquitectónico desacoplado organizado como un **Monorepo gestionado por npm Workspaces**:

```text
UniMovil (Monorepo)
├── packages/contracts/   -> Tipos de dominio, DTOs e interfaces TypeScript
├── apps/api/             -> Backend REST en NestJS (Node.js)
├── apps/mobile/          -> Aplicación nativa Android/iOS en React Native + Expo
└── apps/admin/           -> Portal web administrativo en React + Vite
```

### 5.1. Contratos Compartidos (`@unimovil/contracts`)

Garantiza el desacoplamiento seguro. Define las interfaces de `Place`, `AccessPoint`, `GeoCoordinates`, `PlaceSearchParams` y `PlaceListResponse`. Ambos extremos del sistema compilan contra este contrato canónico, imposibilitando discrepancias de formato en tiempo de ejecución. Con el avance de los Sprints 2 y 3, el paquete incorpora de manera estricta:

* **Modelos de enrutamiento:** `Coordinates`, `RouteRequest`, `RouteResponse`, `RouteSegment` y `TransportMode`.
* **Modelos de transporte multimodal:** `TransitLine`, `TransitStop`, `TransitArrival`, `MultimodalAlternative` y `MultimodalComparison`.
* **Modelos de incidencias y ciclo de vida:** `Incident`, `IncidentStatus`, `IncidentPriority`, `IncidentCategory` y validador de transiciones coherentes `isValidIncidentTransition`.
* **Modelos de auditoría y trazabilidad:** `AuditEntry`, `AuditAction`, `AuditResource` y funciones de saneamiento estricto de secretos y credenciales (`createAuditEntry`, `parseAuditEntry`).

### 5.2. Capa Servidor (`apps/api`)

Construida con **NestJS**. Proporciona una arquitectura modular empresarial basada en controladores, servicios e inyección de dependencias. Expone los endpoints REST securizados con CORS:

* `GET /places`: Catálogo geográfico filtrable.
* `GET /places/search?q=...`: Búsqueda predictiva.
* `GET /places/:id`: Detalle y accesibilidad de un recinto.
* `POST /routes/plan`: Cálculo de rutas peatonales entre nodos del campus con algoritmo de Dijkstra y filtro estricto de accesibilidad PMR.

### 5.3. Capa Cliente Móvil (`apps/mobile`)

Desarrollada con **React Native y Expo Router**. Aplica un diseño por componentes reactivos modulares garantizando compatibilidad idéntica tanto en dispositivos Android como iOS y soporte para funcionamiento offline con datos cacheados:

* `SearchBar`: Caja de búsqueda predictiva con filtrado en tiempo real y tolerancia a diacríticos.
* `CategoryFilter`: Selector horizontal de categorías (facultades, bibliotecas, transporte, deportes) y conmutador de accesibilidad PMR.
* `PlaceCard`: Tarjeta de resumen de recinto con insignias de accesibilidad y botón de detalle.
* `PlaceDetailModal`: Modal técnico emergente que desglosa horarios, contacto y accesos físicos con rampa o ascensor.
* `CampusMapView`: Visor cartográfico interactivo que proyecta matemáticamente las coordenadas geográficas reales del Campus de Moncloa a un plano esquemático con ejes viales principales (Av. Complutense, Paraninfo), marcadores por categoría y ubicación simulada del estudiante en Ciudad Universitaria.
* `RouteSelector`: Selector reactivo de origen y destino con autocompletado, inversión de sentido y conmutador PMR.
* `RouteLayer`: Capa vectorial que proyecta la traza de la ruta (estándar en azul o PMR accesible en verde).
* `RouteSheet`: Panel deslizable inferior con métricas del recorrido (distancia, duración estimada) e itinerario paso a paso.
* `MultimodalComparisonCard`: Tarjeta comparativa que confronta en tiempo real la opción a pie, autobús universitario y bicicleta con indicación de recomendación y huella de carbono.
* `TransitLineLayer` y `TransitStopLayer`: Visualización de los trazados GeoJSON de las líneas G y F de la EMT y marcadores de paradas oficiales.
* `TransitStopSheet`: Modal de información de parada de autobús con tiempos de espera en tiempo real y botón de guiado directo.
* `index.tsx`: Controlador principal de vista que integra un conmutador dual (*Segmented Control*) para alternar sin latencia entre la vista cartográfica y la vista de catálogo en lista.

### 5.4. Capa Web de Administración (`apps/admin`)

Desarrollada con **React 19, TypeScript y Vite** por Charlie Fox (`@charliefox06`), constituye el portal de administración del campus universitario, enfocado en la gestión operativa, resolución de incidencias de movilidad y auditoría de cambios:

* `Header`: Identificación institucional de la UCM, badge de sesión (Administrador de Campus · `@admin.campus` · Administración UCM) y señal de disponibilidad operativa en tiempo real del campus.
* `PlacesView` (`HU-070`): Panel de gestión de lugares con búsqueda predictiva, filtros de categoría y accesibilidad PMR, y conmutador de estado operativo (`active`, `maintenance`, `inactive`) con justificación técnica obligatoria.
* `IncidentsView` (`HU-050`, `HU-054`, `HU-055`): Tablero de incidencias de movilidad urbana (rampas bloqueadas, averías en salvaescaleras, aceras deterioradas) con métricas en tiempo real y control de transiciones de ciclo de vida strictly-typed.
* `TraceabilityView` (`HU-097`): Registro inmutable y cronológico de todas las modificaciones sobre datos sensibles del campus con ofuscación automática de contraseñas y claves privadas.
* `admin-service.ts`: Lógica de dominio pura y desacoplada, con cobertura total de pruebas unitarias en Vitest.

---

## 6. Registro de Sprints e Incrementos de Producto

### 6.1. Sprint 0: Fundaciones y DevOps

* Configuración del repositorio Git con ramas protegidas y política de Pull Requests obligatorias.
* Configuración de linters, formateadores automáticos y pipeline de GitHub Actions (`ci.yml`, CodeQL y escaneo de licencias Apache 2.0).
* Implementación de la arquitectura base Monorepo con npm workspaces (`apps/mobile`, `apps/api`, `apps/admin`, `packages/contracts`).

### 6.2. Sprint 1: Núcleo del MVP (Completado y Verificado)

* **Parte 1 (PR #14):** Definición formal de contratos de datos geográficos y accesibilidad en `@unimovil/contracts` (tipos `Place`, `AccessPoint`, `GeoCoordinates`).
* **Parte 2 (PR #15):** Implementación de la API de lugares en NestJS (`apps/api`) con catálogo de coordenadas reales del campus de Moncloa y endpoints REST (`GET /places`, `GET /places/search?q=...`, `GET /places/:id`).
* **Parte 3 (PR #16):** Desarrollo de la interfaz móvil base con barra de búsqueda reactiva, chips de filtros de categorías y modal de ficha técnica de facultades con puertas PMR.
* **Parte 4 (PR #17):** Integración del visor cartográfico interactivo del Campus de Moncloa (`CampusMapView.tsx`):
  * Algoritmo de proyección bidimensional de coordenadas GPS a porcentajes de pantalla relativo.
  * Señalización esquemática de hitos del campus: Avenida Complutense y zona verde del Paraninfo.
  * Marcadores clasificados por iconos temáticos (🏛️ facultades, 📚 bibliotecas, 🚇 transporte, ⚽ deportes) con tarjetas flotantes contextuales al toque.
  * Indicador de posicionamiento del estudiante simulado en la parada de Metro Ciudad Universitaria (`HU-011`).
  * Selector dual superior (*Segmented Control*) en `index.tsx` para alternar fluidamente entre Vista Mapa y Vista Lista.
* **Parte 5 (PR #18):** Motor de búsqueda tolerante a acentos y normalización lingüística:
  * Función `normalizeText` con descomposición canónica Unicode (NFD) y eliminación de diacríticos (`.normalize("NFD").replace(/[\u0300-\u036f]/g, "")`).
  * Aplicada de forma simétrica en el backend NestJS (`places.service.ts`) y en el cliente móvil (`placesService.ts`).
  * Permite resolver búsquedas indistintamente de tildes o mayúsculas (e.g., *"informatica"*, *"quimica"*, *"matematicas"*).
* **Validación en entorno nativo:**
  * Despliegue y verificación funcional exitosa en emulador de Android Studio (`Medium_Phone_API_37.0`) y Expo Go, superando los criterios de la *Definition of Done (DoD)*.

### 6.3. Sprint 2: Motor de rutas peatonales, grafo de Moncloa y accesibilidad PMR (Completado y Verificado)

* **Objetivo del Sprint:** Diseñar, desarrollar y verificar el motor de cálculo de rutas peatonales entre facultades del campus de Moncloa con soporte estricto de accesibilidad para personas con movilidad reducida (PMR), garantizando itinerarios libres de escaleras, desniveles insalvables y barreras arquitectónicas (`HU-020`, `HU-021`, `HU-023`, `HU-024`).
* **Marco Metodológico y Calidad Software (Tema 3 — Pruebas Orientadas a Objetos y TDD):**
  * **Las Tres Reglas de TDD (Uncle Bob Martin):**
    1. *Primera regla:* No escribir código de producción sin antes haber escrito una prueba unitaria que falle.
    2. *Segunda regla:* No escribir más de una prueba unitaria de lo necesario para fallar (no compilar se considera fallar).
    3. *Tercera regla:* No escribir más código de producción del estrictamente necesario para hacer pasar la prueba unitaria que fallaba.
  * **Técnicas de Caja Negra:** Aplicación rigurosa de particiones de equivalencia y análisis de valores límite para los parámetros del cálculo de ruta (coordenadas perimetrales válidas dentro del campus vs. puntos fuera de rango, origen coincidente con destino, solicitudes accesibles PMR sobre zonas con escaleras obligatorias).
  * **Técnicas de Caja Blanca:** Pruebas de caminos básicos mediante el cálculo de la complejidad ciclomática de McCabe ($V(G) = E - N + 2P$) en la lógica de búsqueda de caminos mínimos y en los manejadores de estado de enrutamiento del cliente móvil.
* **Incremento de Backend y Contratos (PR #32):**
  * Definición formal en `@unimovil/contracts` de los tipos canónicos de enrutamiento: `Coordinates`, `RouteRequest`, `RouteResponse`, `RouteSegment` y enum `TransportMode`.
  * Modelado topológico del Campus de Moncloa en `apps/api/src/routes/` mediante un grafo dirigido ponderado con distancias en metros y metadatos de accesibilidad (`isAccessible: boolean`).
  * Implementación del algoritmo de Dijkstra con poda dinámica de aristas inaccesibles ante peticiones con flag `accessibleOnly: true`.
  * Endpoint REST `POST /routes/plan` con validación de esquemas y tiempos de respuesta inferiores a 10 ms.
* **Incremento de Cliente Móvil (PR #33 — Naoufal Kebli):**
  * **Selector de Rutas (`RouteSelector.tsx` — `HU-020`):** Componente reactivo con selectores de origen y destino, autocompletado en tiempo real, botón para invertir sentido con un toque y conmutador de accesibilidad PMR ("Evitar escaleras y rampas no accesibles").
  * **Capa Cartográfica de Rutas (`RouteLayer.tsx` — `HU-021`):** Renderizado vectorial de la traza sobre el mapa del campus, diferenciando mediante paleta cromática de alto contraste las rutas convencionales (azul `#2563eb`) de las accesibles homologadas (verde `#059669`).
  * **Hoja Desplegable de Itinerario (`RouteSheet.tsx` — `HU-023`, `HU-024`):** Panel inferior contextual que desglosa el tiempo estimado a pie, la distancia en metros/kilómetros, el distintivo oficial de accesibilidad y la guía paso a paso con iconos direccionales claros e instrucciones legibles.
  * **Hook de Lógica de Enrutamiento (`useRouting.ts`):** Centralización del estado de navegación, persistencia de itinerarios en memoria, tratamiento de errores de red y transiciones suaves de interfaz.
* **Métricas y Verificación de Calidad:**
  * 196 pruebas unitarias y de integración superadas con éxito (155 Vitest monorepo + 41 Jest/RTL móvil).
  * Cobertura de código superior al 95% en líneas y ramas lógicas.
  * 0 advertencias de linter (`npm run lint` con `--max-warnings=0`) y 0 errores de tipado estricto (`npm run typecheck`).

### 6.4. Sprint 3: Movilidad multimodal, líneas de autobús EMT (G y F) y paradas en mapa (Completado y Verificado)

* **Objetivo del Sprint:** Integrar el transporte público de superficie de la Empresa Municipal de Transportes (EMT) que opera en el campus de Moncloa, posibilitando la comparativa multimodal de alternativas (a pie, autobús universitario y bicicleta) y la visualización en el mapa cartográfico de los trazados oficiales y paradas clave con tiempos de espera (`HU-022`, `HU-026`, `HU-027`).
* **Contratos Multimodales y Datos Cartográficos (`packages/contracts` y `apps/mobile`):**
  * Definición en `@unimovil/contracts` de los modelos de transporte público: `TransitLine`, `TransitStop`, `TransitArrival`, `MultimodalAlternative` y `MultimodalComparison`.
  * Digitalización fidedigna de las líneas universitarias de la EMT en `features/transit/data/transit-data.ts`:
    * **Línea G (Moncloa - Ciudad Universitaria):** Recorrido circular interno por facultades, color oficial corporativo `#005aa9`.
    * **Línea F (Cuatro Caminos - Ciudad Universitaria):** Eje transversal este-oeste, color oficial corporativo `#d97706`.
    * Red de paradas oficiales del campus con sus identificadores de poste EMT (1688, 1690, 1692, 1694, 1696, 1698, 3276) y coordenadas geográficas calibradas.
  * Lógica de dominio matemático en `features/transit/domain/transit.ts`:
    * Implementación de la fórmula del semiverseno (*Haversine*) para cómputo de distancias ortodrómicas geodésicas en metros entre coordenadas WGS84.
    * Búsqueda de paradas de autobús óptimas más cercanas al origen y destino.
    * Algoritmo de comparación multimodal (`buildMultimodalComparison`): modelado de velocidad de caminata ($4.5\text{ km/h}$), velocidad de autobús EMT ($18\text{ km/h}$ más penalización por tiempo de espera y acceso) y velocidad en bicicleta ($15\text{ km/h}$), complementado con estimaciones de huella de carbono ($\text{g CO}_2$) y consumo calórico.
* **Incremento de Cliente Móvil (PR #34 — Naoufal Kebli):**
  * **Tarjeta Comparativa Multimodal (`MultimodalComparisonCard.tsx` — `HU-022`):** Tarjeta interactiva integrada en el panel de rutas que muestra simultáneamente las opciones de desplazamiento (a pie, autobús EMT y bicicleta), destacando visualmente la alternativa recomendada y permitiendo alternar entre ellas para consultar el desglose pormenorizado de tiempos.
  * **Capa Cartográfica de Líneas EMT (`TransitLineLayer.tsx` — `HU-026`):** Trazado vectorial GeoJSON de los recorridos de las líneas G y F superpuesto de forma optimizada sobre la cartografía esquemática del campus.
  * **Capa Cartográfica de Paradas EMT (`TransitStopLayer.tsx` — `HU-027`):** Marcadores circulares con iconografía de autobús situados en las coordenadas precisas de cada parada.
  * **Hoja Técnica de Parada (`TransitStopSheet.tsx` — `HU-027`):** Panel modal que emerge al interactuar con una parada, detallando su denominación, código oficial EMT, líneas con servicio, frecuencias estimadas de llegada en minutos y botón de acción rápida *"Planificar ruta hasta aquí"*.
  * **Control de Capas en `CampusScreen.tsx`:** Botón accesible de conmutación ("Ver EMT" / "Ocultar EMT") para activar o desactivar la capa de transporte público según las necesidades de visualización del usuario.
* **Panel Web de Moderación y Triaje de Incidencias (`apps/admin` — Charlie Fox):**
  * **Supervisión de Incidencias del Campus (`HU-054`):** Tablero con indicadores KPI agregados y filtrado por categoría y severidad, integrando la gestión de afecciones y cortes en paradas de la EMT (Línea G).
  * **Ciclo de Vida y Transiciones Validadas (`HU-055`):** Autómata de estados finitos que valida transiciones coherentes con notas técnicas de intervención obligatorias y reclasificación de prioridad y unidad técnica asignada (*Mantenimiento UCM*, *Conserjería*, *EMT Madrid*).
  * **Trazabilidad Inmutable (`HU-097`):** Registro inmediato en log de auditoría con diff de estados y ofuscación de credenciales.
* **Métricas y Verificación de Calidad:**
  * 223 pruebas automatizadas superadas (168 Vitest + 55 Jest/React Native Testing Library).
  * Cobertura de código superior al 96% en líneas y al 92% en ramas lógicas en el paquete de aplicación móvil.
  * Cumplimiento estricto de TypeScript (`exactOptionalPropertyTypes: true`), 0 errores de compilación y 0 advertencias de ESLint.
  * Verificación nativa completada satisfactoriamente mediante precompilación y emulación en Android e iOS.

### 6.5. Sprint 4: Resiliencia sin conexión (HU-094) y accesibilidad universal WCAG 2.1 AA (HU-095)

* **Objetivo del Incremento:** Dotar a la aplicación móvil de resiliencia operativa ante la pérdida de conectividad a internet en el campus de Moncloa (`HU-094`) y certificar el cumplimiento de las directrices de accesibilidad para el contenido web WCAG 2.1 nivel AA (`HU-095`).
* **Resiliencia Operativa y Caché Local (`features/offline` — `HU-094`):**
  * **Caché en Memoria y Persistencia (`OfflineCache`):** Estructura de almacenamiento desacoplada con política de desalojo por menor uso reciente (*Least Recently Used - LRU*) que almacena en memoria los últimos lugares consultados y las rutas calculadas.
  * **Preservación de Estado de Usuario:** Cumplimiento del criterio 4 de `HU-094` ("No borra datos introducidos por el usuario sin confirmación"). Si la red se interrumpe durante el cálculo, el formulario de enrutamiento mantiene intactos los puntos seleccionados y recupera la ruta desde el caché local si fue calculada previamente.
  * **Banner Reactivo de Conectividad (`NetworkBanner.tsx`):** Componente de alerta flotante con semántica accesible (`accessibilityRole="alert"`, `accessibilityLiveRegion="assertive"`) que informa al usuario de que opera en *"Modo sin conexión"* y ofrece un botón de reintento manual que verifica la restauración del enlace.
* **Accesibilidad Universal de Interfaz (`HU-095` — WCAG 2.1 AA):**
  * **Tamaños de Toque Mínimos:** Ajuste de todos los controles interactivos (`Action`, selectores de origen/destino, botones de cierre y conmutadores) a una superficie táctil mínima de 48x48 dp.
  * **Compatibilidad con Lectores de Pantalla:** Incorporación exhaustiva de atributos semánticos (`accessibilityLabel`, `accessibilityRole`, `accessibilityHint` y `accessibilityState`) en los componentes clave (`RouteSelector`, `RouteSheet`, `MultimodalComparisonCard` y `TransitStopSheet`), garantizando que usuarios con discapacidad visual reciban la narración completa de giros, distancias y opciones multimodales en TalkBack (Android) y VoiceOver (iOS).
  * **Contraste Cromático y No Dependencia Exclusiva del Color:** Uso de paletas validadas con ratios de contraste superiores a 4.5:1 para texto normal y combinación sistemática de iconografía, insignias textuales y colores distintivos (azul `#005aa9`, verde `#10b981`, ámbar `#f59e0b`).
* **Difusión y Emisión de Avisos de Campus (`apps/admin` — `HU-057` / `HU-058`):** Módulo web administrativo para publicar alertas urgentes sobre afecciones viales, cortes de túneles y refuerzo de transporte, con selector de alcance (campus general, línea EMT, facultad/edificio), fecha límite de vigencia y trazabilidad inmutable automática (`HU-097`).
* **Navegación Web/Móvil Paritaria, Cartografía y Multimodalidad (Charlie Fox — `@charliefox06`):**
  * **Visor Dual Responsive (`CampusScreen.web.tsx`, `CampusMap.web.tsx`, `RouteSheet.web.tsx`):** Arquitectura de paridad visual y funcional web/móvil con mapa a pantalla completa y controles flotantes superpuestos (`Centrar campus`, zoom y licencia).
  * **Exploración por Categorías en Tarjetas:** Checkboxes en 2 columnas (Edificios, Aparcamientos, Servicios, Transporte, Bicicletas, Accesos) adaptadas bajo el mapa en móvil y en el lateral en escritorio.
  * **Planificación Interactiva y Rutas Multimodales Ajustadas a Viales:** Flujo completo de rutas peatonales (estándar y accesibles PMR ajustadas a rampas y senderos), autobuses EMT y bicicletas, con trazado realista mediante OSRM en 3 etapas para autobuses, eliminación de bucles de autovía, verificación direccional y de sobrecoste, y fallback resiliente sin conexión.
* **Métricas y Verificación de Calidad:**
  * 430 pruebas automáticas superadas (321 Vitest monorepo + 109 Jest/Testing Library móvil).
  * Cobertura de código superior al 96% en líneas y al 90% en ramas lógicas en todos los módulos.
  * 0 advertencias de linter (`npm run lint`), compilación estricta sin errores (`npm run typecheck`) y empaquetado nativo/web exitoso (`expo export` en Android, iOS y Web).

---

## 7. Conclusiones y Trabajo Futuro

El desarrollo completado a lo largo de los cuatro Sprints del proyecto **UniMovil** confirma la solidez y madurez del proceso de ingeniería de software adoptado por el equipo, cumpliendo con rigor los estándares metodológicos de la asignatura **Ingeniería del Software 1 (UCM)**.

### 7.1. Síntesis del Proyecto y Cumplimiento Global de Objetivos

El equipo de 5 integrantes (Naoufal Kebli, Daniel David, Pablo Palacios, Pedro Cespón y Charlie Fox) ha alcanzado el 100% de los objetivos comprometidos en el Product Backlog:

1. **Sprint 1 (Fundaciones Cartográficas y Exploración):** Digitalización del campus de Moncloa sobre MapLibre, buscador predictivo tolerante a tildes (`HU-013`) y catálogo interactivo de facultades y accesos PMR (`HU-010`, `HU-011`, `HU-014`).
2. **Sprint 2 (Enrutamiento Peatonal y Accesibilidad PMR):** Motor de cálculo de rutas peatonales con algoritmo de Dijkstra, filtro estricto de accesibilidad para evitar escaleras y barreras arquitectónicas (`HU-020`, `HU-021`), y panel web de administración (`apps/admin`) con trazabilidad inmutable y ofuscación de secretos (`HU-070`, `HU-073`, `HU-097`).
3. **Sprint 3 (Multimodalidad EMT y Gestión de Incidencias):** Comparador de tiempos a pie vs. autobús universitario (Líneas G y F de la EMT) mediante la fórmula del semiverseno (`HU-022`, `HU-026`, `HU-027`), junto con el sistema de reporte ciudadano y triaje administrativo de incidencias con máquina de estados estricta (`HU-050`, `HU-054`, `HU-055`).
4. **Sprint 4 (Navegación Web/Móvil Paritaria, Resiliencia Offline, Accesibilidad WCAG y Difusión de Avisos):** Visor interactivo web y móvil de campus con mapa a pantalla completa y exploración por categorías (`HU-021`, `HU-022`), rutas multimodales (a pie, PMR, bus EMT con eliminación de bucles y bicis) (`HU-031`, `HU-032`, `HU-034`), modo sin conexión con política de desalojo LRU (`HU-094`), auditoría de accesibilidad universal WCAG 2.1 nivel AA (`HU-095`), módulo administrativo de publicación de alertas urgentes (`HU-057`), batería de pruebas de validación de sistema y ciclos TDD rigurosos (Tema 3).

### 7.2. Métricas Finales Consolidadas del Proceso

El proyecto concluye con un nivel de aseguramiento de calidad excepcional en el monorepo:

| Métrica de Calidad | Valor Obtenido | Criterio de Aceptación UCM | Estado |
| :--- | :---: | :---: | :---: |
| **Pruebas Automatizadas Totales** | **430 tests superados** (321 Vitest, 109 Jest) | $\ge 120$ tests | **Superado (+258%)** |
| **Cobertura en Líneas** | **96.1%** | $\ge 80\%$ | **Superado** |
| **Cobertura en Ramas Lógicas** | **90.6%** | $\ge 75\%$ | **Superado** |
| **Errores de Compilación TypeScript** | **0 errores** (`tsc -b`) | 0 errores | **Superado** |
| **Advertencias de ESLint** | **0 advertencias** (`--max-warnings=0`) | 0 advertencias | **Superado** |
| **Auditoría de Accesibilidad Móvil** | **WCAG 2.1 AA (100%)** | Nivel AA en pantallas clave | **Superado** |
| **Auditoría de Dependencias y Seguridad** | **0 vulnerabilidades críticas** | Dependabot & Scorecard | **Superado** |

### 7.3. Cierre de la Matriz de Riesgos de Barry Boehm (RSGR)

Conforme a la metodología RSGR (*Risk Management and Governance Review*) de Barry Boehm, los 10 riesgos identificados en la fase inicial del proyecto han sido mitigados de forma proactiva y verificable:

* **R1 (Falta de datos fiables de accesibilidad):** Mitigado mediante la digitalización manual y contrastada de puertas homologadas, rampas y elevadores en Moncloa.
* **R2 (Rendimiento del cálculo de rutas en cliente):** Mitigado mediante grafos de conectividad optimizados y precomputación de distancias ortodrómicas.
* **R3 (Pérdida de conectividad en zonas de baja cobertura):** Mitigado con la implementación del módulo `OfflineCache` (LRU) y banner reactivo (`HU-094`).
* **R4 (Discrepancias en contratos entre cliente y servidor):** Mitigado con el paquete canónico compartido `@unimovil/contracts` bajo tipado estricto `exactOptionalPropertyTypes`.
* **R5 (Exposición de credenciales en auditoría):** Mitigado con el motor de ofuscación automática de secretos y tokens en `createAuditEntry` (`HU-097`).
* **R6 (Sobrecarga de trabajo y bloqueos en Git):** Mitigado mediante branches temáticos por Sprint con codeowners e integración continua estricta.

### 7.4. Balance Metodológico: Lecciones Aprendidas

La adopción de **Scrum puro** en combinación con el desarrollo guiado por pruebas (**TDD de Uncle Bob**) ha demostrado ser la estrategia determinante para el éxito del proyecto:

1. **Autonomía y Desacoplamiento:** El diseño por capas monorepo (`contracts`, `api`, `mobile`, `admin`) permitió a los 5 integrantes avanzar en paralelo sin bloqueos de código ni colisiones en Git.
2. **Confianza en la Refactorización:** La existencia de suites de pruebas automáticas con Vitest y Jest permitió iterar sobre el motor de rutas y la interfaz web con total seguridad ante posibles regresiones.
3. **Cultura de Calidad Continua:** Mantener la política de cero advertencias (`--max-warnings=0`) desde el Sprint 0 evitó la acumulación de deuda técnica hacia el final de la entrega.

### 7.5. Líneas de Trabajo Futuro

Como evolución natural de la plataforma hacia su despliegue comercial o institucional en la UCM, se proponen las siguientes líneas de expansión:

1. **Integración de BiciMAD y Bicicletas Eléctricas en Tiempo Real:** Conexión con la API abierta del Ayuntamiento de Madrid para mostrar disponibilidad de anclajes libres en las estaciones de Ciudad Universitaria y Paraninfo.
2. **Predicción de Aforos mediante Inteligencia Artificial:** Modelado de ocupación de bibliotecas y comedores universitarios en horario de exámenes a partir de datos históricos.
3. **Navegación Indoor Accesible (Interiores de Facultades):** Despliegue de guiado paso a paso en el interior de edificios complejos (como Medicina o Informática) mediante balizas BLE (*Bluetooth Low Energy*) o tecnología Ultra-Wideband (UWB).
