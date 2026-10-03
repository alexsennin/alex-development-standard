# ALEX DEVELOPMENT STANDARD v1.1

Metodología personal de desarrollo mediante vibecoding y agentes. Versión 1.1, 2026-10-03. Estado: **ALEX DEVELOPMENT STANDARD v1.1 — aprobado para piloto**. Piloto no iniciado; no adoptado universalmente ni aplicado a otros repositorios.

Este paquete es la fuente normativa de la metodología. No obliga a usar un stack, arquitectura, marca o dominio concretos. Describe cómo comprender, cambiar, verificar, registrar y entregar un proyecto.

## Entrada y mapa

Comenzar por [ENGINEERING_STANDARD.md](ENGINEERING_STANDARD.md), documento raíz normativo.

| Documento | Responsabilidad |
| --- | --- |
| [ENGINEERING_STANDARD](ENGINEERING_STANDARD.md) | Principios, alcance y criterios de terminado |
| [CHANGE_MANAGEMENT](CHANGE_MANAGEMENT.md) | Modos PATCH/FEATURE/SYSTEM/CHECK/RELEASE y economía de contexto |
| [AGENT_WORKFLOW](AGENT_WORKFLOW.md) | Etapas de trabajo y roles conceptuales |
| [CONTEXT_MANAGEMENT](CONTEXT_MANAGEMENT.md) | Contexto persistente y recuperación entre chats |
| [GIT_WORKFLOW](GIT_WORKFLOW.md) | Ramas, commits, publicación y evidencia remota |
| [PROJECT_DOCUMENTATION](PROJECT_DOCUMENTATION.md) | Contratos, ubicación y mantenimiento de documentos del proyecto |
| [SESSION_HANDOFF](SESSION_HANDOFF.md) | Cierre y arranque de una sesión sin pérdida de contexto |
| [DECISION_MANAGEMENT](DECISION_MANAGEMENT.md) | Decisiones, alternativas y sustituciones |
| [TASK_MANAGEMENT](TASK_MANAGEMENT.md) | Tareas concretas, estados y aceptación |
| [TESTING_STANDARD](TESTING_STANDARD.md) | Verificación proporcional y límites de evidencia |
| [DEPLOYMENT_STANDARD](DEPLOYMENT_STANDARD.md) | Destinos, publicación, recuperación y comprobación |
| [DESIGN_STANDARD](DESIGN_STANDARD.md) | Consistencia visual sin imponer identidad |
| [PROJECT_ADOPTION](PROJECT_ADOPTION.md) | Adopción gradual y adaptación a cada repositorio |
| [ADOPTION_REPORT](ADOPTION_REPORT.md) | Resumen ejecutivo, trazabilidad de creación y estado formal |

## Convención de organización en proyectos consumidores

La distribución recomendada es:

```text
<TARGET_ROOT>/
├── AGENTS.md
├── README.md
├── <código/configuración>
└── project-methodology/
    ├── PROJECT_CONTEXT.md
    ├── PROJECT_STATE.md
    ├── ARCHITECTURE.md
    ├── TODO.md
    ├── DECISIONS.md
    ├── ENVIRONMENTS.md        # si aplica
    ├── RELEASE_STATE.md       # si aplica
    └── design/
        ├── DESIGN_SYSTEM.md
        ├── TOKENS.md
        ├── COMPONENTS.md
        └── LAYOUTS.md
```

Reglas:

- `AGENTS.md` permanece en la raíz como puerta de entrada de agentes.
- La memoria persistente específica del proyecto vive en `project-methodology/`.
- Los documentos visuales viven en `project-methodology/design/` sólo cuando aplican.
- No copiar dentro del proyecto consumidor los documentos normativos de este estándar.
- Si un repositorio ya tiene otra ubicación documental válida, puede mapearse explícitamente durante la adopción; evitar dos fuentes que compitan como autoridad.

## Uso de v1.1

Un chat nuevo usa la [Plantilla de inicio de sesión](CONTEXT_MANAGEMENT.md#plantilla-de-inicio-de-sesión), lee `AGENTS.md`, sigue sus enlaces a `project-methodology/`, valida vigencia y aplica el flujo.

La adopción debe indicar la versión de la metodología y adaptaciones locales. No afirmar que un repositorio cumple v1.1 sólo porque contiene nombres de archivo.

La [clasificación por nivel](ENGINEERING_STANDARD.md#niveles-de-cambio) ajusta la carga del proceso. [Actualizar sólo la verdad que cambió](PROJECT_DOCUMENTATION.md#regla-contra-la-sobredocumentación) evita burocracia.


## Cambio principal de v1.1

v1.1 desacopla **riesgo** (niveles 1–4) de **modo operativo**. PATCH/FEATURE permiten iteración focal; CHECK consolida una ronda; RELEASE concentra publicación, migraciones y Producción. El objetivo es conservar rigor sin pagar una auditoría completa en cada corrección.
