# BATCH ROUTING — agrupación y handoff manual de ARC

**Estado:** extensión operativa opcional (no normativa). **Fecha:** 2026-11-13.  
**Norma prevalente:** [CORE](../standards/v1.3.2/CORE.md), [ORCHESTRATION](../standards/v1.3.2/ORCHESTRATION_STANDARD.md), [TASK_MANAGEMENT](../standards/v1.3.2/TASK_MANAGEMENT.md), [SESSION_HANDOFF](../standards/v1.3.2/SESSION_HANDOFF.md).  
**Modelos vigentes:** [MODEL_PROFILE](MODEL_PROFILE.md).

## Objetivo
Permitir que un orquestador revise el backlog, agrupe tareas compatibles en lotes ejecutables, **seleccione y recomiende explícitamente UN modelo y UN nivel de pensamiento por lote al usuario**, con alternativa argumentada según capacidad, calidad y ahorro esperado por tarea aprobada, y entregue un **prompt neutral** que pueda pegarse en cualquier agente. Tras la ejecución, el constructor **publica el estado y la evidencia en GitHub**; el retorno predeterminado es un **disparador breve y neutral de auditoría**, no la repetición del informe. Un handoff extendido se reserva para casos en que el auditor no pueda acceder a la evidencia. No requiere AXIOM, nuevo chat, nueva aplicación ni nuevos archivos por lote.

## Separación estricta: tarjeta de enrutamiento vs. prompt copiable

**Tarjeta para el usuario — nunca copiar al ejecutor:**
- ID del lote, objetivo y tareas.
- **Recomendación obligatoria y explícita:** modelo principal concreto + nivel de pensamiento recomendado; alternativa concreta + su nivel.
- **Justificación por lote:** por qué ese modelo puede cubrir correctamente todas las tareas con el mejor ahorro razonable; cuándo usar alternativa; confianza y supuestos de cuota, sin cifras inventadas.
- Si se necesita auditoría independiente, **recomendación aparte para el auditor** con nivel y alternativa, también fuera del prompt.
- Estado, dependencias, riesgos y lugar de ejecución elegidos por el usuario, si aporta valor a su propio tablero.

**Prompt copiable — completamente neutral:**
- No nombrar modelo, proveedor, IDE, plataforma o aplicación de IA.
- No preguntar ni discutir con el agente ejecutor dónde se trabaja o qué modelo se usa.
- No incluir instrucciones de cambiar de modelo ni recomendaciones de router.
- En ejecución, sí incluir repositorio, tarea/IDs, objetivos, contexto/contratos, dependencias, autorización, límites, pruebas y entrega.
- En retorno, usar sólo el identificador de lote y rama/ref cuando permitan resolver sin ambigüedad los registros publicados; SOL lee evidencia desde GitHub.
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

Esta tabla **no es parte del prompt**. Valorar cuota restante, contexto disponible, criticidad y rendimiento aprobado histórico; no gastar recursos FRONTIER en cambios simples. **Para cada lote elegir y decir de forma inequívoca «Modelo recomendado: X — Pensamiento: Y», además de la alternativa concreta con su nivel**. Indicar en una o dos frases por qué maximiza el trabajo bien aprobado por cuota esperada. No vale responder sólo «elige el modelo y esfuerzo disponible», presentar toda la tabla sin elegir, ni delegar al usuario el juicio técnico. El usuario sólo elige manualmente si acepta esa recomendación y dónde ejecutarla.

## Algoritmo de preparación de lotes

