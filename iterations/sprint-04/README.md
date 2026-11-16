# Sprint 4 — Mejorar resiliencia y accesibilidad

## 1. Estado y fuente de información

- **Estado:** plan candidato; no hay aquí evidencia de entrega integrada y aceptada.
- La documentación previa declaraba offline/WCAG y métricas como completados mientras citaba una rama. Se tratan como objetivos pendientes de demostrar.

## 2. Sprint Goal

> Como persona que consulta UniMovil en el campus, quiero entender los errores y completar tareas esenciales con conectividad limitada y tecnologías de asistencia, para orientarme sin perder el trabajo introducido.

## 3. Historias candidatas y criterios de aceptación

| Historia candidata | Resultado de valor | Criterio observable y evidencia |
| --- | --- | --- |
| [HU-094 — Gestionar errores y falta de conexión](../../requirements/user-stories/08-seguridad-privacidad-y-calidad.md#hu-094--gestionar-errores-y-falta-de-conexión) | Entender fallos y recuperar trabajo. | Distingue causas, ofrece reintento y conserva entradas. Definir qué funciones/datos siguen disponibles offline. |
| [HU-095 — Utilizar una interfaz accesible](../../requirements/user-stories/08-seguridad-privacidad-y-calidad.md#hu-095--utilizar-una-interfaz-accesible) | Completar flujos esenciales con tecnologías de asistencia. | Etiquetas, contraste, no depender del color, texto ampliado/lector de pantalla y alternativa textual al mapa comprobados. |

“Cumple WCAG 2.1 AA” requiere definir alcance y evidencia de auditoría; no se deriva de atributos UI o conteo de tests.

## 4. Plan inicial y dependencias

- Elegir flujos integrados de Sprints 1–3; no cachear datos sensibles por defecto.
- Definir significado y límites de offline: catálogo/mapa/ruta, expiración y datos desactualizados.
- Confirmar detección real de conectividad y recuperación; no simular reconexión.
- Comprobar foco, TalkBack/VoiceOver, texto ampliado, contraste, targets y alternativa de mapa.
- Seleccionar alcance según capacidad real.

## 5. Riesgos — RSGR

| Riesgo | Probabilidad / consecuencia / prioridad inicial | Reducción y seguimiento | Contingencia |
| --- | --- | --- | --- |
| Caché desactualizada → ruta vieja parece vigente | Ocasional / Crítica / Alta | Fechas, expiración, estados offline y prueba de reconexión. | No mostrar rutas antiguas como actuales; limitar a datos estáticos etiquetados. |
| Accesibilidad incompleta → bloqueo de usuarios | Ocasional / Crítica / Alta | Auditoría por flujo, pruebas manuales con lector y registrar barreras. | Limitar declaración de conformidad y priorizar defectos críticos. |
| Plataforma/proveedor falla → evidencia incompleta | Ocasional / Seria / Media | Registrar entorno, runner, artefactos y fallos. | Marcar plataforma no validada; no declarar aceptación multiplataforma. |

## 6. Verificación y Definition of Done

- Recuperación: desconexión, timeout, reintento, reconexión y conservación de entradas.
- Caja negra: datos vacíos/antiguos, permisos rechazados y errores diferenciados.
- Accesibilidad: automatización más comprobación manual con lectores y texto ampliado; evidencia por flujo.
- Regresión de mapa/rutas y builds acordados.
- No afirmar “offline completo” ni WCAG AA sin alcance, criterio, resultado y evidencia fechada.

## 7. Sprint Review y retrospectiva

Pendientes. Inspeccionar flujos reales con y sin red y tecnologías de asistencia; registrar feedback y defectos.

## 8. Trabajo no terminado y siguiente paso

Definir persistencia/expiración antes de implementar offline. Reordenar defectos y limitaciones en el Product Backlog; Sprint 4 no es cierre final del proyecto.
