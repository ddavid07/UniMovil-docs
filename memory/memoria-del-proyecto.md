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
   * 6.1. Fundaciones de ingeniería (trabajo preparatorio)
   * 6.2. Sprint 1: Exploración del campus
   * 6.3. Sprint 2: Rutas peatonales accesibles
   * 6.4. Sprint 3: Transporte público
   * 6.5. Sprint 4: Resiliencia y accesibilidad
   * 6.6. Sprint 5: Cuentas, privacidad y permisos
   * 6.7. Sprint 6: Seguimiento de incidencias y comunicaciones
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

La propuesta inicial contempla Sprints cortos de duración fija. No hay una duración/fechas confirmadas en los registros disponibles; el equipo debe acordarlas para cada ciclo, con un máximo de un mes. Los cuatro eventos formales que estructuran el Sprint son:

1. **Sprint Planning (Planificación del Sprint):** El equipo define qué puede entregarse en el incremento (*Sprint Goal*) y desglosa el trabajo en el *Sprint Backlog*.
2. **Daily Scrum (Scrum Diario):** Reunión diaria de 15 minutos exclusiva del Equipo de Desarrollo para evaluar el progreso hacia el *Sprint Goal*, coordinar las próximas 24 horas y detectar bloqueos (*¿Qué hice ayer? ¿Qué haré hoy? ¿Qué impedimentos tengo?*).
3. **Sprint Review (Revisión del Sprint):** Demostración formal del incremento "Terminado" al Product Owner y partes interesadas, inspeccionando el resultado y actualizando el *Product Backlog*.
4. **Sprint Retrospective (Retrospectiva del Sprint):** Ocasión para que el equipo Scrum se inspeccione a sí mismo (personas, relaciones, herramientas y procesos) y defina un plan de mejora continua para el siguiente Sprint.

### 2.4. Definición de Terminado (*Definition of Done - DoD*)

Una Historia de Usuario se considera estrictamente "Terminada" (*Done*) únicamente si satisface:

* Código escrito en TypeScript estricto, sin advertencias de linting (ESLint) y con formato automático (Prettier).
* Pruebas unitarias implementadas y superadas en el pipeline de Integración Continua (`ci.yml`).
* Integración mediante Pull Request y comprobaciones aplicables del pipeline de CI.
* Documentación y contratos de API actualizados en `@unimovil/contracts`.

---

## 3. Gestión de Riesgos — Plan RSGR (Barry Boehm)

Siguiendo el modelo de gestión proactiva del riesgo de **Barry Boehm** y las directrices del **Software Engineering Institute (SEI)**, este documento conserva una evaluación inicial de riesgos. Las probabilidades, consecuencias y prioridades son propuestas que el equipo debe revisar; no se registra una aprobación ni un seguimiento medido.

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

La prioridad inicial propuesta recae en **R1 (curva de aprendizaje móvil)** y **R3 (desincronización de contratos API-móvil)**. La regla de Pareto es una heurística, no una medición de que exactamente el 20% de riesgos cause el 80% del impacto; revisar esta prioridad con datos del proyecto.

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

---

## 6. Registro de Sprints e Incrementos de Producto

### 6.1. Fundaciones de ingeniería (trabajo preparatorio)

Estas tareas son trabajo preparatorio de ingeniería, no un Sprint adicional ni evidencia de que cada control siga activo. La configuración vigente debe comprobarse en el repositorio antes de afirmar ramas protegidas, workflows o controles de seguridad.

### Estado de los incrementos y planificación

**Corte de estado: 16 de noviembre de 2026.** La existencia de una rama o PR no equivale a una funcionalidad integrada ni a una historia terminada. El estado observable debe actualizarse cuando cambien GitHub y las evidencias.

#### 6.2. Sprint 1: Exploración del campus

El objetivo propuesto es explorar el mapa de Moncloa, buscar/filtrar lugares y consultar una ficha básica. La implementación candidata está en la [PR #23 del repositorio principal](https://github.com/ddavid07/UniMovil/pull/23), que sigue abierta. Por tanto, el incremento no se registra como aceptado en main. Los criterios, riesgos y pruebas pendientes están en [iterations/sprint-01](../iterations/sprint-01/README.md).

#### 6.3. Sprint 2: Rutas peatonales accesibles

La [PR #32](https://github.com/ddavid07/UniMovil/pull/32) sigue abierta hacia main. La propuesta cubre cálculo de rutas y accesibilidad, pero no se considera Sprint terminado ni ruta PMR verificada mientras no haya integración y evidencia de datos/grafo. Véase [iterations/sprint-02](../iterations/sprint-02/README.md).

#### 6.4. Sprint 3: Transporte público

La [PR #34](https://github.com/ddavid07/UniMovil/pull/34) está cerrada como parte del trabajo de una rama de feature; la PR principal #32 continúa abierta. No se afirma que el incremento multimodal esté aceptado en main. Las afirmaciones de líneas, paradas, tiempos y datos deben contrastarse con su fuente, fecha y permisos. Véase [iterations/sprint-03](../iterations/sprint-03/README.md).

#### 6.5. Sprint 4: Resiliencia y accesibilidad

Se conserva como propuesta de incremento de resiliencia/offline y accesibilidad. La documentación anterior citaba una rama y métricas, pero no acredita integración ni una auditoría completa de accesibilidad; esos resultados quedan pendientes de evidencia. Véase [iterations/sprint-04](../iterations/sprint-04/README.md).

#### 6.6. Sprint 5: Cuentas, privacidad y permisos

Propuesta no iniciada: preparar identidad, autorización y consentimiento antes de habilitar operaciones privadas de incidencias y notificaciones. Historias candidatas y riesgos están en [iterations/sprint-05](../iterations/sprint-05/README.md). El equipo debe refinar y seleccionar alcance en Sprint Planning.

#### 6.7. Sprint 6: Seguimiento de incidencias y comunicaciones

Propuesta no iniciada: seguir una incidencia desde el envío hasta la gestión y comunicar su estado. Notificaciones push son opcionales hasta confirmar proveedor, consentimiento y capacidad. Véase [iterations/sprint-06](../iterations/sprint-06/README.md).

Los seis registros son una secuencia candidata, no fechas ni compromisos. La selección de cada Sprint depende de valor, refinamiento, dependencias, riesgos y capacidad real.

---

## 7. Conclusiones y trabajo futuro

En el corte de estado indicado, las funcionalidades de mapa, routing y transporte tienen cambios en PR o ramas, pero no todas están aceptadas en main. No se declaran como producto integrado porcentajes, pruebas, WCAG, funcionamiento offline, cobertura nativa ni tiempos de respuesta sin vincularlos a commit, entorno, ejecución y criterio de aceptación.

El trabajo próximo es completar/refinar la selección de Sprints 1–4 con evidencia y planificar los incrementos 5–6 en Sprint Planning. El resto de historias permanece en Product Backlog; seis registros de Sprint no significan que se haya comprometido o completado todo el alcance del producto.
