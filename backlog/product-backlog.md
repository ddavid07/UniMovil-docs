# Product Backlog de UniMovil

Este índice enlaza las historias existentes y conserva su prioridad funcional. La columna de Sprint muestra una secuencia candidata para los seis incrementos propuestos en iterations; no indica estado implementado, orden definitivo ni compromiso. El Product Owner y los Developers refinarán, ordenarán y seleccionarán trabajo según valor, dependencias, riesgo y capacidad en cada Sprint Planning.

**Estado de planificación:** propuestas de Sprint 1–6; selección, orden detallado, estimaciones, capacidad y estado de implementación pendientes de confirmar. Una PR no marca una historia como terminada.

Las descripciones completas y los criterios de aceptación están en el [catálogo de historias](../requirements/user-stories/README.md). Actualiza las prioridades aquí y en la historia cuando el equipo acuerde un cambio.

## Propuesta de alcance candidato para Sprint 1

El Sprint Goal propuesto es que una persona pueda explorar el mapa de Moncloa, localizar lugares mediante búsqueda o categoría y seleccionar uno para consultar una ficha básica. El equipo debe confirmarlo en Sprint Planning. La propuesta de alcance y dependencias está en el [plan de Sprint 1](../iterations/sprint-01/README.md).

Candidatas relacionadas, pendientes de selección definitiva en Sprint Planning según capacidad real:

1. [HU-010 — Consultar el mapa del campus](../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-010--consultar-el-mapa-del-campus).
2. [HU-012 — Filtrar categorías del mapa](../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-012--filtrar-categorías-del-mapa).
3. [HU-013 — Buscar lugares](../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-013--buscar-lugares).
4. Un corte de [HU-014 — Consultar la ficha de un lugar](../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-014--consultar-la-ficha-de-un-lugar) limitado a mostrar información básica verificada al seleccionar un punto; no implica terminar la historia completa.

