# Metodología de trabajo: Scrum

## Decisión vigente

UniMovil utiliza **Scrum** como marco de trabajo para organizar el desarrollo, revisar incrementos y adaptar las prioridades a lo que el equipo aprende en cada ciclo. Esta decisión satisface el requisito de la asignatura de trabajar de forma ágil. La referencia normativa del equipo es la [Guía oficial de Scrum](https://scrumguides.org/scrum-guide.html).

El alcance completo del proyecto no se convierte en un plan de ejecución cerrado. Se mantiene un objetivo de producto y un backlog ordenado que se refina progresivamente. Cada Sprint concreta un objetivo próximo, produce un incremento verificable y deja que el feedback influya en la planificación posterior.

## Responsabilidades

Scrum define tres responsabilidades dentro del Scrum Team:

- **Product Owner:** maximiza el valor del producto y ordena el Product Backlog. Recoge y aclara necesidades con las personas interesadas.
- **Scrum Master:** ayuda a que el equipo comprenda y aplique Scrum, facilita la mejora y ayuda a resolver impedimentos. No es un jefe que reparte tareas.
- **Developers:** crean el incremento y deciden cómo organizar el trabajo necesario para lograr el Sprint Goal.

Las personas que asumirán estas responsabilidades en UniMovil se acordarán entre el equipo antes de la primera planificación. No se asignan nombres ni se presuponen acuerdos en esta documentación. El Scrum Team trabaja como un equipo autogestionado; las responsabilidades no requieren crear subequipos separados.

## Cadencia y eventos

El trabajo se organiza en Sprints de duración fija, de un mes como máximo. La duración concreta se acordará antes del primer Sprint, teniendo en cuenta el calendario de la asignatura y las oportunidades reales de presentar y recibir feedback. No se presume aquí una fecha ni una duración que el equipo aún no haya acordado.

Cada Sprint incluye:

1. **Sprint Planning:** el equipo acuerda por qué el Sprint es valioso (Sprint Goal), qué trabajo puede contribuir a ese objetivo y un plan inicial para producirlo.
2. **Daily Scrum:** encuentro diario de hasta 15 minutos para que los Developers inspeccionen el progreso hacia el Sprint Goal y adapten el plan de trabajo.
3. **Sprint Review:** equipo e interesados inspeccionan el incremento, conversan sobre lo aprendido y adaptan el Product Backlog. Una presentación en clase puede servir como Review si se muestra el incremento y se busca conversación y feedback; una exposición de diapositivas por sí sola no sustituye esa inspección.
4. **Sprint Retrospective:** el equipo inspecciona cómo trabajó y acuerda mejoras concretas para el siguiente Sprint.

El refinamiento del Product Backlog ocurre de manera continua y no es una ceremonia adicional obligatoria. El feedback se registra con su origen y se convierte en cambios del backlog cuando el Product Owner y el equipo acuerdan cómo responder.

## Artefactos y compromisos

- **Product Backlog — Product Goal:** lista ordenada y evolutiva del trabajo necesario para mejorar el producto. El [backlog del proyecto](../backlog/product-backlog.md) enlaza a las historias completas, que permanecen en `requirements/user-stories/`.
- **Sprint Backlog — Sprint Goal:** objetivo del Sprint, elementos elegidos para el Sprint y plan de trabajo actualizado por los Developers.
- **Increment — Definition of Done:** resultado usable que cumple la Definition of Done acordada. Los criterios generales existentes están en el [índice de historias de usuario](../requirements/user-stories/README.md); el equipo los concreta para que sean verificables en el código y la aplicación.

Una historia solo se considera terminada cuando cumple los criterios de aceptación aplicables y la Definition of Done. El trabajo no terminado vuelve al Product Backlog para ser reordenado; no se da por completado por haber llegado a una presentación.

## Registro y adaptación

Cada Sprint tendrá su propio registro en `iterations/sprint-XX/README.md`, creado a partir de la [plantilla de Sprint](../iterations/template-sprint.md). El registro enlazará la presentación, las evidencias, la revisión, los acuerdos y la retrospectiva cuando existan. Las presentaciones se guardan en `presentations/`, las actas en `meetings/` y las pruebas/evidencias en `validation/`, evitando duplicar archivos.

Las decisiones sobre el producto y el proceso pueden cambiar a partir de evidencia o feedback. Se registra qué cambió y por qué, y se mantiene el historial mediante Git. Los documentos históricos no son compromisos de planificación vigentes.

## Primer paso operativo

Antes de planificar el primer Sprint, el equipo acordará la asignación de responsabilidades, la duración del Sprint, el Product Goal y una Definition of Done comprobable. Después refinará y ordenará el Product Backlog y celebrará la primera Sprint Planning. No se define un “Sprint 0” por defecto: una fase inicial solo se trataría como Sprint si tuviera un Sprint Goal y produjera un incremento útil.
