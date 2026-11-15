# Acta de Reunión — Planificación del Sprint 2 y Reparto de Responsabilidades

* **Fecha:** 13 de noviembre de 2026
* **Hora:** 13:30 - 14:15 CET
* **Lugar:** Sesión de trabajo telemática y laboratorio de software
* **Asistentes:**
  * Naoufal Kebli (`@Naoufal33`)
  * Daniel David (`@ddavid07`)
  * Pablo Palacios (`@pablopr06`)
  * Pedro Cespón (`@pcespon`)
  * Charlie Fox / Carlos (`@yoespain`)

---

## 1. Propósito de la Reunión

Planificar el **Sprint 2**, desbloquear la integración del incremento del Sprint 1 en la rama `main`, estructurar el plan de aceleración de **3 semanas hacia la entrega final** del proyecto y formalizar el reparto de historias de usuario y responsabilidades técnicas entre los 5 integrantes del equipo de acuerdo con el marco Scrum y las directrices de pruebas del Tema 3.

---

## 2. Puntos Tratados y Acuerdos

### 2.1. Cierre del Sprint 1 y Aprobación de la PR #23

* Se constata que la implementación del visor cartográfico con MapLibre y catálogo OpenStreetMap está finalizada en la rama `feature/sprint-01-campus` (PR #23).
* Debido a que Naoufal Kebli figura como co-autor del último commit de ajuste, se acuerda que **Pedro Cespón** o **Pablo Palacios** aprueben formalmente la revisión en GitHub para permitir la fusión definitiva en `main`.

### 2.2. Definición del Sprint Goal (Sprint 2)

El equipo acuerda por unanimidad el objetivo del Sprint:
> *"Implementar el motor de enrutamiento peatonal y multimodal (EMT) en el campus de Moncloa con filtros de accesibilidad PMR y desplegar la suite completa de pruebas unitarias y de integración conforme al marco TDD de la asignatura."*

### 2.3. Asignación de Roles y Reparto de Trabajo (5 Integrantes)

| Miembro | Rol Scrum | Área Técnica Principal | Historias de Usuario |
| :--- | :--- | :--- | :--- |
| **Naoufal Kebli** | Developer | Frontend Móvil (React Native / Expo) | `HU-020` (Origen/Destino), `HU-021` (Ruta a pie), `HU-023` (Indicaciones paso a paso) |
| **Daniel David** | Developer / Arquitecto | Backend NestJS y Contratos Compartidos | Soporte API a `HU-020`/`HU-021`, Contratos de Rutas, `HU-075` (Estado datos) |
| **Pablo Palacios** | Developer | Movilidad Especializada, PMR y Red EMT | `HU-022` (Multimodalidad), `HU-024` (Ruta accesible), `HU-026` (Líneas EMT), `HU-040` (Preferencias PMR) |
| **Pedro Cespón** | QA Lead / Developer | Calidad del Software y Automatización de Pruebas | `HU-094` (Errores/Offline), `HU-095` (Accesibilidad UI), Batería de Tests Vitest/Jest (Tema 3) |
| **Charlie Fox** | Scrum Master / Developer | Panel Web Admin y Seguimiento de Proyecto | `HU-050` (Incidencias), `HU-057` (Avisos), `HU-070` (Gestión edificios), Actas y Burndown |

### 2.4. Adopción de la Estrategia de Pruebas (Tema 3 de la Asignatura)

En consonancia con las lecciones impartidas por los profesores D. Antonio Navarro y D. Gonzalo Méndez sobre *Pruebas Orientadas a Objetos*:

1. **Pruebas de Unidad con Jest y Vitest:**
   * Toda nueva clase y servicio de enrutamiento contará con pruebas unitarias en una estructura paralela de directorios (`test/` o `*.spec.ts`).
   * Se aplicará el método del camino básico (Caja Blanca) para cubrir los grafos de flujo de cálculo de rutas y normalización de textos.
   * Se diseñarán casos de prueba de Caja Negra mediante clases de equivalencia y valores límite (ej. entradas nulas, nombres de lugares fuera de Moncloa).
2. **Práctica de TDD:**
   * El desarrollo del motor de rutas seguirá las 3 reglas de Uncle Bob (*Red $\rightarrow$ Green $\rightarrow$ Refactor*).
3. **Pruebas de Regresión en CI:**
   * Ningún commit podrá fusionarse en `main` si rompe los tests existentes en GitHub Actions.

### 2.5. Acuerdos Operativos y Siguientes Pasos

* **Daily Scrum asíncrono:** cada miembro publicará al inicio de jornada en el canal del equipo qué completó ayer, qué abordará hoy y qué bloqueos tiene.
* **Integración continua estricta:** evitar trabajar en ramas locales aisladas durante más de 48 horas sin abrir un borrador de PR para visibilidad del equipo.
* **Duración:** Sprint 2 tendrá una duración fijada de 2 semanas, enlazando directamente con la semana final (Sprint 3) de consolidación, pruebas de sistema y preparación de la defensa oral.

---

*Acta aprobada por los 5 integrantes del equipo.*
