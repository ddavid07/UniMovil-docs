# Sprint 6 — Seguir incidencias y comunicar cambios

## 1. Estado y fuente de información

- **Estado:** propuesta de planificación, no acordada todavía.
- **Dependencias:** identidad/autorización de Sprint 5 para funciones privadas y roles de gestión; mapa/rutas/transporte para referenciar ubicaciones.
- No se asignan fechas, puntos, capacidad ni responsables. Este Sprint no implica que todo el Product Backlog quede terminado.

## 2. Sprint Goal

> Como usuario, quiero comunicar y seguir una incidencia de movilidad y recibir información relevante de su estado, mientras los gestores la revisan, para que los cambios del campus tengan un ciclo de seguimiento comprensible.

## 3. Historias candidatas y criterios de aceptación

| Historia candidata | Resultado de valor | Criterio observable y evidencia |
| --- | --- | --- |
| [HU-050 — Comunicar incidencia](../../requirements/user-stories/05-incidencias-y-comunicaciones.md#hu-050--comunicar-una-incidencia) | Enviar problema con ubicación/categoría. | Validación, identificador, confirmación y estado inicial; requiere cuenta. |
| [HU-052 — Consultar mis incidencias](../../requirements/user-stories/05-incidencias-y-comunicaciones.md#hu-052--consultar-mis-incidencias) | Seguir incidencias propias. | Aislamiento por cuenta, estados y estado vacío. |
| [HU-053 — Consultar incidencias públicas](../../requirements/user-stories/05-incidencias-y-comunicaciones.md#hu-053--consultar-incidencias-públicas) | Consultar incidencias autorizadas. | Moderación, anonimización, fecha/estado y retirada de resueltas. |
| [HU-054/055 — Gestionar y actualizar](../../requirements/user-stories/05-incidencias-y-comunicaciones.md#hu-054--gestionar-una-incidencia) | Gestor revisa y cambia el estado. | Solo rol permitido; transiciones válidas, historial y respuesta visible. |
| [HU-063/064 — Preferencias/notificaciones](../../requirements/user-stories/06-personalizacion-y-notificaciones.md#hu-063--configurar-notificaciones) | Elegir notificaciones y recibir cambios relevantes. | Consentimiento, preferencias, evento válido y desactivación. Candidata opcional si capacidad/proveedor no están listos. |

HU-051 (fotos) queda fuera hasta definir tamaño, almacenamiento y moderación. HU-056/avisos HU-057–059 se refinan después; no se asumen dentro.

## 4. Plan inicial y dependencias

1. Acordar estados/transiciones y permisos de usuario/gestor.
2. Definir qué contenido se publica y cómo se separa de los datos privados.
3. Construir un corte vertical desde envío hasta estado/respuesta visible.
4. Añadir push solo si proveedor, consentimiento, eventos y opt-out están definidos.
5. Validar extremo a extremo con datos sintéticos y enlazar evidencias.

Selección final según capacidad; dividir historias que no quepan.

## 5. Riesgos — RSGR

| Riesgo | Probabilidad / consecuencia / prioridad inicial | Reducción y seguimiento | Contingencia |
| --- | --- | --- | --- |
| Incidencia expone ubicación/datos de autor | Ocasional / Crítica / Alta | Minimizar datos, separar vistas, probar permisos y anonimización. | Retirar publicación, corregir permisos y revisar registros. |
| Moderación/transiciones incorrectas | Ocasional / Seria / Media | Máquina de estados, pruebas por rol, historial auditable. | Volver a estado seguro y registrar corrección. |
| Notificaciones duplicadas/no deseadas | Ocasional / Seria / Media | Idempotencia, preferencias, opt-out y pruebas antes de enviar. | Desactivar canal y mantener avisos dentro de la app. |
| Proveedor push falla | Ocasional / Seria / Media | Prototipo y monitorización de configuración/entrega. | Mantener bandeja interna o posponer push. |

## 6. Verificación y Definition of Done

- Caja negra: campos incompletos, ubicación fuera de ámbito, acceso usuario/gestor, incidencia propia/ajena y transiciones inválidas.
- Integración por caso de uso: envío → persistencia → moderación → estado/respuesta → consulta.
- Seguridad/privacidad: autorización del servidor, identidad oculta públicamente, logs sin secretos.
- Regresión de mapa/rutas; pruebas de duplicado/rechazo/revocación si se seleccionan notificaciones.
- Evidencia ligada a historia y commit integrado; reportar entorno y límites.

## 7. Sprint Review y retrospectiva

Pendientes. Inspeccionar el flujo con datos sintéticos; registrar feedback real y una mejora de proceso.

## 8. Trabajo no terminado y siguiente paso

Reordenar HU-051/056, avisos HU-057–059, gestión de datos HU-070–080 y calidad HU-096–098. Tras Sprint 6 se puede planificar otro incremento si el Product Goal/backlog lo requiere.