1. Leer `AGENTS.md`, `PRODUCT_STRATEGY.md` si existe, `project-methodology/TODO.md` y estado vigente. No duplicar tareas existentes.
2. Clasificar cada tarea por modo, nivel 1–4 y capacidad ARC. Verificar dependencias, autorización, compatibilidad de archivos/contratos y pruebas previstas.
3. Ordenar por resultados comerciales/operativos aprobados y dependencias, no por cantidad. Separar análisis EXPERT si falta contrato o fórmula clara.
4. Agrupar inicialmente **3–6 tareas**, pudiendo llegar a 10 sólo cuando estén bien acotadas e independientes. Mantener un objetivo verificable por lote y considerar si los cambios compartirán esquema/archivos.
5. Registrar ID de lote, tareas, estado y siguiente paso en los documentos *ya existentes*, sólo cuando realmente cambien. **Emitir obligatoriamente una recomendación principal y una alternativa con niveles concretos de pensamiento por cada lote**, fuera del prompt copiable; cuando el nivel exacto no esté verificado en el selector, declarar esa incertidumbre en la tarjeta. Si la dificultad de un lote exigiría gastar capacidad superior sólo para algunas tareas, dividirlo.
6. El usuario autoriza uno o varios lotes, copia los prompts y decide manualmente dónde y con qué modelo ejecutarlos.
7. El ejecutor completa las tareas autorizadas sin requerir aprobación rutinaria entre microtareas, prueba y corrige dentro del alcance. Si una tarea se bloquea, documenta la causa y continúa sólo con las independientes y seguras.
8. Ejecutar CHECK proporcional; registrar en los archivos existentes de ARC el lote ejecutado, su estado **pendiente de auditoría**, rama, SHAs, criterios, pruebas/resultados y bloqueos, sin inventar verificaciones. Crear commit y hacer push al remoto autorizado cuando corresponda; confirmar la referencia publicada. El retorno al usuario es un disparador breve de auditoría con lote y rama, no un nuevo informe extenso. Si no hay evidencia publicada y verificable, declarar «No publicado / no verificable en GitHub» y entregar handoff proporcional como excepción.
9. El auditor ubica el lote y la referencia exacta en GitHub, verifica diff/commits, contratos y pruebas; no confía en resúmenes del constructor. Cierra tareas sólo cuando se cumple aceptación y autorización.
10. Si hay fallas, retornar correcciones acotadas; si hay hechos nuevos o dos intentos sin progreso, replanificar o elevar la tarea afectada. No gastar cuota repetidamente.

**Paradas obligatorias:** cambios materiales de alcance o contrato, migraciones no previstas, permisos/secretos/auth, dinero/datos productivos, operación destructiva, despliegue en Producción o falta de seguridad para revertir. Un lote no concede autorización para RELEASE ni para tareas adicionales.

## Requisito de aceptación de una respuesta del orquestador

La respuesta **NO está completa** hasta que **todos los lotes propuestos** tengan una recomendación concreta y su nivel de pensamiento. Una lista de candidatos, una tabla genérica de modelos o una frase como «estas recomendaciones son para que tú elijas el modelo y esfuerzo disponible» no cumple la petición.

El orquestador **hace el análisis técnico y recomienda**. El usuario solo toma la decisión de disponibilidad/ejecución. Incluir un único modelo principal por lote (con alternativa) fuera del prompt; si hay auditoría, recomendar por separado un modelo concreto para la auditoría. No preguntar al constructor por plataforma, cuota o modelo.

Si no hay evidencia para cuantificar ahorro, justificarlo cualitativamente y proponer medirlo; no inventar límites de cuota, precios o porcentajes de rendimiento.

## Plantilla A — salida del orquestador

### A1. Tarjeta de enrutamiento (SÓLO PARA EL USUARIO; NO COPIAR)

```text
LOTE: [BATCH_ID]
TAREAS: [IDs]
OBJETIVO: [resultado verificable]
MODELO RECOMENDADO: [nombre específico de UN modelo]
NIVEL DE PENSAMIENTO: [Low / Medium / High / nivel real del selector]
ALTERNATIVA: [nombre específico de UN modelo] — [nivel de pensamiento]
POR QUÉ ES LA MEJOR RELACIÓN CALIDAD/CUOTA: [1–2 frases: complejidad, riesgo, reintentos y rendimiento por lote aprobado]
CUÁNDO USAR ALTERNATIVA: [motivo concreto]
RECOMENDACIÓN DE AUDITORÍA SI APLICA: [modelo + pensamiento] — [alternativa + pensamiento]
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

Deja registrados en el seguimiento de ARC el lote, rama/ref, commits,
pruebas y resultado, y sincroniza con el remoto autorizado cuando corresponda.
No afirmes que el auditor tiene acceso a cambios sólo locales o no publicados.
Termina con «PROMPT DE AUDITORÍA» breve, listo para copiar, que indique el
lote y la rama/ref necesarios para consultar GitHub. Sólo adjunta un handoff
más detallado si los cambios no quedaron publicados o falta acceso a ellos.
```

