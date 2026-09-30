# ALEX DEVELOPMENT STANDARD v1.0

Metodología personal de desarrollo mediante vibecoding y agentes. Versión 1.0, 2026-09-30. Estado: **ALEX DEVELOPMENT STANDARD v1.0 — aprobado para piloto**, por instrucción de Alex tras esta revisión. Piloto no iniciado; no adoptado universalmente ni aplicado a otros repositorios.

Este paquete se aloja en el repositorio de referencia, pero no obliga a usar su stack, arquitectura, marca o dominio. Describe cómo comprender, cambiar, verificar, registrar y entregar un proyecto. No instala una skill ni migra código.

## Entrada y mapa

Comenzar por [ENGINEERING_STANDARD.md](ENGINEERING_STANDARD.md), documento raíz normativo. “Debe” es requisito; “recomendado” admite adaptación justificada; “cuando aplica” exige comprobar la condición. Una excepción se registra con razón, responsable, alcance, riesgo y revisión pendiente; no se oculta como cumplimiento.

| Documento | Responsabilidad |
| --- | --- |
| [ENGINEERING_STANDARD](ENGINEERING_STANDARD.md) | Principios, alcance y criterios de terminado |
| [AGENT_WORKFLOW](AGENT_WORKFLOW.md) | Etapas de trabajo y roles conceptuales |
| [CONTEXT_MANAGEMENT](CONTEXT_MANAGEMENT.md) | Contexto persistente y recuperación entre chats |
| [GIT_WORKFLOW](GIT_WORKFLOW.md) | Ramas, commits, publicación y evidencia remota |
| [PROJECT_DOCUMENTATION](PROJECT_DOCUMENTATION.md) | Contratos y mantenimiento de documentos del proyecto |
| [SESSION_HANDOFF](SESSION_HANDOFF.md) | Cierre y arranque de una sesión sin pérdida de contexto |
| [DECISION_MANAGEMENT](DECISION_MANAGEMENT.md) | Decisiones, alternativas y sustituciones |
| [TASK_MANAGEMENT](TASK_MANAGEMENT.md) | Tareas concretas, estados y aceptación |
| [TESTING_STANDARD](TESTING_STANDARD.md) | Verificación proporcional y límites de evidencia |
| [DEPLOYMENT_STANDARD](DEPLOYMENT_STANDARD.md) | Destinos, publicación, recuperación y comprobación |
| [DESIGN_STANDARD](DESIGN_STANDARD.md) | Consistencia visual sin imponer identidad |
| [PROJECT_ADOPTION](PROJECT_ADOPTION.md) | Adopción gradual y adaptación a cada repositorio |
| [ADOPTION_REPORT](ADOPTION_REPORT.md) | Resumen ejecutivo, trazabilidad de creación y estado formal |

Cada documento tiene un propietario temático; las reglas detalladas se enlazan, no se copian en cada archivo. Los documentos de un proyecto describen ese proyecto; este paquete describe la metodología.

## Clasificación de lo aprendido antes de abstraer

Origen: revisión de los once documentos de extracción de la primera fase, base dd7fe7f. Esta tabla explica la derivación; no constituye configuración que deba instalarse en otros proyectos.

| Categoría | Evidencia del proyecto de referencia | Tratamiento en v1 |
| --- | --- | --- |
| Universal | Contexto en archivos, tareas verificables, cambios pequeños, permisos aplicados por autoridad, minimización de datos, evidencia de cierre | Convertir en principios y procedimientos adaptables |
| Dependiente del stack | App Router, clientes SSR, RLS/RPC/Edge Functions, scripts npm, versiones y herramientas de CI | Definir responsabilidad/resultado; comandos y tecnología se eligen al adoptar |
| Dependiente del dominio | Reglas escolares, ciclos/grupos, Diario, prendas/tallas, folios y excepción de stock negativo | Excluir del núcleo; registrar en contexto/decisiones del proyecto que las necesite |
| Visual/identidad | Logo, Nunito, paleta, medidas, navegación horizontal, radios y breakpoints | No copiar valores; exigir diseño documentado y coherente con identidad propia |
| Deuda técnica | Dashboard concentrado, helpers duplicados, CSS acumulado, documentos contradictorios, E2E condicionada, paginación incompleta | Registrar como problemas; no convertir estructura o carencia en convención |

AGENTS aporta disciplina; PROJECT_CONTEXT, contexto estable; PROJECT_STATE, necesidad de una fotografía presente; ARCHITECTURE, separación actual/objetivo; TODO y DECISIONS, trazabilidad; DESIGN_SYSTEM/TOKENS/COMPONENTS/LAYOUTS, método de diseño; REPORT_STANDARD, límites de la extracción. Se abstraen responsabilidades, no se copian esos archivos como plantillas.

## Uso de v1.0

Un chat nuevo usa la [Plantilla de inicio de sesión](CONTEXT_MANAGEMENT.md#plantilla-de-inicio-de-sesión), lee los documentos del proyecto, valida su vigencia y aplica el flujo. La adopción debe indicar versión de la metodología y adaptaciones locales. No afirmar que un repositorio cumple v1 sólo porque contiene los nombres de archivo.

Cambios al estándar: registrar motivo y compatibilidad en una propuesta revisable. Conservar esta versión en Git; una versión siguiente debe indicar qué reglas cambian. No actualizar otros proyectos automáticamente.

La [clasificación por nivel](ENGINEERING_STANDARD.md#niveles-de-cambio) ajusta la carga del proceso. [Actualizar sólo la verdad que cambió](PROJECT_DOCUMENTATION.md#regla-contra-la-sobredocumentación) evita burocracia. El [reporte ejecutivo](ADOPTION_REPORT.md) registra el cierre de v1.0 y los puntos aún sujetos a validación humana.