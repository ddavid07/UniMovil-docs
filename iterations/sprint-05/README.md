# Sprint 5 — Gestionar cuentas, privacidad y permisos

## 1. Estado y fuente de información

- **Estado:** propuesta de planificación, no acordada todavía.
- **Dependencia:** establecer identidad/autorización antes de operaciones privadas de incidencias y notificaciones.
- No se asignan fecha, duración, puntos, capacidad ni responsables.

## 2. Sprint Goal

> Como usuario de UniMovil, quiero crear y proteger mi cuenta, controlar permisos opcionales y saber quién puede realizar acciones administrativas, para usar funciones personales sin exponer mis datos.

## 3. Historias candidatas y criterios de aceptación

| Historia candidata | Resultado de valor | Criterio observable y evidencia |
| --- | --- | --- |
| [HU-002/003 — Crear cuenta y sesión](../../requirements/user-stories/01-acceso-y-cuentas.md#hu-002--crear-una-cuenta) | Crear cuenta y entrar/salir de forma segura. | Validar entradas, sesión y errores sin filtrar credenciales. |
| [HU-004 — Recuperar acceso](../../requirements/user-stories/01-acceso-y-cuentas.md#hu-004--recuperar-el-acceso-a-la-cuenta) | Recuperar acceso con flujo verificable. | Enlace/token de un uso y vencimiento; no revelar si existe la cuenta. Refinar con proveedor. |
| [HU-090/091 — Proteger datos y permisos](../../requirements/user-stories/08-seguridad-privacidad-y-calidad.md#hu-090--proteger-los-datos-de-la-cuenta) | Proteger datos y restringir acciones por rol. | Autorización en servidor; negativos para usuario/gestor/admin. |
| [HU-092 — Privacidad y consentimiento](../../requirements/user-stories/08-seguridad-privacidad-y-calidad.md#hu-092--gestionar-privacidad-y-consentimiento) | Controlar permisos opcionales. | Explicar ubicación/notificaciones; rechazar/retirar sin bloquear funciones independientes. |
| [HU-076 — Gestionar usuarios y roles](../../requirements/user-stories/07-administracion-y-datos.md#hu-076--gestionar-usuarios-y-roles) | Limitar gestión de roles. | Solo admin; protección del último acceso; trazabilidad. Puede dividirse si excede capacidad. |

Candidatas para refinar, no Sprint Backlog seleccionado. Priorizar primero modelo de amenazas, autorización del servidor y política de datos.

HU-001 es un requisito transversal establecido desde Sprint 1 y no se vuelve a planificar aquí; validar que las funciones públicas sigan accesibles sin cuenta es una regresión de cada Sprint.

## 4. Plan inicial y dependencias

- Confirmar proveedor de identidad y responsabilidades de cliente/API/proveedor.
- Acordar modelo de roles; la afiliación declarada a UCM no concede permisos.
- Definir datos mínimos, retención, revocación de sesión y recuperación.
- Mantener consulta pública sin registro.
- No recopilar ubicación continua por defecto.
- Refinar y estimar en Sprint Planning según capacidad y dependencias.

## 5. Riesgos — RSGR

| Riesgo | Probabilidad / consecuencia / prioridad inicial | Reducción y seguimiento | Contingencia |
| --- | --- | --- | --- |
| Autorización incompleta → acceso indebido | Ocasional / Crítica / Alta | Modelo de amenazas; pruebas negativas por rol en servidor; revisar rutas sensibles. | Desactivar operaciones privilegiadas hasta corregir y revisar registros. |
| Proveedor de identidad no disponible → bloqueo | Ocasional / Seria / Media | Spike de integración y recuperación; observar disponibilidad. | Mantener datos públicos accesibles y posponer funciones de cuenta. |
| Consentimiento/retención ambiguos → uso inesperado | Ocasional / Crítica / Alta | Inventario de datos, propósito y retención antes de implementar. | No recopilar dato opcional hasta aclarar política. |
| Pérdida del último admin | Remota / Crítica / Media | Probar invariantes y recuperación administrativa. | Procedimiento controlado y trazable. |

## 6. Verificación y Definition of Done

- Caja negra: registro válido/inválido, sesión caducada, token expirado/repetido, permiso aceptado/rechazado/revocado.
- Pruebas negativas: usuario/gestor/admin, API directa y aislamiento de datos.
- Integración de proveedor/API/app y regresión del acceso público.
- Trazar requisitos de privacidad/seguridad a prueba/evidencia; sin secretos.
- Integrado en `main` y CI aplicable en verde antes de Done.

## 7. Sprint Review y retrospectiva

Pendientes. Demostrar consulta pública y flujos autenticados, incluidos rechazos, con datos sintéticos.

## 8. Trabajo no terminado y siguiente paso

Si autorización, recuperación o política de datos no están claras, mantener la historia en backlog y no habilitar funciones dependientes. Refinar HU-005/006, HU-093 y auditoría después de inspeccionar el incremento.
