# ALEX DEVELOPMENT STANDARD v1.3

Metodología personal de desarrollo mediante vibecoding y agentes. Versión 1.3, 2026-10-06, **vigente y recomendada para adopción gradual**. Su publicación no implica adopción automática.

v1.3 conserva el núcleo operativo de v1.2 y añade **orquestación de capacidad por actividad/microtarea**: separar riesgo de complejidad cognitiva, usar capacidad experta para diagnóstico/arquitectura y capacidad eficiente para ejecución acotada.

## Entrada y mapa

Comenzar por [ENGINEERING_STANDARD.md](ENGINEERING_STANDARD.md).

| Documento | Responsabilidad |
| --- | --- |
| [ENGINEERING_STANDARD](ENGINEERING_STANDARD.md) | Principios, alcance y terminado |
| [CHANGE_MANAGEMENT](CHANGE_MANAGEMENT.md) | Modos y economía de contexto |
| [AGENT_WORKFLOW](AGENT_WORKFLOW.md) | Etapas, fases y roles |
| [ORCHESTRATION_STANDARD](ORCHESTRATION_STANDARD.md) | Capability routing, modelos/reasoning, microtareas, escalamiento y delegación |
| [CONTEXT_MANAGEMENT](CONTEXT_MANAGEMENT.md) | Contexto y transferencia entre agentes |
| [TASK_MANAGEMENT](TASK_MANAGEMENT.md) | Tareas/microtareas y aceptación |
| [TESTING_STANDARD](TESTING_STANDARD.md) | Verificación proporcional |
| [DEPLOYMENT_STANDARD](DEPLOYMENT_STANDARD.md) | Publicación/despliegue |
| [MIGRATION_STANDARD](MIGRATION_STANDARD.md) | Datos persistentes y compatibilidad |
| [PROMPTING_GUIDE](PROMPTING_GUIDE.md) | Pedidos y autonomía por fases |
| [PROJECT_ADOPTION](PROJECT_ADOPTION.md) | Adopción gradual |
| [PROJECT_DOCUMENTATION](PROJECT_DOCUMENTATION.md) | Documentación del proyecto |
| [GIT_WORKFLOW](GIT_WORKFLOW.md) | Git y evidencia remota |
| [SESSION_HANDOFF](SESSION_HANDOFF.md) | Cierre/handoff |
| [DECISION_MANAGEMENT](DECISION_MANAGEMENT.md) | Decisiones |
| [DESIGN_STANDARD](DESIGN_STANDARD.md) | Diseño |
| [WEEKLY_RECONCILIATION_AGENT](WEEKLY_RECONCILIATION_AGENT.md) | Conciliación opcional |
| [ADOPTION_REPORT](ADOPTION_REPORT.md) | Estado formal de v1.3 |

## Cambios principales de v1.3

- Capability routing como tercera dimensión separada de modo y nivel.
- Clases ROUTER/FOCUSED/ADVANCED/EXPERT/FRONTIER con mapping operativo sustituible.
- Modelos expertos para causa raíz, arquitectura y descomposición; eficientes para ejecución acotada.
- Microtareas por comportamiento verificable, no por archivo/línea.
- Fases y autorización de una, varias o todas las fases sin aprobaciones rituales entre handoffs.
- Delegación interna automática dentro del alcance autorizado, sin alterar RELEASE ni permisos externos.
- Escalamiento sin reiniciar, stop conditions y compatibilidad manual si el runtime no enruta modelos.
- Se conserva el núcleo de despliegue, migraciones, CHECK y RELEASE de v1.2.