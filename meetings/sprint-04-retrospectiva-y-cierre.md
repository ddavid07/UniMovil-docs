# Acta de Reunión — Retrospectiva Final y Cierre del Proyecto UniMovil (Sprint 4)

* **Fecha y Hora:** 16 de noviembre de 2026, 18:30 – 19:45 CET
* **Lugar:** Aula 12 / Conexión Híbrida (Facultad de Informática, UCM)
* **Asistentes:**
  * Charlie Fox (`@charliefox06`) — Developer (Web Admin & Documentación/Presentación)
  * Naoufal Kebli (`@Naoufal33`) — Developer (Móvil & Accesibilidad)
  * Daniel David (`@ddavid07`) — Developer (Backend, API & Infraestructura)
  * Pablo Palacios (`@pablopr06`) — Developer (Web Admin & Lugares)
  * Pedro Cespón (`@pcespon`) — Developer (QA, Routing & Validación)

---

## 1. Propósito de la Reunión

1. Llevar a cabo la **Sprint Review del Sprint 4**, comprobando la finalización y aceptación técnica de todos los incrementos planificados.
2. Realizar la **Retrospectiva Final del Proyecto** (Sprint Retrospective) evaluando la velocidad del equipo, lecciones aprendidas y balance metodológico de Scrum frente a modelos tradicionales en cascada.
3. Verificar el cumplimiento formal de la **Definition of Done (DoD)** de la entrega académica de Ingeniería del Software 1 (IS1).
4. Validar el material de la **Defensa Oral y Demostración Técnica en Vivo (5 minutos)** ante el tribunal docente (profesores Antonio Navarro y Gonzalo Méndez).

---

## 2. Sprint Review: Balance de Entregables del Sprint 4

El equipo constata el cumplimiento del 100% de los objetivos comprometidos para el Sprint 4:

### 2.1. Panel Web de Administración y Avisos Urgentes (`apps/admin`) — Charlie Fox & Pablo Palacios
* **Publicación y Difusión de Avisos (`HU-057` / `HU-058`):**
  * Vista de Avisos y Alertas (`AnnouncementsView.tsx`) con métricas en tiempo real (Avisos Activos, Alta Prioridad, Alcance Campus).
  * Modal reactivo para publicar nuevos comunicados oficiales tipificados por severidad (`informativo`, `advertencia`, `urgente`) y ámbito (`global`, `edificio`, `transporte`, `accesibilidad`).
* **Trazabilidad Inmutable del Administrador (`HU-097`):**
  * Cada publicación genera automáticamente un evento de auditoría en la pestaña de Trazabilidad (`AuditView.tsx`) con formato estructurado, diff de cambios y preservación de autoría institucional (`@admin.campus`).
* **Calidad y Verificación:**
  * 5 nuevas pruebas unitarias añadidas en `admin-service.spec.ts` (28 pruebas en dominio admin, 125 pruebas verdes en el workspace).

### 2.2. Modo Offline y Accesibilidad Móvil (`apps/mobile`) — Naoufal Kebli
* Implementación de la caché local en SQLite / AsyncStorage para consulta de edificios y paradas sin conexión (`HU-094`).
* Auditoría de contrastes y compatibilidad con lectores de pantalla según WCAG 2.1 AA (`HU-095`).

### 2.3. Hardening y Seguridad Backend (`apps/api`) — Daniel David
* Endpoints administrativos protegidos por token y rate-limiting contra abusos (`HU-090`, `HU-091`).
* Endpoints de healthcheck y métricas de rendimiento en `/health` y `/metrics` (`HU-075`).

### 2.4. QA, Validación del Sistema y Matriz de Trazabilidad — Pedro Cespón
* Ejecución de pruebas de recuperación forzada ante cortes de red y pruebas de sistema basadas en casos de uso (Tema 3).
* Matriz de trazabilidad exhaustiva vinculando cada HU con su respectiva prueba automatizada.

---

## 3. Retrospectiva Final del Proyecto: Análisis Metodológico

