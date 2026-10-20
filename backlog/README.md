# Backlog del producto

El Product Backlog es la lista ordenada y evolutiva de oportunidades de producto, historias, defectos y trabajo técnico. Es la fuente para decidir qué refinar y qué podría entrar en un Sprint; no es un calendario ni un compromiso de entregar todas sus entradas.

## Fuente de verdad

- [Product Backlog](product-backlog.md): índice de planificación que enlaza las historias y refleja su prioridad actual.
- [Historias de usuario](../requirements/user-stories/README.md): descripción completa, criterios de aceptación, dependencias y prioridad funcional existente.
- [Catálogo funcional](../requirements/functional-catalog.md): capacidades y alcance funcional del producto.

No copies aquí el texto completo de las historias. Mantén sus identificadores y referencias para que cada necesidad tenga una sola descripción canónica.

## Orden y refinamiento

El Product Owner es responsable de ordenar el backlog. El equipo aporta información sobre valor, riesgo, dependencias, esfuerzo y aprendizaje esperado. El orden se revisa cuando hay feedback de una Sprint Review, nueva evidencia, cambios de contexto o mejor comprensión del producto.

El Product Backlog inicial agrupa las historias por las prioridades Alta, Media y Baja que ya aparecen en sus documentos. Esas etiquetas expresan la prioridad funcional relativa ya registrada; **no son un orden definitivo entre historias ni una asignación a Sprints**. El orden concreto de trabajo y el estado de implementación se confirmarán en el primer refinamiento del equipo. No se atribuyen aquí estimaciones, responsables, fechas ni resultados que aún no se hayan acordado.

Durante el refinamiento, el equipo puede aclarar el resultado, revisar criterios de aceptación, identificar dependencias, dividir historias demasiado amplias y reordenar elementos. Los cambios relevantes deben conservar trazabilidad en el historial de Git y, cuando proceda, explicar el motivo en el registro del Sprint o del acuerdo.

## Cuándo está lista una historia para planificarse

Una historia está suficientemente refinada para considerarla en una Sprint Planning cuando:

- el problema y el usuario beneficiado se entienden;
- el resultado esperado y los criterios de aceptación son observables;
- las dependencias y riesgos conocidos están visibles;
- el equipo entiende el trabajo y puede colaborar en un plan inicial;
- su tamaño permite completarla dentro de un Sprint o puede dividirse.

Estar lista no garantiza que se seleccione para el siguiente Sprint. La selección se decide en la planificación considerando el Sprint Goal y la capacidad real del equipo.

## Cuándo está terminada

Una historia está terminada cuando cumple sus criterios de aceptación y la Definition of Done aplicable, está integrada en el incremento y dispone de las pruebas y documentación necesarias. Los criterios generales están en el [índice de historias](../requirements/user-stories/README.md); el equipo concretará antes del primer Sprint cualquier criterio técnico adicional que necesite.

Si una historia no alcanza ese estado al terminar el Sprint, se vuelve a ordenar en el Product Backlog. No se arrastra automáticamente como compromiso al siguiente Sprint.
