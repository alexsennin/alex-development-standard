# ARC DEVELOPMENT STANDARD v1.3.2

Versión 1.3.2, 2026-10-06. Estado: **vigente y de adopción obligatoria para todo trabajo nuevo o activo bajo ARC Development Standard**.

v1.3.2 introdujo **AXIOM — Development Orchestration Runtime**. Ajuste de compatibilidad: ARC es independiente de su herramienta de ejecución; AXIOM continúa disponible de forma opcional. v1.3.1 queda histórica.

## Entrada
1. Leer [CORE.md](CORE.md).
2. Leer `AGENTS.md` del proyecto y aplicar el perfil de modelos según el entorno disponible.
3. Cargar sólo documentos especializados indicados por CORE.
4. Solo si se usa AXIOM, consultar [AXIOM_RUNTIME.md](AXIOM_RUNTIME.md).

## Entornos compatibles
- **Codex:** aplicación o CLI; selección de modelo según disponibilidad y perfil operativo.
- **Antigravity:** aplicación de agentes; mismas reglas, tareas, autorizaciones y comprobaciones.
- **AXIOM + Codex CLI:** orquestación automática opcional; su propio contrato está en AXIOM_RUNTIME.

Ningún entorno es requisito para adoptar ARC. No suponer que cambiar una recomendación de modelo modifica el selector de la aplicación.

Perfil operativo vigente: [MODEL_PROFILE](../../profiles/MODEL_PROFILE.md).

Los proyectos nuevos adoptan v1.3.2 desde el inicio. Los proyectos activos bajo ARC Development Standard deben adoptarla antes de su siguiente cambio sustantivo.