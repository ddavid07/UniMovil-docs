# Guión y Diapositivas de la Defensa Final de UniMovil (5 Minutos)

> **Presentación oficial de fin de proyecto de Ingeniería del Software 1 (UCM).**  
> **Tribunal / Docente:** Prof. D. Gonzalo Méndez.  
> **Equipo 5:** Charlie Fox (`@charliefox06`), Naoufal Kebli (`@Naoufal33`), Pedro Cespón (`@pcespon`), Daniel David (`@ddavid07`) y Pablo Palacios (`@pablopr06`).  
> **Duración total:** 5 minutos estrictos + turno de preguntas.

---

## ⏱️ Estructura y Cronograma de la Exposición

```
[0:00 - 0:45] Diapositiva 1: Motivación, Problema y Valor Diferencial
[0:45 - 1:30] Diapositiva 2: Arquitectura Monorepo y Contratos Canónicos
[1:30 - 2:30] Diapositiva 3: Incremento Técnico por Sprints (S1 a S4)
[2:30 - 3:45] Diapositiva 4: Demo Técnica en Vivo (Flujo Móvil + Web Admin)
[3:45 - 4:30] Diapositiva 5: Estrategia de Pruebas y Calidad (Tema 3)
[4:30 - 5:00] Diapositiva 6: Cierre, Riesgos (Boehm RSGR) y Conclusiones
```

---

## 📽️ Diapositiva 1 (0:00 – 0:45) — Motivación y Problema en Ciudad Universitaria

### Contenido visual:
* Logotipo de la **UCM** y marca **UniMovil**.
* Fotografía aérea del Campus de Moncloa y mapa de Ciudad Universitaria.
* Puntos clave:
  * Más de 20 facultades y 100.000 desplazamientos diarios.
  * Google Maps ubica edificios genéricos, pero desconoce puertas accesibles, desniveles y escaleras.
  * Carencia de información unificada sobre si compensa caminar o tomar las líneas de autobús universitario (G o F de la EMT).

### Guión del ponente:
> *"Buenos días, profesor. Somos el equipo de UniMovil. Todos los que estudiamos en Ciudad Universitaria nos hemos encontrado con la misma situación: sales del metro con 15 minutos para llegar a una clase o examen en otra facultad, y no sabes si llegarás a pie, si te sale más a cuenta esperar al autobús G o F, o si la rampa que necesitas está cortada por obras.  
> Las herramientas comerciales ubican los edificios a nivel genérico, pero no bajan al detalle peatonal, accesible ni multimodal de nuestro campus. Por eso hemos construido **UniMovil**: una plataforma integral que une una aplicación móvil accesible y resiliente con un panel web administrativo de supervisión y trazabilidad en tiempo real."*

---

## 📽️ Diapositiva 2 (0:45 – 1:30) — Arquitectura Monorepo y Contratos Canónicos

### Contenido visual:
* Diagrama de arquitectura por capas desacopladas:
  * `@unimovil/contracts`: Modelos canónicos estrictamente tipados (`Place`, `Route`, `Transit`, `Incident`, `AuditEntry`).
  * `apps/mobile`: React Native + Expo Router + MapLibre.
  * `apps/admin`: React 19 + TypeScript + Vite.
  * `apps/api`: NestJS + TypeScript.

### Guión del ponente:
> *"Para garantizar que un equipo de 5 desarrolladores pudiera avanzar en paralelo sin bloqueos ni colisiones en Git, adoptamos una arquitectura monorepo desacoplada basada en contratos canónicos.  
> En `@unimovil/contracts` definimos los modelos de datos compartidos con compilación estricta en TypeScript. Esto asegura que la aplicación móvil, el servidor backend y el panel web administrativo hablen exactamente el mismo lenguaje tipado. Si una propiedad cambia en un contrato, el compilador nos avisa en tiempo de construcción antes de que ningún error llegue a producción."*

---

## 📽️ Diapositiva 3 (1:30 – 2:30) — Incremento Técnico Acumulado (Sprints 1 a 4)

### Contenido visual:
* Línea temporal de los 4 Sprints:
  * **Sprint 1:** Motor cartográfico MapLibre, catálogo geográfico y buscador tolerante a diacríticos (`HU-013`).
  * **Sprint 2:** Enrutamiento peatonal con Dijkstra, filtro estricto de accesibilidad PMR y panel web admin con trazabilidad inmutable (`HU-020`, `HU-070`, `HU-097`).
  * **Sprint 3:** Movilidad multimodal EMT (Líneas G y F con tiempos por Haversine), reporte móvil y moderación web de incidencias (`HU-022`, `HU-054`, `HU-055`).
  * **Sprint 4:** Modo sin conexión resiliente con caché LRU (`HU-094`), accesibilidad universal WCAG 2.1 AA (`HU-095`) y difusión administrativa de avisos urgentes (`HU-057`).

