# Sprint XX — [resultado breve de valor]

> Registro vivo. Distingue plan, trabajo en curso e incremento integrado. No rellenes campos con supuestos.

## 1. Estado y fuente de información

- **Estado:** Propuesta / En curso / Integrado y verificado.
- **Fuente del estado:** PR, commit, evidencia o acuerdo enlazado.
- **Periodo:** pendiente hasta que el equipo acuerde inicio y duración; al cerrar, registrar fechas reales.
- **Capacidad y estimación:** las acuerdan los Developers en Planning. No convertir Story Points en horas ni asignar puntos desde este documento.
- **Responsabilidades Scrum:** enlazar acuerdo cuando exista; no repartir trabajo individual aquí.

## 2. Sprint Goal

[Resultado de valor único, comprensible y comprobable. Marcar como propuesta hasta acordarlo.]

## 3. Historias candidatas y criterios de aceptación

| Historia candidata | Resultado de valor | Criterio observable y evidencia |
| --- | --- | --- |
| [ID y enlace] | [Qué podrá hacer la persona usuaria] | [Cómo se comprobará] |

Las historias son candidatas hasta que el equipo las seleccione según Sprint Goal, capacidad y dependencias. Refinar o dividir las que no puedan terminarse dentro del Sprint.

## 4. Plan inicial y dependencias

[Orden inicial del trabajo, decisiones/spikes, dependencias y cambios relevantes hacia el Sprint Goal. Los Developers mantienen el plan.]

## 5. Riesgos — RSGR

Valoración inicial propuesta para revisar con el equipo. Identifica probabilidad y consecuencia, prioriza, reduce, supervisa y prepara contingencia.

| Riesgo (causa → posible efecto) | Probabilidad / consecuencia / prioridad | Reducción y señal de seguimiento | Contingencia si ocurre |
| --- | --- | --- | --- |
| [Riesgo específico] | [Estimación inicial] | [Acción preventiva y señal] | [Respuesta prevista] |

## 6. Verificación y Definition of Done

Por cada historia terminada, enlazar requisito, código integrado y evidencia. Elegir pruebas según el riesgo: caja negra (clases de equivalencia y valores límite), caja blanca (decisiones/caminos cuando aplique), unitarias, integración, sistema, aceptación y regresión.

- **Criterios de aceptación comprobados:**
- **Pruebas/herramientas, commit y entorno:**
- **Builds/plataformas, cuando proceda:**
- **Trazabilidad requisito → cambio → prueba/evidencia:**
- **Limitaciones, datos no verificados y riesgos abiertos:**

DoD: criterios cumplidos; comprobaciones requeridas en verde; cambio integrado en `main`; documentación y procedencia actualizadas; sin secretos/datos privados. PR abierta, cobertura o demo aislada no bastan para declarar Done. Aplicar TDD durante el desarrollo cuando corresponda; no afirmar retrospectivamente una secuencia sin evidencia.

## 7. Sprint Review y retrospectiva

- **Review:** fecha/contexto, incremento inspeccionado, feedback real y cambios acordados al Product Backlog.
- **Retrospectiva:** observaciones y una acción concreta de mejora.
- **Enlaces:** `meetings/`, `validation/` y `presentations/`.

Si no se celebraron, indicar “Pendiente”; una agenda o presentación no es una Review ni un acta.

## 8. Trabajo no terminado y siguiente paso

[Historias que no cumplen DoD, riesgos vigentes y propuesta de reordenación del Product Backlog. No prometer su inclusión automática en el siguiente Sprint.]
