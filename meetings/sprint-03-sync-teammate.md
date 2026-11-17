# Acta de Reunión — Sincronización y Validación del Sprint 3

* **Fecha y Hora:** 17 de noviembre de 2026, 17:00 – 18:15 CET
* **Lugar:** Aula 12 / Conexión Híbrida (Facultad de Informática, UCM)
* **Asistentes:**
  * Charlie Fox (`@charliefox06`) — Developer (Web Admin & Panel de Gestión)
  * Naoufal Kebli (`@Naoufal33`) — Mobile Frontend Developer
  * Pedro Cespón (`@pcespon`) — QA & Routing Developer (asíncrono)
  * Daniel David (`@ddavid07`) — Backend & Infrastructure (asíncrono)
  * Pablo Palacios (`@pablopr06`) — PMR Accessibility Developer (asíncrono)

---

## 1. Propósito de la Reunión

1. Sincronizar el progreso del **Sprint 3** centrado en la **Movilidad Multimodal de la EMT** (Líneas G y F de Ciudad Universitaria) y la **Gestión de Incidencias en Campus**.
2. Formalizar la integración técnica entre el reporte móvil de obstáculos y el sistema de moderación y triaje en el **Panel Web de Administración (`apps/admin`)** desarrollado por Charlie Fox (`@charliefox06`).
3. Validar la ampliación del contrato canónico de incidencias en `@unimovil/contracts` para soportar asignación departamental y reclasificación de prioridades (`HU-054` / `HU-055`).
4. Evaluar la batería de pruebas automatizadas según los estándares del Tema 3 (profesores Antonio Navarro y Gonzalo Méndez).

---

## 2. Acuerdos y Decisiones Técnicas

### 2.1. Movilidad Multimodal EMT en Cliente Móvil (PR #34)
* Se valida la integración de las líneas G y F de la EMT sobre la cartografía esquemática de MapLibre con paradas oficiales calibradas (Paraninfo, Metro Ciudad Universitaria, Filosofía, Medicina).
* La tarjeta comparativa multimodal (`MultimodalComparisonCard.tsx` — `HU-022`) confronta con precisión matemática (fórmula del semiverseno) los tiempos a pie vs. autobús universitario.

### 2.2. Panel Web de Moderación y Resolución de Incidencias (`apps/admin`) — Entregable de Charlie Fox (`@charliefox06`)
* **Gestión y Clasificación de Incidencias (`HU-054`):**
  * Implementado el tablero de supervisión de incidencias reportadas por la comunidad universitaria, con métricas agregadas por estado (Total, Pendientes, En Intervención, Resueltas).
  * Soporte específico para incidencias sobre el transporte público del campus (e.g. obras y cortes de carril bus en parada EMT 1688 de la Línea G).
  * Modal de gestión que permite reclasificar la severidad operativa (`baja`, `media`, `alta`, `urgente`) y asignar la resolución a departamentos o unidades técnicas específicas (ej. *Mantenimiento UCM*, *Conserjería*, *EMT Madrid*).
* **Actualización del Ciclo de Vida de Incidencias (`HU-055`):**
  * Control estricto de transiciones conforme al autómata de estados:
    $$\text{recibida} \longrightarrow \text{en\_revisión} \longrightarrow \text{en\_proceso} \longrightarrow \text{resuelta} \longrightarrow \text{cerrada}$$
  * Bloqueo preventivo en la interfaz para impedir transiciones incoherentes o saltos directos no permitidos.
  * Inclusión obligatoria de notas técnicas de intervención y justificación en cada cambio de estado.
* **Trazabilidad Inmutable (`HU-097`):**
  * Cada acción de moderación genera de manera transparente un registro en el log de auditoría con diff de estados (anterior vs. nuevo), fecha/hora formateada y ofuscación de datos confidenciales.

### 2.3. Contratos Canónicos Compartidos (`@unimovil/contracts`)
* Actualización de la interfaz `Incident` y su validador `parseIncident` para acoger el campo opcional `assignedTo`.
* Compatibilidad estricta asegurada bajo compilación TypeScript `exactOptionalPropertyTypes: true`.

### 2.4. Estrategia y Resultados de Pruebas (Tema 3)
* **Pruebas de Unidad (Caja Blanca & Caja Negra):** 23 tests específicos en `apps/admin/src/domain/admin-service.spec.ts` y 10 tests en contracts.
* **Resultados Monorepo:** **120 pruebas superadas** en Vitest, 0 errores de compilación (`typecheck`) y 0 advertencias de ESLint (`--max-warnings=0`).

---

## 3. Próximos Pasos (Sprint 4: Cierre Académico y Validación Global)

1. **Charlie Fox:** Liderar la preparación del cierre académico: redacción de conclusiones y métricas en la memoria técnica (`memory/memoria-del-proyecto.md`), guión y diapositivas de la defensa final de 5 minutos (`presentations/presentacion-del-proyecto.md`) y soporte para publicación de avisos urgentes (`HU-057`).
2. **Naoufal Kebli / Pedro Cespón:** Consolidar el modo sin conexión (`HU-094`) y la auditoría de accesibilidad WCAG 2.1 AA (`HU-095`) en la app móvil.
3. **Daniel David:** Verificar la securización de endpoints y métricas de producción en `apps/api`.

---

*Acta redactada por Charlie Fox (`@charliefox06`), Developer del equipo UniMovil.*
