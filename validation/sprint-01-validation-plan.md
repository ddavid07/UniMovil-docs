# Plan de validación — Sprint 1

**Estado:** primeras pruebas automatizadas disponibles; aceptación nativa y del incremento pendientes. Las pruebas de componentes no acreditan por sí solas el funcionamiento de MapLibre nativo o MapTiler real.

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

## Primeras evidencias automatizadas

La [CI del commit 828fb98](https://github.com/ddavid07/UniMovil/actions/runs/39369566780) aprobó la validación del monorepo: formato, lint, tipos, catálogo, 76 pruebas de dominio, 13 de componentes, una de rendimiento de búsqueda y builds. La cobertura de dominio fue del 100 %; los componentes superaron los umbrales acordados. Esta evidencia corresponde a esa versión de la PR y no sustituye comprobar su último commit.

La [PR #23](https://github.com/ddavid07/UniMovil/pull/23) contiene el seguimiento actualizado de CI, compilación Android/iOS y flujos Maestro. Gitleaks, CodeQL y Dependency Review aprobaron la primera versión; auditoría npm y OSV detectaron bloqueos pendientes. Los escenarios V1 siguen pendientes hasta comprobar sus evidencias específicas; no se aprueban por disponer únicamente de pruebas de lógica o componentes.

## Umbrales de aceptación

| Control | Condición |
| --- | --- |
| Cobertura del código nuevo de producto | 90 % de líneas, sentencias y funciones; 85 % de ramas. |
| Validación del catálogo y reglas de exploración | 100 % de ramas. |
| Mínimo por archivo | 80 % de líneas y 70 % de ramas. |
| Búsqueda/filtros con 1.000 registros sintéticos | p95 ≤ 30 ms; 20 calentamientos y 100 muestras. La medición en Node no acredita rendimiento nativo. |
| Entrada hasta resultados visibles | p95 ≤ 150 ms, al menos 30 muestras nativas. |
| Selección hasta ficha visible | p95 ≤ 200 ms, al menos 30 muestras nativas. |
| Arranque hasta interfaz local utilizable | p95 ≤ 3 s, 20 arranques; descarga del proveedor medida por separado. |
| Renderizado con estilo de prueba controlado | p95 ≤ 5 s. |
| Gestos Android | Menos del 5 % de fotogramas fuera de 16,7 ms; traza que incluya la superficie nativa del mapa. |
| Memoria y estabilidad | 20 ciclos, sin cierres/ANR ni crecimiento sostenido; variación final ≤ 10 % tras reposo. |
| Ejecución nativa | Tres recorridos consecutivos sobre el mismo commit en Android e iOS; escenarios normales y de recuperación, tamaños habitual y compacto. |
| Proveedor real | MapTiler configurado con clave pública restringida, atribución y posiciones revisadas; la fixture no sustituye esta prueba. |
| Seguridad | Sin secretos ni altos/críticos pendientes. No se omiten controles para declarar éxito. |

Las mediciones de interacción, arranque, fotogramas y memoria permanecen pendientes. La falta de clave de MapTiler y los advisories sin parche impiden cerrar la aceptación. No se presupone validación en hardware físico.

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
