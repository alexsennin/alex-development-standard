# ARC Development Standard

**ARC — Adaptive Reasoning & Coding.**

Metodología personal de desarrollo mediante vibecoding y agentes.

## Versión vigente
- [v1.3.2](standards/v1.3.2/README.md) — **vigente / adopción obligatoria** (2026-10-06)
- [v1.3.1](standards/v1.3.1/README.md) — histórica
- [v1.3](standards/v1.3/README.md) — histórica
- [v1.2](standards/v1.2/README.md) — histórica
- [v1.1](standards/v1.1/README.md) — histórica
- [v1.0](standards/v1.0/README.md) — histórica

**Independiente del entorno:** ARC se aplica desde Codex, Antigravity o [AXIOM](standards/v1.3.2/AXIOM_RUNTIME.md) (orquestador opcional). Las mismas reglas y validaciones rigen en cada entorno.

Entrada operativa: [CORE v1.3.2](standards/v1.3.2/CORE.md).

## Operación con modelos y lotes (no normativa)

- [MODEL_PROFILE — catálogo completo de 7 modelos](profiles/MODEL_PROFILE.md): GPT-6 Luna, GPT-6.1 Terra, GPT-6.1 Sol, GPT-6 Astra, Gemini 3.8 Flash, Gemini 4 Hydrogen y Gemini 4 Argon. **Recomendación obligatoria de un modelo concreto y su nivel de pensamiento por cada lote**, con alternativa y motivo, visibles **sólo para el usuario**.
- [BATCH_ROUTING — lotes de ejecución y prompts de ida/vuelta](profiles/BATCH_ROUTING.md): planificación por dependencias, recomendación explícita de modelo + nivel por lote, trabajos compatibles, prompts neutrales, validación independiente y medidas de eficiencia por tarea aprobada.

**SOL hace la recomendación técnica concreta de modelo y pensamiento; el usuario sólo decide si la acepta y selecciona manualmente el entorno disponible.** Los prompts copiables de ejecución y auditoría **no contienen** recomendaciones de modelo, proveedor ni plataforma. La norma ARC v1.3.2 y sus límites de autorización siguen siendo la autoridad; esta operativa es opcional, no exige AXIOM ni autoriza despliegues.