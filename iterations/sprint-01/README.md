# Sprint 1 — Mapa interactivo del campus

## Estado de este registro

**Implementación técnica en revisión; incremento todavía no aceptado.** El objetivo y el alcance de implementación se han concretado y existe una propuesta de código en la [PR #23 de UniMovil](https://github.com/ddavid07/UniMovil/pull/23). El equipo todavía debe confirmar capacidad, fechas, responsabilidades y su Sprint Planning. Este registro no acredita reuniones ni resultados que no hayan ocurrido.

## Sprint Goal

> Como persona que se desplaza por el campus de Moncloa, quiero explorar un mapa interactivo, encontrar lugares por nombre o categoría y seleccionar un lugar para consultar una ficha básica, para orientarme sin recorrer el campus a ciegas.

El resultado esperado es un primer recorrido móvil coherente: abrir el mapa del campus, desplazarse y acercarse, buscar o filtrar lugares, seleccionar uno y ver su ubicación y datos básicos. El Sprint prioriza comportamiento funcional. No incluye establecer un sistema visual definitivo.

## Periodo y equipo

- **Duración objetivo:** tres semanas, como duración propuesta para este primer Sprint.
- **Inicio y cierre:** pendientes de acordar con el equipo y de encajar con el calendario de la asignatura.
- **Product Owner, Scrum Master y Developers:** responsabilidades y personas pendientes de acordar en la Sprint Planning.
- **Capacidad y disponibilidad:** pendientes de concretar por los Developers.
- **Estimaciones:** no asignadas. El equipo estimará o dimensionará el trabajo durante la planificación; no se presupone velocidad previa.

El Sprint se inicia con su Sprint Planning, en la que el equipo confirma el Sprint Backlog. Si la duración de tres semanas no encaja con el calendario real, el equipo acordará una duración fija alternativa de un mes como máximo antes de empezar.

## Contexto técnico conocido

El estado inspeccionado en el repositorio principal es una pantalla móvil inicial, sin integración de mapas ni API de lugares. La API contiene actualmente un endpoint de salud. La decisión técnica vigente está en [ADR-0003 del repositorio principal](https://github.com/ddavid07/UniMovil/blob/main/docs/fundamentos/adr/0003-servicios-de-mapas-y-rutas.md): MapLibre React Native como renderizador, MapTiler Cloud como proveedor inicial de mapa base, OpenStreetMap como fuente geográfica cuando corresponda y datos propios del campus bajo control de UniMovil.

La instalación y configuración de MapLibre con la versión Expo existente debe comprobarse antes de comprometer el resto del trabajo. No se actualizará Expo ni se cambiará de proveedor por conveniencia sin revisar compatibilidad, consecuencias y la decisión técnica existente. La clave/configuración del proveedor no se guardará en Git y el mapa mostrará la atribución necesaria.

## Sprint Backlog propuesto

La selección se basa en las historias de prioridad Alta relacionadas con el objetivo. El equipo puede ajustar alcance durante Sprint Planning sin perder el Sprint Goal.

| Orden inicial | Elemento | Resultado esperado para este Sprint | Criterios verificables del Sprint |
| --- | --- | --- | --- |
| 1 | Spike de viabilidad MapLibre + Expo, ligado a HU-010 | Confirmar una configuración mínima que renderice el mapa en las plataformas objetivo y documentar límites o bloqueos. | La app móvil compila y abre el mapa en los entornos que el equipo acuerde soportar; la fuente de estilo/capas carga; la atribución se ve; se documenta el procedimiento de configuración sin publicar secretos. |
| 2 | HU-010 — [Consultar el mapa del campus](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-010--consultar-el-mapa-del-campus) | Mapa base interactivo del campus de Moncloa con sus límites/elementos principales, contenido geográfico disponible y marcadores comprensibles. | Muestra los límites y elementos principales del campus; permite desplazar y acercar/alejar el mapa; se adapta a pantalla móvil; presenta lugares con símbolos comprensibles; muestra estado de carga/error cuando no se obtienen teselas o datos; mantiene atribución y condiciones del proveedor. |
| 3 | HU-012 — [Filtrar categorías del mapa](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-012--filtrar-categorías-del-mapa) | Filtrar marcadores sin reiniciar la pantalla y restablecer el filtro. | El filtro se aplica a los lugares cargados; el mapa y la lista mantienen resultados coherentes; existe forma de restablecerlo; los símbolos/categorías mostrados se entienden. Las categorías de HU-012 que no cuenten con datos verificados no se presentarán como implementadas; si el alcance completo no cabe, se dividirá/refinará la historia y no se declarará HU-012 terminada. |
| 4 | HU-013 — [Buscar lugares](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-013--buscar-lugares) | Buscar un lugar del campus y localizarlo desde el mapa. | Búsqueda por nombre y categoría en el conjunto disponible; sugerencias cuando haya coincidencias; el resultado identifica nombre y categoría; seleccionar un resultado centra o destaca su marcador; la búsqueda vacía muestra un mensaje recuperable. La distancia solo se mostrará si se puede calcular de forma fiable. |
| 5 | Corte vertical de HU-014 — [Consultar la ficha de un lugar](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-014--consultar-la-ficha-de-un-lugar) | Al seleccionar un marcador, consultar una ficha breve con nombre, categoría, ubicación y descripción o accesibilidad solo cuando el dato esté verificado. | La ficha corresponde al marcador seleccionado y distingue los datos no disponibles. Este corte **no** completa HU-014: horarios, contactos, enlaces oficiales, rutas y favoritos quedan fuera salvo que el equipo los añada expresamente al alcance y cumplan su criterio de terminado. |
| 6 | Integración y validación | Un incremento integrado que permita demostrar el recorrido del Sprint Goal. | Cambios integrados mediante PR revisada; comprobaciones aplicables pasan; se verifican dispositivos/tamaños acordados; pruebas y limitaciones se registran en el plan de validación enlazado abajo. |

### Decisión de datos para el primer incremento

La base de lugares debe ser pequeña, de solo lectura y suficiente para demostrar las historias. Cada lugar que se incluya tendrá nombre, categoría, coordenadas y fuente/procedencia verificable; no se inventarán direcciones, accesos o características. La estrategia concreta de provisión de estos datos debe confirmarse en Sprint Planning, porque `main` aún no contiene API de lugares ni persistencia para ellos.

**Alcance confirmado para la implementación:** catálogo local de solo lectura detrás de una interfaz sustituible por la API. El conjunto inicial incluye 24 lugares consultados en OpenStreetMap, cuatro por cada una de las seis categorías, con fuente, fecha de consulta y licencia ODbL por registro. Incluye recursos del entorno compartido de Ciudad Universitaria. La consulta de la fuente no equivale a una inspección de campo ni acredita apertura o accesibilidad actual. API y base de datos no se incorporan en este incremento; la arquitectura final aprobada se mantiene.

## Condiciones de implementación y revisión

- Android e iOS se comprobarán con este equipo y runners de GitHub; no se presuponen dispositivos físicos ni un Mac local.
- La calidad es condición de aceptación. Si queda trabajo al terminar las tres semanas, se registra y reordena; el Sprint no se prolonga para aparentar que todo se terminó.
- Se permite una actualización estable coordinada del SDK cuando sea necesaria y verificable. No se fuerzan downgrades o exclusiones para ocultar vulnerabilidades.
- La implementación está aislada en `feature/sprint-01-campus`, mediante PR en borrador. No modifica funcionalmente la API ni el panel y no integra ramas de features abiertas.
- Existen controles de formato, lint sin advertencias, tipos estrictos, límites de tamaño/complejidad, catálogo, cobertura y builds. La aceptación también requiere pruebas nativas, proveedor real y presupuestos de rendimiento.
- Persisten bloqueos altos transitivos de `node-forge` y `braces` sin parche publicado. También falta configurar una clave pública restringida de MapTiler para la validación real. No se considera el incremento terminado ni se omiten checks.
- Evidencia y estado de ejecución: [validación del Sprint 1](../../validation/sprint-01-validation-plan.md).

## Plan inicial de trabajo

Este orden expresa dependencias, no asigna tareas a personas. Los Developers decidirán cómo repartirse el trabajo y adaptarán el plan cada día.

1. **Sprint Planning y preparación:** acordar equipo/responsabilidades, fechas, capacidad, DoD, dispositivo(s) de demostración y alcance de datos; refinar HU-010/012/013 y confirmar el corte de HU-014.
2. **Comprobación técnica temprana:** instalar una pantalla mínima de MapLibre en la versión Expo actual; confirmar Android/iOS, estilo MapTiler, atribución, configuración local y comportamiento sin red. Si falla, inspeccionar opciones sin actualizar dependencias a ciegas y registrar la decisión/impedimento.
3. **Datos y dominio mínimo:** elegir fuente(s) pública(s)/oficial(es), validar coordenadas y categorías, crear el conjunto semilla con procedencia y definir estados de datos ausentes.
4. **Mapa usable:** integrar el mapa base y controles de desplazamiento/zoom; añadir marcadores y estados de carga/error.
5. **Exploración de lugares:** implementar búsqueda, sugerencias, filtro de categorías, selección de resultado/marcador y ficha básica; mantener lista y mapa sincronizados.
6. **Integración continua:** abrir PR pequeñas revisables, ejecutar las validaciones del repositorio, resolver bloqueos y mantener este Sprint Backlog actualizado.
7. **Preparación de Review:** estabilizar el recorrido de demostración, guardar evidencias sin datos personales y presentar también las limitaciones conocidas.
8. **Sprint Review y Retrospective:** inspeccionar el incremento con interesados; registrar feedback y cambios acordados al Product Backlog; después acordar una mejora concreta del proceso.

No se planifican días/fechas para cada tarea ni reuniones con asistentes inventados. Los Developers decidirán el plan detallado y harán un Daily Scrum de hasta 15 minutos cada día laborable del Sprint, adaptando el trabajo para alcanzar el Sprint Goal.

## Fuera del Sprint

- Ubicación GPS real y solicitud de permisos (HU-011). La exploración manual del mapa seguirá disponible.
- Cálculo de rutas y navegación paso a paso (HU-021 y relacionadas).
- Inicio de sesión, favoritos persistentes y perfiles.
- Gestión administrativa, API/BD completa e importación automatizada de fuentes, salvo que la Sprint Planning sustituya trabajo de alcance equivalente.
- Cierres en tiempo real, incidencias y notificaciones.
- Definir una identidad visual completa, pulir animaciones o realizar prototipos visuales. Se priorizan funcionalidad, legibilidad y controles básicos accesibles.
- Considerar las PR abiertas como incremento entregado. Cualquier código candidato deberá integrarse, revisarse y satisfacer la Definition of Done antes de formar parte del incremento.

## Definition of Done para confirmar

La Definition of Done general de las historias está en [Historias de usuario](../../requirements/user-stories/README.md). Para este Sprint se propone concretarla así en Sprint Planning:

- El recorrido incluido funciona en los dispositivos/simuladores acordados y no depende de datos o coordenadas ficticios presentados como reales.
- El mapa, búsqueda, filtro, selección y ficha cumplen los criterios verificables del Sprint Backlog; existen estados de carga, error y cero resultados.
- Los datos tienen fuente verificable; la atribución y condiciones del proveedor de mapas son visibles y se respetan.
- La configuración sensible está fuera del repositorio; no se han añadido claves, secretos ni datos personales.
- El código está integrado en `main` tras revisión por PR, con formato, lint, typecheck, pruebas y build aplicables en verde. No se omiten checks ni se relajan controles para declarar el Sprint terminado.
- La documentación técnica que deba evolucionar junto al código se actualiza en UniMovil; este registro, el plan de validación y las evidencias se actualizan en UniMovil-docs.
- Se puede ejecutar la demostración acordada desde un entorno limpio siguiendo las instrucciones existentes.

El equipo debe confirmar esta propuesta. El incremento solo se considera terminado cuando satisface una Definition of Done verificable. El Sprint termina al concluir su duración fija, incluso si queda trabajo pendiente.

## Validación, Review y retrospectiva

- **Plan de pruebas:** [plan de validación del Sprint 1](../../validation/sprint-01-validation-plan.md).
- **Evidencias:** guardar capturas o notas de ejecución en `validation/` después de generarlas, sin datos personales.
- **Demostración propuesta:** abrir la app, explorar el mapa manualmente, buscar un lugar, filtrar una categoría, seleccionar su marcador y mostrar la ficha breve; después enseñar el estado de búsqueda vacía y cómo se informa un error de carga.
- **Material de presentación:** pendiente de crear cuando la fecha/contexto de la Review esté acordado. Una exposición de diapositivas sin inspección del incremento no sustituye la Sprint Review.
- **Feedback y acuerdos de Review:** pendientes; no hay resultados todavía.
- **Retrospective y acción de mejora:** pendientes; se completarán después de celebrar el evento.

## Riesgos, dependencias y decisiones pendientes

| Riesgo o decisión | Tratamiento previsto |
| --- | --- |
| Compatibilidad de MapLibre con el Expo/React Native actual | Resolver con spike al inicio. No ocultar fallos con actualización de SDK no planificada. |
| Acceso/configuración del proveedor de mapa | Confirmar configuración local, cuota y atribución antes de integrar. No commitear claves. |
| Datos fiables del campus y coordenadas | Recopilar y validar procedencia; no usar contenido generado como si fuese geografía real. |
| API de lugares inexistente en el estado actual | Confirmar si se usa semilla temporal sustituible o se amplía el Sprint a API/BD. Recalcular capacidad si cambia. |
| HU-012 y HU-014 abarcan más que la demo mínima | Refinar/dividir historias antes de cerrar el Sprint Backlog; no marcar la historia padre terminada si quedan criterios. |
| Capacidad, fechas y responsabilidades no confirmadas | Resolver en Sprint Planning antes de iniciar; no asignar responsables o fechas desde este documento. |
| La primera integración falla por proveedor/red | Incluir estado de error y forma de continuar la prueba con la configuración de desarrollo permitida; no simular éxito en la demo. |

### Acuerdos pendientes de la Sprint Planning

- [ ] Confirmar Product Goal que guía el Sprint y la prioridad final del objetivo.
- [ ] Confirmar duración fija y fechas de inicio/cierre.
- [ ] Acordar quién asume las responsabilidades Scrum y quiénes forman Developers.
- [ ] Confirmar capacidad/disponibilidad y seleccionar el Sprint Backlog definitivo.
- [ ] Confirmar dispositivos y plataformas de demostración.
- [x] Conjunto inicial: 24 elementos de OpenStreetMap, cuatro por cada una de las seis categorías, con procedencia explícita.
- [x] Alcance de implementación: catálogo local sustituible, sin API/BD en este incremento.
- [ ] Refinar/dividir HU-012 y el corte de HU-014; acordar cuándo se consideran terminadas.
- [ ] Acordar la Definition of Done específica.
- [ ] Confirmar fecha/contexto de Sprint Review y cómo se recogerá feedback.

## Seguimiento y cierre

Durante el Sprint, registrar aquí solo cambios relevantes al plan y al Sprint Goal. No es necesario transcribir cada Daily Scrum. Al final, actualizar el estado, el incremento realmente integrado, la evidencia, el feedback recibido, la retrospectiva y el trabajo no terminado. Los elementos que no cumplan la Definition of Done vuelven al Product Backlog para ser reordenados; no pasan automáticamente al siguiente Sprint.
