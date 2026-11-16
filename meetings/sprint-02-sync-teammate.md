# Acta de Reunión — Sincronización y Validación del Sprint 2

* **Fecha y Hora:** 17 de noviembre de 2026, 10:00 – 11:15 CET
* **Lugar:** Aula 12 / Conexión Híbrida (Facultad de Informática, UCM)
* **Asistentes:**
  * Charlie Fox (`@charliefox06`) — Developer (Web Admin & Panel de Gestión)
  * Naoufal Kebli (`@Naoufal33`) — Mobile Frontend Developer
  * Pedro Cespón (`@pcespon`) — QA & Routing Developer (asíncrono)
  * Daniel David (`@ddavid07`) — Backend & Infrastructure (asíncrono)
  * Pablo Palacios (`@pablopr06`) — PMR Accessibility Developer (asíncrono)

---

## 1. Propósito de la Reunión

1. Verificar la integración definitiva del Sprint 1 en la rama `main` tras el cierre de la PR #23.
2. Sincronizar el progreso del **Sprint 2** entre el desarrollo móvil (`apps/mobile`), el motor de rutas peatonal y accesible, y el nuevo **Panel Web de Administración** (`apps/admin`).
3. Formalizar la entrega de los contratos canónicos de **Auditoría y Trazabilidad (`HU-097`)** y **Gestión de Incidencias (`HU-050` / `HU-054` / `HU-055`)** en `@unimovil/contracts`.
4. Revisar la batería de pruebas automatizadas según los estándares de pruebas del Tema 3 (profesores Antonio Navarro y Gonzalo Méndez).

---

## 2. Acuerdos y Decisiones Técnicas

### 2.1. Cierre y Verificación del Sprint 1
* Se confirma que la rama `main` de `UniMovil` ya incorpora el visor cartográfico con MapLibre y el catálogo de facultades de Moncloa.
* Todos los integrantes trabajan a partir de ahora directamente desde ramas derivadas de `main`.

### 2.2. Panel de Administración y Backoffice (`apps/admin`) — Entregable de Charlie Fox (`@charliefox06`)
* **Gestión de Edificios y Lugares (`HU-070`):** Implementada la vista de administración de recursos del campus con filtrado por categoría, accesibilidad PMR y estado operativo (`active`, `maintenance`, `inactive`). Permite cambiar el estado de facultades y accesos con motivo justificado.
* **Gestión de Incidencias de Movilidad (`HU-050`, `HU-054`, `HU-055`):** Implementado el panel de revisión de incidencias (rampas, ascensores, aceras, etc.) con transiciones de estado estrictamente tipadas y validadas según el ciclo:
  $$\text{recibida} \longrightarrow \text{en\_revisión} \longrightarrow \text{en\_proceso} \longrightarrow \text{resuelta} \longrightarrow \text{cerrada}$$
* **Trazabilidad de Cambios (`HU-097`):** Vista de registro de auditoría que registra en tiempo real autor (`@charliefox06`), marca de tiempo ISO 8601, recurso afectado y acción realizada.
  * **Seguridad y Privacidad:** Se incorpora mecanismo de saneado y ofuscación de credenciales para garantizar que contraseñas, tokens y datos sensibles jamás queden expuestos en los logs.

### 2.3. Contratos Compartidos (`@unimovil/contracts`)
* Se publican los modelos canónicos:
  * `AuditEntry`, `AuditAction`, `AuditResource`, `createAuditEntry`, `parseAuditEntry`.
  * `Incident`, `IncidentStatus`, `IncidentPriority`, `IncidentCategory`, `isValidIncidentTransition`, `parseIncident`.
* Se valida la compatibilidad estricta con TypeScript `exactOptionalPropertyTypes: true` y compilación modular `NodeNext`.

### 2.4. Estrategia de Pruebas Unitarias (Tema 3)
* Se valida la suite de pruebas unitarias en `apps/admin/src/domain/admin-service.spec.ts` y en `@unimovil/contracts`.
* Cobertura de caminos independientes mediante el método del camino básico (Caja Blanca) y análisis de partición de equivalencia y valores límite (Caja Negra) en transiciones de incidencias y filtros.
* Resultados: **119 pruebas superadas**, 0 errores de compilación (`typecheck`) y 0 advertencias de ESLint (`--max-warnings=0`).

---

## 3. Próximos Pasos y Plan de Aceleración

1. **Naoufal Kebli:** Continuar con la integración del visor de polilíneas de ruta en `apps/mobile/src/features/routing/`.
2. **Charlie Fox:** Monitorizar el Burndown chart del Sprint 2 y actualizar la matriz RSGR de riesgos de Barry Boehm en la memoria del proyecto.
3. **Pedro Cespón / Daniel David:** Integrar el servicio backend NestJS con los nuevos contratos de incidencias.

---

*Acta redactada por Charlie Fox (`@charliefox06`), Developer del equipo UniMovil.*
