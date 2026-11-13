# Acta de Reunión — Planificación del Sprint 3 y Reparto de Responsabilidades

* **Fecha:** 13 de noviembre de 2026
* **Hora:** 14:00 - 14:30 CET
* **Lugar:** Sesión de trabajo telemática y laboratorio de software
* **Asistentes:**
  * Naoufal Kebli (`@Naoufal33`)
  * Daniel David (`@ddavid07`)
  * Pablo Palacios (`@pablopr06`)
  * Pedro Cespón (`@pcespon`)
  * Charlie Fox / Carlos (`@yoespain`)

---

## 1. Propósito de la Reunión

Planificar el **Sprint 3**, consolidar el trabajo sobre el transporte público multimodal de la EMT (Líneas G y F de Ciudad Universitaria) y establecer el sistema de notificación y visualización de incidencias del campus para la aceleración del proyecto.

---

## 2. Puntos Tratados y Acuerdos

### 2.1. Revisión de Prerrequisitos y Alcance

* Se valida la integración de los contratos de enrutamiento y se aprueba extender el modelo de datos para acoger las líneas y paradas de la EMT.
* Se define el mecanismo de incidencias ciudadanas/universitarias para señalar obstáculos temporales en el campus (obras, desvíos, aceras cortadas).

### 2.2. Sprint Goal del Sprint 3

Aprobado por unanimidad:
> *"Integrar el transporte público interno del campus (líneas G y F de la EMT) con cálculo comparativo de tiempos respecto a la caminata, e implementar el sistema de reporte y consulta de incidencias y obras en viales de Moncloa."*

### 2.3. Asignación de Historias y Responsables

| Miembro | Responsabilidad Principal | Historias Asignadas |
| :--- | :--- | :--- |
| **Naoufal Kebli** | Frontend Móvil: Tarjeta comparativa multimodal y trazado de líneas EMT | `HU-022`, `HU-026` |
| **Daniel David** | Backend NestJS: Catálogo de paradas y endpoints de transporte EMT | `HU-026`, `HU-027`, `HU-072` |
| **Pablo Palacios** | Móvil: Formulario de incidencias y capas cartográficas de obras | `HU-050`, `HU-051`, `HU-053` |
| **Pedro Cespón** | QA: Pruebas de integración basadas en hilos y caja negra (Tema 3) | `HU-094`, Verificación Sprint 3 |
| **Charlie Fox** | Web Admin: Panel de visualización de incidencias reportadas en `apps/admin` | `HU-054`, `HU-055`, Burndown |

---

*Acta aprobada por los 5 integrantes del equipo.*
