# Plan de validación — Sprint 1

**Estado:** plan pendiente de ejecutar. Este documento define verificaciones previstas; no contiene resultados de pruebas ni evidencias realizadas.

Relacionado con [Sprint 1 — Mapa interactivo del campus](../iterations/sprint-01/README.md) y con HU-010, HU-012, HU-013 y el corte previsto de HU-014.

## Prerrequisitos

- Build de desarrollo de la app en los dispositivos/emuladores que confirme el equipo.
- Configuración local válida del mapa, fuera del repositorio, y acceso a red para las teselas.
- Conjunto semilla con procedencia de los datos documentada.
- Atribución del proveedor visible.

## Escenarios previstos

| ID | Escenario | Resultado esperado | Evidencia a guardar |
| --- | --- | --- | --- |
| V1-01 | Abrir UniMovil con conectividad y configuración válida. | Se muestra el mapa del campus y sus controles; se ve la atribución correspondiente. | Captura de pantalla sin datos personales y dispositivo/plataforma. |
| V1-02 | Desplazar el mapa y acercar/alejar. | La cámara responde a gestos y mantiene visibles los marcadores pertinentes. | Nota/captura antes y después, y plataforma. |
| V1-03 | Esperar la carga inicial de los lugares. | Cada marcador corresponde a una entrada del conjunto verificado y usa su categoría. | Lista de IDs de datos y fuente/procedencia. |
| V1-04 | Buscar un lugar por su nombre. | Aparecen sugerencias/resultados comprensibles con nombre y categoría; al elegir uno, el mapa centra o destaca el lugar. | Búsqueda usada y resultado observado. |
| V1-05 | Buscar por categoría o texto relacionado cuando el catálogo lo soporte. | Se muestran solo coincidencias pertinentes. | Consulta y resultado observado. |
| V1-06 | Aplicar un filtro y restablecerlo; combinarlo con una búsqueda. | Lista y marcadores permanecen sincronizados; restablecer recupera los elementos disponibles. | Filtro/consulta y resultado observado. |
| V1-07 | Seleccionar un marcador en el mapa. | Se destaca la selección y aparece la ficha breve del mismo lugar; datos ausentes se indican como no disponibles. | Captura del marcador y ficha. |
| V1-08 | Realizar una búsqueda sin coincidencias. | Mensaje claro y posibilidad de corregir/limpiar la consulta. | Consulta y captura. |
| V1-09 | Iniciar sin red o provocar un fallo de carga del mapa. | Se comunica que el mapa/datos no pudieron cargarse; la pantalla no presenta un mapa vacío como si fuese correcto. | Pasos reproducibles, mensaje y plataforma. |
| V1-10 | Revisar tamaños de pantalla y orientación soportados por el equipo. | Controles, buscador, resultados y ficha son utilizables sin solapamientos críticos. | Tamaño/plataforma y observaciones. |
| V1-11 | Revisar accesibilidad básica de controles. | Controles interactivos tienen nombre accesible; texto legible y foco/uso táctil comprensible. | Lista de comprobaciones y limitaciones. |
| V1-12 | Revisar fuentes, licencia/atribución, configuración y repositorio. | Las atribuciones son visibles; no se incorporan secretos; datos y uso del proveedor respetan sus condiciones. | Enlaces a fuentes/PR y resultado de revisión. |

## Registro de ejecución

Completar únicamente después de ejecutar cada escenario.

| ID | Estado (pendiente/aprobado/fallido/bloqueado) | Build/dispositivo | Fecha | Evidencia/enlace | Observaciones o incidencia |
| --- | --- | --- | --- | --- | --- |
| V1-01 | Pendiente | — | — | — | — |
| V1-02 | Pendiente | — | — | — | — |
| V1-03 | Pendiente | — | — | — | — |
| V1-04 | Pendiente | — | — | — | — |
| V1-05 | Pendiente | — | — | — | — |
| V1-06 | Pendiente | — | — | — | — |
| V1-07 | Pendiente | — | — | — | — |
| V1-08 | Pendiente | — | — | — | — |
| V1-09 | Pendiente | — | — | — | — |
| V1-10 | Pendiente | — | — | — | — |
| V1-11 | Pendiente | — | — | — | — |
| V1-12 | Pendiente | — | — | — | — |

## Registro de feedback de Review

No registrar feedback antes de recibirlo. Tras la Sprint Review, añadir cada comentario con su contexto, aclarar si es observación o acuerdo y enlazar el cambio de Product Backlog si el equipo decide actuar.

| Contexto/fecha | Observación recibida | Decisión acordada | Enlace a backlog/evidencia |
| --- | --- | --- | --- |
| Pendiente de Sprint Review | — | — | — |
