# BATCH ROUTING — agrupación y handoff manual de ARC

**Estado:** extensión operativa opcional (no normativa). **Fecha:** 2026-11-13.  
**Norma prevalente:** [CORE](../standards/v1.3.2/CORE.md), [ORCHESTRATION](../standards/v1.3.2/ORCHESTRATION_STANDARD.md), [TASK_MANAGEMENT](../standards/v1.3.2/TASK_MANAGEMENT.md), [SESSION_HANDOFF](../standards/v1.3.2/SESSION_HANDOFF.md).  
**Modelos vigentes:** [MODEL_PROFILE](MODEL_PROFILE.md).

## Objetivo
Permitir que un orquestador revise el backlog, agrupe tareas compatibles en lotes ejecutables, recomiende **al usuario** una capacidad/modelo y entregue un **prompt neutral** que pueda pegarse en cualquier agente. Tras la ejecución, el constructor devuelve un **prompt neutral de auditoría**. No requiere AXIOM, nuevo chat, nueva aplicación ni nuevos archivos por lote.

## Separación estricta: tarjeta de enrutamiento vs. prompt copiable

**Tarjeta para el usuario — nunca copiar al ejecutor:**
- ID del lote, objetivo y tareas.
- Modelo recomendado, esfuerzo y alternativa según disponibilidad.
- Motivo de la elección y cuota/consumo estimado con la incertidumbre correspondiente.
- Estado, dependencias, riesgos y lugar de ejecución elegidos por el usuario, si aporta valor a su propio tablero.

**Prompt copiable — completamente neutral:**
- No nombrar modelo, proveedor, IDE, plataforma o aplicación de IA.
- No preguntar ni discutir con el agente ejecutor dónde se trabaja o qué modelo se usa.
- No incluir instrucciones de cambiar de modelo ni recomendaciones de router.
- Sí incluir repositorio, tarea/IDs, objetivos, contexto/contratos, dependencias, autorización, límites, pruebas y entrega.
- Mantener la decisión **fuera** del texto copiable, incluso para el prompt de retorno.

## Selección del constructor o revisor (sólo tarjeta privada del usuario)

Consultar el catálogo de siete modelos de [MODEL_PROFILE.md](MODEL_PROFILE.md). Orientación resumida:

| Tipo de trabajo | Modelo prioritario | Alternativa |
| --- | --- | --- |
| Clasificar, documentar, cambiar algo mecánico y aislado | GPT-6 Luna | Gemini 3.8 Flash |
| CRUD, UI, validaciones y pruebas corrientes | Gemini 3.8 Flash | GPT-6.1 Terra |
| Construcción entre varios módulos, depuración compleja ya delimitada | Gemini 4 Hydrogen | GPT-6.1 Terra / Gemini 4 Argon si reaparece incertidumbre |
| Arquitectura, contratos entre servicios, análisis de riesgos | GPT-6.1 Sol | Gemini 4 Argon |
| Auditoría de fórmulas financieras, seguridad, migraciones o datos | GPT-6.1 Sol independiente del constructor | Gemini 4 Argon independiente |
| Problema extraordinario no resuelto tras análisis EXPERT | GPT-6 Astra excepcional | Gemini 4 Argon |

Esta tabla **no es parte del prompt**. Valorar cuota restante, contexto disponible, criticidad y rendimiento aprobado histórico; no gastar recursos FRONTIER en cambios simples. Al recomendar, ofrecer alternativa y una sola razón clara. Ante empate práctico, dejar que el usuario seleccione el entorno disponible.

## Algoritmo de preparación de lotes

1. Leer `AGENTS.md`, `PRODUCT_STRATEGY.md` si existe, `project-methodology/TODO.md` y estado vigente. No duplicar tareas existentes.
2. Clasificar cada tarea por modo, nivel 1–4 y capacidad ARC. Verificar dependencias, autorización, compatibilidad de archivos/contratos y pruebas previstas.
3. Ordenar por resultados comerciales/operativos aprobados y dependencias, no por cantidad. Separar análisis EXPERT si falta contrato o fórmula clara.
4. Agrupar inicialmente **3–6 tareas**, pudiendo llegar a 10 sólo cuando estén bien acotadas e independientes. Mantener un objetivo verificable por lote y considerar si los cambios compartirán esquema/archivos.
5. Registrar ID de lote, tareas, estado y siguiente paso en los documentos *ya existentes*, sólo cuando realmente cambien. Proponer modelo/alternativa en **tarjeta externa para el usuario**, nunca en el prompt copiable.
6. El usuario autoriza uno o varios lotes, copia los prompts y decide manualmente dónde y con qué modelo ejecutarlos.
7. El ejecutor completa las tareas autorizadas sin requerir aprobación rutinaria entre microtareas, prueba y corrige dentro del alcance. Si una tarea se bloquea, documenta la causa y continúa sólo con las independientes y seguras.
8. Ejecutar CHECK proporcional, producir resultados y prompt de auditoría. El revisor inspecciona directamente diff/commits y evidencias, no toma el resumen del constructor como prueba. Cierra tareas sólo cuando se cumple aceptación y autorización.
9. Si hay fallas, retornar correcciones acotadas; si hay hechos nuevos o dos intentos sin progreso, replanificar o elevar la tarea afectada. No gastar cuota repetidamente.