### 3.1. ¿Qué ha funcionado excepcionalmente bien?
1. **Disciplina TDD (Las 3 Reglas de Uncle Bob):** Desarrollar la lógica de negocio guiada por pruebas rojas antes del código productivo evitó por completo regresiones entre sprints.
2. **Arquitectura Monorepo con Contratos Canónicos (`@unimovil/contracts`):** La tipificación estricta compartida entre backend, panel web y cliente móvil eliminó discrepancias de formato de datos.
3. **Gestión Proactiva de Riesgos (Barry Boehm RSGR):** La monitorización continua de los 10 riesgos identificados permitió mitigar amenazas críticas tempranamente (discrepancias cartográficas, límites de cuotas, inconsistencias de estado).
4. **Automatización en CI/CD:** El pipeline de GitHub Actions garantizó que ninguna PR fuera integrada con advertencias de linter (`--max-warnings=0`) ni pruebas rotas.

### 3.2. ¿Qué dificultades se afrontaron y cómo se resolvieron?
* **Sincronización de Contratos:** Añadir campos opcionales en `@unimovil/contracts` requería recompilar antes de correr el `typecheck` del admin. Se solventó formalizando scripts de build en el monorepo.
* **Layouts Responsivos en Tablas Administrativas:** Las discrepancias en resolución de pantalla exigieron establecer límites explícitos de `min-height` y `max-height` en la tabla de trazabilidad para evitar colapsos visuales.

### 3.3. Balance: Scrum Ágil frente al Modelo en Cascada
El equipo concluye que abordar UniMovil mediante un modelo en cascada tradicional habría resultado ineficiente o inviable debido a la volatilidad de los requisitos de transporte urbano (líneas de la EMT y obras en Ciudad Universitaria). La cadencia de iteraciones de Scrum permitió:
* Descubrir tempranamente la necesidad de diferenciar paradas oficiales de autobuses y reportar cortes de carril bus en tiempo real.
* Entregar incrementos funcionales desplegables al final de cada sprint (versión web admin en Sprint 2, moderación en Sprint 3, avisos y cierre en Sprint 4).
* Mantener una velocidad de equipo sostenida (45 Story Points totales planificados y completados al 100%).

---

## 4. Comprobación Formal de la Definition of Done (DoD)

| Criterio de la DoD | Estado | Evidencia |
| :--- | :---: | :--- |
| **Compilación Íntegra** | ✅ CUMPLIDO | Monorepo compila con 0 errores TypeScript (`npm run build`). |
| **Pruebas Automatizadas** | ✅ CUMPLIDO | 125 tests en verde en Vitest (`admin-service`, `contracts`, `mobile`). |
| **Calidad de Código** | ✅ CUMPLIDO | 0 errores y 0 warnings en ESLint (`--max-warnings=0`). |
| **Memoria Académica** | ✅ CUMPLIDO | Secciones 1 a 7 completas y revisadas (`memory/memoria-del-proyecto.md`). |
| **Presentación de Defensa** | ✅ CUMPLIDO | Slides y guión de demo de 5 minutos cerrados (`presentations/presentacion-del-proyecto.md`). |
| **Trazabilidad de Requisitos** | ✅ CUMPLIDO | Todas las HUs del Product Backlog vinculadas a código y pruebas. |

---

## 5. Acuerdos Finales para la Defensa Oral

1. **Charlie Fox:** Abrirá la presentación situando el problema de accesibilidad universitaria, defenderá la arquitectura del panel administrativo (`apps/admin`), la trazabilidad inmutable (`HU-097`) y expondrá el balance metodológico y conclusiones.
2. **Equipo:** Todo el equipo asiste a la defensa oral con los artefactos listos para su demostración en vivo (Vite dev server en web y emulador en móvil).

---

*Acta redactada por Charlie Fox (`@charliefox06`), Developer del equipo UniMovil.*
*Aprobada por unanimidad por los 5 integrantes del equipo de desarrollo.*