### Guión del ponente:
> *"A lo largo de los cuatro Sprints hemos construido un incremento funcional continuo y medible:  
> En el Sprint 1 digitalizamos el campus y su catálogo con normalización lingüística.  
> En el Sprint 2 implementamos el motor de rutas peatonales con Dijkstra y un filtro estricto de accesibilidad que garantiza itinerarios sin barreras arquitectónicas para sillas de ruedas.  
> En el Sprint 3 conectamos la red de autobuses de la EMT, comparando en segundos la caminata frente al bus G o F, y creamos el flujo de reporte y moderación de incidencias.  
> Y en el Sprint 4 dotamos a la app de modo sin conexión ante pérdidas de cobertura y certificamos la accesibilidad WCAG 2.1 AA, sumando el módulo de avisos urgentes en la web de administración."*

---

## 📽️ Diapositiva 4 (2:30 – 3:45) — Demostración Técnica en Vivo (75 Segundos)

### Secuencia de la Demo en Vivo:
1. **Paso 1 (Móvil — 25 seg):**
   * Abrir la app móvil en Ciudad Universitaria.
   * Buscar *"medicina"* (sin tilde). Mostrar cómo el buscador tolera errores diacríticos.
   * Seleccionar ruta accesible: el motor traza el recorrido en verde evitando las escaleras del Paraninfo.
   * Abrir la comparativa multimodal: muestra *"🚶 A pie (14 min)"* vs. *"🚌 Bus G (6 min)"*.
2. **Paso 2 (Web Admin — 25 seg):**
   * Cambiar a la pantalla del **Panel Web Admin** (`http://localhost:5173/`).
   * Pestaña **Incidencias**: Abrir la incidencia de la rampa de Farmacia, cambiar estado a *"En Proceso"*, reasignar a *"Mantenimiento UCM"* y añadir nota técnica.
   * Pestaña **Avisos**: Publicar una alerta urgente sobre el corte del túnel de Medicina por obras.
3. **Paso 3 (Trazabilidad Inmutable — 25 seg):**
   * Cambiar a la pestaña **Trazabilidad y Auditoría**.
   * Mostrar cómo ambas acciones acaban de registrarse al instante en el log inmutable con el chip de fecha/hora estilizado, diff de estados y ofuscación de credenciales activada.
   * Demostrar la expansión de historial anterior en ventana con desplazamiento interno.

### Guión del ponente:
> *"Pasamos a la demostración en vivo. En la app móvil seleccionamos como origen Metro Ciudad Universitaria y destino Medicina. Si activamos el filtro PMR, el algoritmo recalcula la trayectoria por la rampa exterior. Al abrir el comparador multimodal, la app calcula matemáticamente el tiempo a pie frente a la Línea G de la EMT.  
> Simultáneamente, en nuestro panel web de administración, el gestor del campus puede supervisar el estado de las instalaciones. Si un técnico atiende una incidencia o publicamos un aviso urgente sobre obras en un vial, el cambio se aplica de inmediato y queda registrado en el log inmutable de trazabilidad con estricta protección de datos personales."*

---

## 📽️ Diapositiva 5 (3:45 – 4:30) — Estrategia de Pruebas y Calidad (Tema 3)

### Contenido visual:
* Tabla de cobertura y métricas de testing:
  * **246 pruebas automatizadas superadas** (181 Vitest monorepo + 65 Jest/RTL móvil).
  * Cobertura de código superior al **96% en líneas** y al **92% en ramas lógicas**.
  * Pruebas de Caja Negra (Particiones de equivalencia y valores límite en filtros y transiciones).
  * Pruebas de Caja Blanca (Cobertura de caminos independientes en Dijkstra y autómata de estados).
  * Tres Reglas de TDD de Uncle Bob (Rojo-Verde-Refactorización).
  * 0 advertencias de ESLint (`--max-warnings=0`) y 0 errores de TypeScript (`tsc -b`).

### Guión del ponente:
> *"Siguiendo las directrices del Tema 3 impartidas por los profesores Antonio Navarro y Gonzalo Méndez, la calidad no ha sido un añadido final sino un pilar metodológico.  
> Aplicamos las tres reglas de TDD de Uncle Bob: ninguna línea de lógica se escribió sin un test previo en rojo.  
> Diseñamos casos de prueba de Caja Negra analizando particiones equivalentes y valores frontera en búsquedas y coordenadas, y pruebas de Caja Blanca garantizando la cobertura de caminos independientes en el cálculo de rutas y en la máquina de estados.  
> Cerramos el proyecto con 246 pruebas automáticas superadas en verde y cero advertencias de linter."*

---

## 📽️ Diapositiva 6 (4:30 – 5:00) — Conclusiones y Cierre

### Contenido visual:
* Matriz de Riesgos de Barry Boehm (RSGR) cerrada con 10/10 riesgos mitigados.
* Resumen de fortalezas:
  * Sistema usable, accesible (WCAG 2.1 AA) y verificado.
  * Arquitectura monorepo lista para escalabilidad institucional en la UCM.
* Ruegos y preguntas.

### Guión del ponente:
> *"En conclusión: UniMovil demuestra que es posible aplicar la disciplina de la ingeniería del software (Scrum puro, gestión del riesgo de Barry Boehm y pruebas rigurosas) para resolver un problema cotidiano real de nuestra universidad con una solución accesible para todos.  
> Quedamos a su entera disposición para cualquier pregunta o demostración adicional. Muchas gracias."*