## Plantilla B — retorno Git-first (predeterminada)

**GitHub remoto es la fuente única de verdad compartida.** Los archivos locales son un espacio de trabajo y los chats no conservan un estado autoritativo. Toda tarea lista para auditoría remota debe identificar de forma verificable la **rama/ref publicada**, el **ID del lote**, las **tareas** y los **SHAs** pertinentes en el seguimiento de ese repositorio. Mantener allí también resultados de pruebas, pendientes y criterios de aceptación; no duplicar documentos si ya existe un tablero o registro válido.

No asumir que «el último lote» es inequívoco cuando hay múltiples ramas o tres frentes concurrentes. Si hay más de un lote pendiente de auditoría, usar **ID + rama/ref**. La publicación en GitHub **no equivale** a despliegue y nunca lo autoriza.

### B1. Prompt breve de retorno (siempre que el estado esté publicado y accesible)

```text
ARC — REVISIÓN DE LOTE
Revisa el lote [BATCH_ID] de la rama [BRANCH/REF] usando
el estado y la evidencia publicados en el repositorio [REPO].
Comprueba los cambios y las pruebas, dicta el estado de cada
tarea y actualiza el seguimiento conforme a ARC.
Prepara correcciones o el siguiente paso según el resultado.
```

Si un proyecto contiene un único lote pendiente de auditoría y su rama está inequívocamente establecida, puede bastar: «Revisa el último lote pendiente de auditoría conforme a ARC y actualiza el seguimiento». No usar esa forma si existen varios candidatos.

### B2. Excepción: no hay evidencia remota verificable

Cuando el constructor sólo dispone de cambios locales, commits no publicados, working tree sucio o un remoto inaccesible, debe indicarlo **explícitamente**. No declarar un lote «listo para auditoría remota» ni inventar SHAs publicados. Entregar un handoff proporcional de [SESSION_HANDOFF.md](../standards/v1.3.2/SESSION_HANDOFF.md), que incluya datos realmente comprobados y explique qué resta sincronizar. El auditor sólo evalúa lo que realmente puede acceder; puede requerir la misma carpeta de trabajo o solicitar publicación/traspaso autorizado.

### B3. Regla de auditoría

El auditor debe comprobar **la versión exacta** y no limitarse a leer el tablero: revisar commits/diff y ejecutar o contrastar pruebas pertinentes cuando disponga de acceso. Para cada tarea emitir APROBADA, CORRECCIONES o BLOQUEADA con evidencias, y actualizar el estado en el repositorio autorizado. No aprobar automáticamente por un «completado» del constructor; no realizar RELEASE sin autorización explícita.

## Pruebas de eficiencia

Medir por lote: tareas **aprobadas**, reintentos, minutos hasta aprobación, cuota restante antes/después cuando sea observable y defectos posteriores. Documentar que los resultados de cuota no son directamente comparables entre suscripciones. Cambiar modelos sin modificar los prompts ni el estándar.

## Límites y compatibilidad

- No introducir un segundo sistema de tickets: `TODO.md` o el tablero existente conserva IDs/estados; `PROJECT_STATE.md` resume el siguiente paso; `DECISIONS.md` registra decisiones duraderas. Registrar allí el lote pendiente de auditoría, SHAs y evidencia de forma recuperable.
- Tres chats pueden representar tres áreas; si ejecutan código en paralelo, aislar ramas/worktrees y coordinar cambios compartidos antes de integrar.
- Mantener las distinciones ARC: implementación ≠ auditoría; commit ≠ push; push ≠ merge; merge ≠ despliegue.
- Una tarjeta de ruta no sustituye autorización, control de acceso ni revisión independiente requerida por el nivel.