Parte de la implementación de este alcance está propuesta en la [PR #23 del repositorio principal](https://github.com/ddavid07/UniMovil/pull/23). No se marcan las historias padre como terminadas ni se asignan estimaciones o compromisos individuales. La Definition of Done de cada historia sigue siendo obligatoria para marcarla terminada.

## Prioridad funcional Alta

| Historia | Prioridad registrada | Sprint candidato (propuesta; no compromiso) |
| --- | --- | --- |
| [HU-001 — Consultar información pública sin registrarse](../requirements/user-stories/01-acceso-y-cuentas.md) | Alta | Sprint 1 (regla transversal) |
| [HU-002 — Crear una cuenta](../requirements/user-stories/01-acceso-y-cuentas.md) | Alta | Sprint 5 (candidata) |
| [HU-003 — Iniciar y cerrar sesión](../requirements/user-stories/01-acceso-y-cuentas.md) | Alta | Sprint 5 (candidata) |
| [HU-004 — Recuperar el acceso a la cuenta](../requirements/user-stories/01-acceso-y-cuentas.md) | Alta | Sprint 5 (candidata) |
| [HU-007 — Gestionar permisos del dispositivo](../requirements/user-stories/01-acceso-y-cuentas.md) | Alta | Sprint 5 (refinar) |
| [HU-010 — Consultar el mapa del campus](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Alta | Sprint 1 (candidata) |
| [HU-011 — Mostrar la ubicación actual](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Alta | Sin Sprint propuesto |
| [HU-012 — Filtrar categorías del mapa](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Alta | Sprint 1 (candidata) |
| [HU-013 — Buscar lugares](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Alta | Sprint 1 (candidata) |
| [HU-014 — Consultar la ficha de un lugar](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Alta | Sprint 1 (corte básico) |
| [HU-016 — Consultar cierres y restricciones en el mapa](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Alta | Sin Sprint propuesto |
| [HU-020 — Introducir origen y destino](../requirements/user-stories/03-rutas-y-transporte.md) | Alta | Sprint 2 (candidata) |
| [HU-021 — Consultar una ruta a pie](../requirements/user-stories/03-rutas-y-transporte.md) | Alta | Sprint 2 (candidata) |
| [HU-022 — Consultar rutas con diferentes medios](../requirements/user-stories/03-rutas-y-transporte.md) | Alta | Sprint 3 (candidata) |
| [HU-023 — Consultar indicaciones paso a paso](../requirements/user-stories/03-rutas-y-transporte.md) | Alta | Sprint 2 (candidata) |
| [HU-024 — Consultar una ruta accesible](../requirements/user-stories/03-rutas-y-transporte.md) | Alta | Sprint 2 (candidata) |
| [HU-026 — Consultar una línea de autobús](../requirements/user-stories/03-rutas-y-transporte.md) | Alta | Sprint 3 (candidata) |
| [HU-027 — Consultar una parada](../requirements/user-stories/03-rutas-y-transporte.md) | Alta | Sprint 3 (candidata) |
| [HU-040 — Configurar preferencias de accesibilidad](../requirements/user-stories/04-accesibilidad-y-recursos.md) | Alta | Sprint 2 (refinar) |
| [HU-041 — Consultar accesos y servicios adaptados](../requirements/user-stories/04-accesibilidad-y-recursos.md) | Alta | Sprint 2 (refinar) |
| [HU-050 — Comunicar una incidencia](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Alta | Sprint 6 (candidata) |
| [HU-052 — Consultar mis incidencias](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Alta | Sprint 6 (candidata) |
| [HU-054 — Gestionar una incidencia](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Alta | Sprint 6 (candidata) |
| [HU-055 — Actualizar el estado de una incidencia](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Alta | Sprint 6 (candidata) |
| [HU-057 — Publicar un aviso](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Alta | Sin Sprint propuesto |
| [HU-058 — Consultar avisos](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Alta | Sin Sprint propuesto |
| [HU-059 — Administrar un aviso](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Alta | Sin Sprint propuesto |
| [HU-064 — Recibir una notificación relevante](../requirements/user-stories/06-personalizacion-y-notificaciones.md) | Alta | Sprint 6 (opcional) |
| [HU-070 — Gestionar edificios y lugares](../requirements/user-stories/07-administracion-y-datos.md) | Alta | Sin Sprint propuesto |
| [HU-071 — Gestionar puntos y categorías](../requirements/user-stories/07-administracion-y-datos.md) | Alta | Sin Sprint propuesto |
| [HU-072 — Gestionar transporte y paradas](../requirements/user-stories/07-administracion-y-datos.md) | Alta | Sin Sprint propuesto |
| [HU-073 — Gestionar accesibilidad](../requirements/user-stories/07-administracion-y-datos.md) | Alta | Sin Sprint propuesto |
| [HU-075 — Consultar el estado de los datos](../requirements/user-stories/07-administracion-y-datos.md) | Alta | Sin Sprint propuesto |
| [HU-076 — Gestionar usuarios y roles](../requirements/user-stories/07-administracion-y-datos.md) | Alta | Sprint 5 (refinar) |
| [HU-080 — Gestionar fuentes con errores](../requirements/user-stories/07-administracion-y-datos.md) | Alta | Sin Sprint propuesto |
| [HU-090 — Proteger los datos de la cuenta](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Alta | Sprint 5 (candidata) |
| [HU-091 — Controlar el acceso a funcionalidades](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Alta | Sprint 5 (candidata) |
| [HU-092 — Gestionar privacidad y consentimiento](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Alta | Sprint 5 (candidata) |
| [HU-094 — Gestionar errores y falta de conexión](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Alta | Sprint 4 (candidata) |
| [HU-095 — Utilizar una interfaz accesible](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Alta | Sprint 4 (candidata) |

## Prioridad funcional Media

| Historia | Prioridad registrada | Sprint candidato (propuesta; no compromiso) |
| --- | --- | --- |
| [HU-005 — Gestionar los datos del perfil](../requirements/user-stories/01-acceso-y-cuentas.md) | Media | Sin Sprint propuesto |
| [HU-006 — Eliminar una cuenta](../requirements/user-stories/01-acceso-y-cuentas.md) | Media | Sin Sprint propuesto |
| [HU-015 — Consultar servicios cercanos](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Media | Sin Sprint propuesto |
| [HU-017 — Compartir un lugar o una ubicación](../requirements/user-stories/02-mapa-busqueda-y-lugares.md) | Media | Sin Sprint propuesto |
| [HU-025 — Comparar y ajustar alternativas](../requirements/user-stories/03-rutas-y-transporte.md) | Media | Sin Sprint propuesto |
| [HU-028 — Consultar información en tiempo real](../requirements/user-stories/03-rutas-y-transporte.md) | Media | Sin Sprint propuesto |
| [HU-029 — Guardar y consultar rutas recientes](../requirements/user-stories/03-rutas-y-transporte.md) | Media | Sin Sprint propuesto |
| [HU-042 — Consultar aparcamientos](../requirements/user-stories/04-accesibilidad-y-recursos.md) | Media | Sin Sprint propuesto |
| [HU-043 — Consultar recursos para bicicletas y patinetes](../requirements/user-stories/04-accesibilidad-y-recursos.md) | Media | Sin Sprint propuesto |
| [HU-045 — Consultar recursos cercanos por categoría](../requirements/user-stories/04-accesibilidad-y-recursos.md) | Media | Sin Sprint propuesto |
| [HU-051 — Adjuntar evidencias a una incidencia](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Media | Sin Sprint propuesto |
| [HU-053 — Consultar incidencias públicas](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Media | Sprint 6 (candidata) |
| [HU-056 — Confirmar o reabrir una incidencia](../requirements/user-stories/05-incidencias-y-comunicaciones.md) | Media | Sin Sprint propuesto |
| [HU-060 — Guardar favoritos](../requirements/user-stories/06-personalizacion-y-notificaciones.md) | Media | Sin Sprint propuesto |
| [HU-061 — Consultar búsquedas y rutas recientes](../requirements/user-stories/06-personalizacion-y-notificaciones.md) | Media | Sin Sprint propuesto |
| [HU-062 — Configurar preferencias de movilidad](../requirements/user-stories/06-personalizacion-y-notificaciones.md) | Media | Sin Sprint propuesto |
| [HU-063 — Configurar notificaciones](../requirements/user-stories/06-personalizacion-y-notificaciones.md) | Media | Sprint 6 (opcional) |
| [HU-066 — Compartir una ruta](../requirements/user-stories/06-personalizacion-y-notificaciones.md) | Media | Sin Sprint propuesto |
| [HU-074 — Importar datos externos](../requirements/user-stories/07-administracion-y-datos.md) | Media | Sin Sprint propuesto |
| [HU-077 — Consultar auditoría administrativa](../requirements/user-stories/07-administracion-y-datos.md) | Media | Sin Sprint propuesto |
| [HU-078 — Consultar estadísticas de uso](../requirements/user-stories/07-administracion-y-datos.md) | Media | Sin Sprint propuesto |
| [HU-093 — Acceder a los datos personales](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Media | Sprint 5 (refinar) |
| [HU-096 — Consultar ayuda y soporte](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Media | Sin Sprint propuesto |
| [HU-097 — Mantener trazabilidad de los cambios relevantes](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Media | Sin Sprint propuesto |

## Prioridad funcional Baja

| Historia | Prioridad registrada | Sprint candidato (propuesta; no compromiso) |
| --- | --- | --- |
| [HU-044 — Consultar puntos de carga y mantenimiento](../requirements/user-stories/04-accesibilidad-y-recursos.md) | Baja | Sin Sprint propuesto |
| [HU-065 — Cambiar idioma y preferencias de presentación](../requirements/user-stories/06-personalizacion-y-notificaciones.md) | Baja | Sin Sprint propuesto |
| [HU-079 — Exportar información e informes](../requirements/user-stories/07-administracion-y-datos.md) | Baja | Sin Sprint propuesto |
| [HU-098 — Recibir actualizaciones de la aplicación](../requirements/user-stories/08-seguridad-privacidad-y-calidad.md) | Baja | Sin Sprint propuesto |

## Criterio para ordenar el trabajo

La etiqueta funcional orienta, pero no sustituye la ordenación del Product Backlog. En el refinamiento, considerar valor para usuarios, riesgo, dependencias, aprendizaje esperado y claridad. Registrar la decisión de orden y mantener las historias completas en sus documentos originales.
