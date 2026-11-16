# Sprints e iteraciones

Esta carpeta contiene el plan y registro de cada Sprint. Cada carpeta `sprint-XX/` tiene un README basado en la [plantilla](template-sprint.md). Un plan es propuesta hasta que el equipo acuerda el Sprint Goal y selecciona el Sprint Backlog en Sprint Planning.

## Secuencia de incrementos propuesta

La secuencia refleja dependencias; no fija fechas, duración, capacidad, estimaciones ni compromisos de entrega. Los Sprints 5 y 6 amplían la hoja de ruta, pero no asignan todo el Product Backlog a seis Sprints.

1. [Sprint 1 — Explorar el campus](sprint-01/README.md): mapa, catálogo, búsqueda y ficha básica.
2. [Sprint 2 — Calcular rutas peatonales accesibles](sprint-02/README.md): origen/destino, ruta, indicaciones y accesibilidad.
3. [Sprint 3 — Consultar transporte público](sprint-03/README.md): líneas, paradas y comparación multimodal.
4. [Sprint 4 — Mejorar resiliencia y accesibilidad](sprint-04/README.md): errores/conectividad limitada, accesibilidad de interfaz e integración.
5. [Sprint 5 — Gestionar cuentas, privacidad y permisos](sprint-05/README.md): identidad, sesiones, consentimiento y autorización.
6. [Sprint 6 — Cerrar el ciclo de incidencias](sprint-06/README.md): seguimiento de incidencias, notificaciones y validación de sistema.

## Qué registra cada Sprint

1. **Estado y evidencia:** propuesta, en curso o integrada y verificada. Una rama o PR abierta no equivale a un incremento integrado.
2. **Sprint Goal y alcance:** resultado de valor, historias candidatas y criterios observables. La selección final se hace en Sprint Planning según capacidad.
3. **Plan y dependencias:** orden lógico, decisiones/spikes y ajustes, sin reparto nominal de tareas.
4. **Riesgos RSGR:** probabilidad y consecuencia iniciales, prioridad, reducción, señales de seguimiento y contingencia.
5. **Verificación:** pruebas, resultados con commit/entorno y limitaciones; no se declaran métricas sin evidencia reproducible.
6. **Review y retrospectiva:** incremento inspeccionado, feedback real, decisiones y mejora. Si no ocurrieron, se indica pendiente.
7. **Trabajo restante:** vuelve al Product Backlog para reordenación; no se arrastra automáticamente.

Las actas/acuerdos se guardan en [meetings](../meetings/); los planes y resultados de pruebas, en [validation](../validation/); las presentaciones, en [presentations](../presentations/). Se enlazan desde el Sprint, sin duplicar su contenido.

## Criterio para marcar un incremento como terminado

Una historia solo se marca terminada cuando cumple sus criterios de aceptación y DoD, está integrada en `main` y existe evidencia de las comprobaciones aplicables. El contenido de una PR abierta se describe como trabajo propuesto, no como funcionalidad aceptada.

Los registros de Sprints 1–4 se normalizan con este criterio. Los Sprints 5–6 son propuestas. Ningún documento fija fechas, responsables, puntos o capacidad que el equipo no haya acordado.
