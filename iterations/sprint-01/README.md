# Sprint 1 — Explorar el campus

## 1. Estado y fuente de información

- **Estado:** implementación propuesta en la [PR #23 del repo de código](https://github.com/ddavid07/UniMovil/pull/23); sigue abierta y no está aceptada en `main`.
- **Registro:** plan preparado. No constan fecha de Planning, duración acordada, capacidad ni selección final.
- **Estimaciones/responsables:** pendientes de acordar por el equipo.

## 2. Sprint Goal

> Como estudiante o visitante, quiero explorar el campus de Moncloa, encontrar lugares por nombre o categoría y abrir una ficha básica, para orientarme sin conocer previamente el campus.

## 3. Historias candidatas y criterios de aceptación

| Historia candidata | Resultado de valor | Criterio observable y evidencia |
| --- | --- | --- |
| [HU-001 — Consultar información pública sin registrarse](../../requirements/user-stories/01-acceso-y-cuentas.md#hu-001--consultar-información-pública-sin-registrarse) | Consultar mapa y lugares sin crear cuenta. | El recorrido público no solicita inicio de sesión. |
| [HU-010 — Consultar el mapa](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-010--consultar-el-mapa-del-campus) | Explorar el mapa del campus en móvil. | Desplazamiento/zoom, estados de carga/error y atribución visibles; comprobar plataformas acordadas. |
| [HU-012 — Filtrar categorías](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-012--filtrar-categorías-del-mapa) | Reducir lugares por categoría. | Filtro y restablecimiento mantienen resultados coherentes en mapa/lista. |
| [HU-013 — Buscar lugares](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-013--buscar-lugares) | Encontrar un lugar por nombre. | Resultados identificables, selección centrada y estado vacío comprensible. |
| Corte de [HU-014 — Consultar una ficha](../../requirements/user-stories/02-mapa-busqueda-y-lugares.md#hu-014--consultar-la-ficha-de-un-lugar) | Consultar datos básicos del punto seleccionado. | Nombre, categoría y ubicación; datos desconocidos no se presentan como confirmados. No completa la historia entera. |

HU-011 (ubicación actual) queda fuera de este corte; requiere revisar permisos y privacidad.

## 4. Plan inicial y dependencias

1. Confirmar compatibilidad de MapLibre con Expo y la carga/atribución del proveedor.
2. Mantener catálogo de solo lectura con fuente, fecha y licencia por entrada; datos OSM no acreditan accesibilidad ni inspección de campo.
3. Integrar mapa, búsqueda, filtros, lista y ficha como un recorrido coherente.
4. Ejecutar pruebas de dominio/UI y comprobaciones nativas disponibles; registrar plataforma, commit y resultado.
5. Mantener el código candidato en PR hasta cumplir DoD e integrarlo.

La propuesta usa 24 lugares consultados en OpenStreetMap. La clave pública del proveedor debe estar restringida; nunca guardar claves de servicio en Git.

## 5. Riesgos — RSGR

| Riesgo | Probabilidad / consecuencia / prioridad inicial | Reducción y seguimiento | Contingencia |
| --- | --- | --- | --- |
| Incompatibilidad MapLibre/Expo → no hay mapa demostrable | Ocasional / Crítica / Alta | Spike temprano; validar Android/iOS, estilo y atribución. | Reducir alcance a lo demostrable y registrar decisión antes de cambiar proveedor/SDK. |
| Clave/proveedor o red → validación live falla | Probable / Seria / Alta | Clave pública restringida; observar job live y cuotas; fixtures no sustituyen validación real. | Bloquear aceptación live hasta corregir proveedor/configuración. |
| Datos OSM incompletos → orientación engañosa | Ocasional / Seria / Media | Procedencia/licencia por entrada; no afirmar horarios o accesibilidad no verificados. | Etiquetar u ocultar datos dudosos y priorizar verificación. |

## 6. Verificación y Definition of Done

- Caja negra: búsqueda vacía, coincidencias, filtros y límites del catálogo.
- Integración: seleccionar lugar en lista/mapa y abrir su ficha.
- Pruebas nativas en entornos disponibles; registrar plataforma, commit y resultado.
- Atribución/licencia verificables; errores de proveedor visibles; sin secretos.
- Done solo al integrar el cambio y pasar las comprobaciones aplicables.

La PR #23 informa que siguen pendientes validación real del proveedor y mediciones nativas; métricas de rama no equivalen a aceptación del Sprint.

## 7. Sprint Review y retrospectiva

Pendientes de evidencia de evento y feedback. La [agenda de Sprint Planning 1](../../meetings/sprint-01-planning-agenda.md) no es acta; el [plan de validación](../../validation/sprint-01-validation-plan.md) describe pruebas, no resultados.

## 8. Trabajo no terminado y siguiente paso

Confirmar Sprint Planning, capacidad y DoD; completar validaciones de PR #23. Las historias no terminadas vuelven al Product Backlog para reordenación.