**Paradas obligatorias:** cambios materiales de alcance o contrato, migraciones no previstas, permisos/secretos/auth, dinero/datos productivos, operación destructiva, despliegue en Producción o falta de seguridad para revertir. Un lote no concede autorización para RELEASE ni para tareas adicionales.

## Plantilla A — salida del orquestador

### A1. Tarjeta de enrutamiento (SÓLO PARA EL USUARIO; NO COPIAR)

```text
LOTE: [BATCH_ID]
TAREAS: [IDs]
OBJETIVO: [resultado verificable]
MODELO RECOMENDADO: [modelo / esfuerzo]
ALTERNATIVA: [modelo / esfuerzo]
MOTIVO: [capacidad suficiente, riesgo, disponibilidad/cuota, en una frase]
BLOQUEOS/DEPENDENCIAS: [...]
ESTADO: Listo / Requiere contrato / Bloqueado
```

### A2. Prompt de ejecución (COPIAR SOLO ESTE BLOQUE)

```text
ARC — LOTE DE EJECUCIÓN
Lote: [BATCH_ID]
Repositorio: [REPO]
Rama o base autorizada: [BRANCH/REF]
Tareas: [IDs]
Objetivo: [resultado observable]

Consulta AGENTS.md y los archivos de seguimiento pertinentes del repositorio.
Trabaja exclusivamente en las tareas identificadas y respeta sus contratos,
dependencias, límites y criterios de aceptación.

Plan de ejecución: [pasos ordenados y relaciones]
Archivos/contratos relevantes: [referencias exactas]
No modificar: [alcances fuera de autorización]
Criterios de aceptación: [por tarea y del conjunto]
Pruebas esperadas: [comandos/casos, datos ficticios y resultados]

Ejecuta las tareas compatibles del lote sin solicitar confirmación rutinaria
entre ellas; verifica cada resultado y corrige los defectos dentro del alcance.
Si una tarea se bloquea o aparecen hechos incompatibles con el plan, detén sólo
esa parte, registra evidencia y continúa únicamente con trabajo independiente
y seguro. Nunca extrapoles autorización a datos productivos, operaciones
destructivas, migraciones o despliegue.

Al cerrar, revisa los cambios, registra el estado real de cada tarea y
produce el handoff proporcional de ARC. Informa pruebas ejecutadas y omitidas,
archivos modificados, rama, commits, push/remoto si aplica, bloqueos y
siguientes pasos. No consideres aprobada una tarea que requiera auditoría
independiente sólo por haberla implementado.

Termina con un bloque titulado «PROMPT DE AUDITORÍA» listo para copiar.
Este bloque debe ser autosuficiente y contener solo la información necesaria
para la revisión técnica y el seguimiento del lote.
```

## Plantilla B — prompt de retorno del constructor para revisión

El constructor sustituye los marcadores por resultados **reales**, no inventados. Si algún dato no está disponible, declara `No verificado`.

```text
ARC — AUDITORÍA DE LOTE
Lote: [BATCH_ID]
Repositorio: [REPO]
Rama/base: [BRANCH/REF]
Tareas: [IDs y estado reportado por el constructor]
Commits/diff: [SHAs, URLs o referencia local comprobable]
Archivos modificados: [lista]
Criterios de aceptación: [referencias]
Pruebas y resultados: [comandos, salidas significativas, omisiones]
Riesgos y bloqueos: [lista, o ninguno verificado]
Estado Git: [working tree, push, remoto; no inferir]
Autorizaciones relevantes: [existentes y no concedidas]

Audita el trabajo directamente contra el repositorio y los criterios.
Comprueba diff, pruebas, regresiones, contratos, datos, permisos y coherencia
entre tareas. No asumas que la declaración del constructor demuestra éxito.

Para cada tarea devuelve APROBADA, CORRECCIONES o BLOQUEADA, con evidencia
concreta. Actualiza el seguimiento cuando corresponda conforme a ARC.
Si hay correcciones, prepara un nuevo lote acotado con sus criterios,
sin ampliar silenciosamente el alcance. No ejecutes despliegues en Producción.
```

## Pruebas de eficiencia

Medir por lote: tareas **aprobadas**, reintentos, minutos hasta aprobación, cuota restante antes/después cuando sea observable y defectos posteriores. Documentar que los resultados de cuota no son directamente comparables entre suscripciones. Cambiar modelos sin modificar los prompts ni el estándar.

## Límites y compatibilidad

- No introducir un segundo sistema de tickets: `TODO.md` conserva IDs/estados; `PROJECT_STATE.md` resume el siguiente paso; `DECISIONS.md` registra decisiones duraderas.
- Tres chats pueden representar tres áreas; si ejecutan código en paralelo, aislar ramas/worktrees y coordinar cambios compartidos antes de integrar.
- Mantener las distinciones ARC: implementación ≠ auditoría; commit ≠ push; push ≠ merge; merge ≠ despliegue.
- Una tarjeta de ruta no sustituye autorización, control de acceso ni revisión independiente requerida por el nivel.
