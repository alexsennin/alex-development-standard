# MODEL PROFILE — ARC (perfil operativo multiplataforma)

**Tipo:** perfil operativo no normativo, revisable sin cambiar la versión metodológica de ARC.  
**Revisión:** 2026-11-13.  
**Fuentes normativas:** `standards/v1.3.2/CORE.md`, `ORCHESTRATION_STANDARD.md` y `TASK_MANAGEMENT.md`.  
**Operación por lotes y prompts neutrales:** [BATCH_ROUTING.md](BATCH_ROUTING.md).

## Regla central de enrutamiento

**OBLIGACIÓN DEL ORQUESTADOR: recomendar, no limitarse a ofrecer opciones.** Para **cada lote**, antes de mostrar el prompt copiable, emitir una **recomendación concreta de un modelo y su nivel/esfuerzo de pensamiento**, más **una alternativa concreta con su nivel** y un argumento breve de calidad/eficiencia. El análisis de qué IA conviene se hace **por el orquestador**, no por el usuario ni por el agente ejecutor. Debe decir literalmente qué modelo recomienda para ese lote y por qué. Frases como «estas recomendaciones son para que tú elijas el modelo y esfuerzo disponible», si no van acompañadas de una recomendación real y específica, **NO cumplen** este contrato.

**El usuario sólo toma la decisión operativa final de qué modelo y plataforma seleccionar**, según su cuota real y disponibilidad. No debe tener que analizar por su cuenta cuál conviene, ni responder preguntas sobre dónde se ejecutará. Una alternativa nunca sustituye a la recomendación principal.

**NUNCA insertar nombres de modelos, proveedores, IDE, plataforma, esfuerzo de pensamiento ni instrucciones para cambiar de modelo dentro del prompt copiable de ejecución o del prompt de retorno.** La tarjeta de recomendación es un bloque separado para el usuario; el ejecutor recibe únicamente tareas, contexto y criterios técnicos.

Los nombres de modelos son preferencias del usuario: comprobar disponibilidad real en el selector cuando sea posible. Recomendar el modelo de **mejor rendimiento esperado por lote aprobado**, con la **menor cuota/costo razonable sin degradar calidad**, no el mínimo de tokens por sí solo. Considerar complejidad, riesgos, probabilidad de reintentos y si el beneficio de un modelo superior justifica el consumo. No inventar cuota ni ahorro cuantitativo cuando no se conoce. Si no se puede comprobar disponibilidad, emitir igualmente la mejor recomendación técnica y una alternativa; anotar «disponibilidad por verificar» únicamente en la tarjeta externa.

## Contrato obligatorio de salida por lote (para el usuario; fuera del prompt)

Cada lote listo para ejecutar debe presentar esta estructura con **valores rellenados, no placeholders**:

```text
LOTE: [id real] — [resultado concreto]
MODELO RECOMENDADO: [nombre exacto] — [Low / Medium / High / esfuerzo real]
ALTERNATIVA: [nombre exacto] — [nivel/esfuerzo]
POR QUÉ ÉSTE: [1–2 frases sobre probabilidad de completar correctamente, necesidad de razonamiento y cuota por lote aprobado]
CUÁNDO USAR LA ALTERNATIVA: [cuota agotada, disponibilidad o cambio de complejidad]
CONFIANZA: [alta / media / baja, según evidencia]
```

- **Prohibido** presentar sólo un catálogo, una comparación o la frase «tú eliges» sin seleccionar primero **una** opción recomendada y su nivel. Debe quedar claro qué conviene usar **ahora** para ese trabajo.
- Para un lote de varias tareas, elegir un modelo que cubra correctamente el **conjunto**; si se mezclan tareas con dificultades incompatibles, **separar lotes** en vez de forzar un modelo caro para todo.
- El nivel de pensamiento importa: sugerir el **menor nivel suficiente** (Low, Medium, High o el nivel que realmente ofrezca el selector); no poner High automáticamente. Si el nivel no está confirmado, marcarlo como «nivel a comprobar en selector» en la tarjeta, jamás inventar un nivel.
- **Ejecución y auditoría pueden requerir recomendaciones distintas**; cuando el lote requiera auditor independiente, incluir una segunda recomendación concreta para la revisión con nivel y alternativa. Esta recomendación tampoco entra al prompt de retorno.
- La elección manual del usuario nunca elimina la obligación de razonar y recomendar por parte del orquestador.

## Matriz de trabajo y alternativas

| Trabajo | Recomendación principal | Alternativas según disponibilidad/cuota | Regla |
| --- | --- | --- | --- |
| Arquitectura, contratos de datos, alcance, clasificación EXPERT | GPT-6.1 Sol High | Gemini 4 Argon High; GPT-6.1 Terra High para análisis acotado | EXPERT antes de editar si CORE detecta datos, pagos, auth, permisos, migraciones o Producción. |
| Auditoría independiente de lógica financiera, seguridad o cambios delicados | GPT-6.1 Sol High | Gemini 4 Argon High en contexto independiente; GPT-6 Astra excepcionalmente | Revisar evidencia directa y diff; no confiar en el relato del constructor. |
| Construcción corriente: UI, formularios, CRUD, funciones claras, pruebas | Gemini 3.8 Flash High | GPT-6.1 Terra High; GPT-6 Luna para porciones mecánicas acotadas | Preferir Flash cuando su cuota permita mayor rendimiento por tarea aprobada. |
| Integración entre módulos y depuración compleja con especificación clara | Gemini 4 Hydrogen High (si está disponible) | GPT-6.1 Terra High; Gemini 4 Argon High si continúa incertidumbre | Hydrogen es preferencia operativa a medir, no ganador universal ni permiso para omitir auditoría. |
| Correcciones focalizadas, cambios visuales concretos, pruebas en varios archivos relacionados | GPT-6.1 Terra High | Gemini 3.8 Flash High; GPT-6.1 Sol High si exige nueva arquitectura | Terra es alternativa intermedia para sesiones de construcción acotadas. |
| Tareas de alta frecuencia y bajo riesgo: documentación, triage, extracción, ajustes mecánicos | GPT-6 Luna Low/Medium | Gemini 3.8 Flash; GPT-6.1 Terra | No asignarle por defecto integraciones complejas ni operaciones críticas. |
| Diagnóstico de gran alcance, arquitectura transversal difícil o revisión experta alternativa | Gemini 4 Argon High | GPT-6.1 Sol High; GPT-6 Astra sólo si el bloqueo lo justifica | Reserva Argon para tareas donde el análisis experto reduzca reintentos o riesgos; comprobar cuota real. |
| Problema excepcionalmente ambiguo o no resuelto tras EXPERT con nueva evidencia | GPT-6 Astra (si disponible y justificado) | Gemini 4 Argon High; GPT-6.1 Sol High | FRONTIER es excepcional: registrar hipótesis, evidencia e intentos; evitar consumo excesivo de Plus. |

## Catálogo completo para decisión del usuario

El perfil incluye **siete modelos**. El catálogo no asigna modelos automáticamente y no debe filtrarse a los prompts copiables.

| Modelo | Capacidad ARC de uso típico | Función preferida | Condición de uso |
| --- | --- | --- | --- |
| **GPT-6 Luna** (Low/Medium) | ROUTER / FOCUSED | Clasificación, documentación y cambios mecánicos de bajo riesgo | Priorizar volumen de tareas simples; escalar si se vuelve compleja. |
| **GPT-6.1 Terra** (High) | FOCUSED / ADVANCED | Ejecución técnica intermedia, depuración concreta, pruebas y refactor focal | Alternativa eficiente cuando Flash no está disponible o conviene usar Codex. |
| **GPT-6.1 Sol** (High) | EXPERT | Orquestador principal, arquitectura, definición de contratos y auditoría independiente | Reservar para decisiones/revisión difíciles, no construcción mecánica de cada tarea. |
| **GPT-6 Astra** | FRONTIER | Desbloqueo excepcional y análisis/auditoría de máxima dificultad | Cuota Plus más restringida; no usar de forma rutinaria. |
| **Gemini 3.8 Flash** (High) | FOCUSED / ADVANCED | Constructor habitual, UI, CRUD, pruebas y ciclos prolongados de ejecución | Preferido si el usuario dispone de suficiente cuota y la tarea es clara. |
| **Gemini 4 Hydrogen** (High) | ADVANCED | Construcción compleja, integraciones y depuración con varias piezas | Medir eficiencia real por lote aprobado frente a Flash/Terra. |
| **Gemini 4 Argon** (High, según selector) | EXPERT / FRONTIER condicionado | Arquitectura exigente, incertidumbre compleja y revisión de alto riesgo | Escalar solo si aporta valor y existe cuota; no confundir con Hydrogen. |

No son rangos absolutos: una actividad de riesgo elevado obliga a cumplir los controles de ARC aunque la implementación use un ejecutor más económico.

**Separación de fases:** una tarea puede tener *análisis EXPERT*, *ejecución FOCUSED/ADVANCED* y *auditoría EXPERT*. Es un plan interno de enrutamiento, no una instrucción para que el constructor negocie qué modelo ejecutará la tarea.

## Comparación verificada (orientativa, no contractual)

Artificial Analysis (comparativas publicadas, razonamiento **High**) informa:

| Modelo | Intelligence Index | Terminal-Bench 4.0 | FrontierCode-AA 2.0 | Costo estimado por tarea de su evaluación | Tokens de salida por tarea |
| --- | ---: | ---: | ---: | ---: | ---: |
| GPT-6.1 Sol High | 50 | 51.5% | 36.7% | USD 0.59 | 22.6k |
| GPT-6.1 Terra High | 42 | 41.9% | 37.5% | USD 0.26 | 16.7k |
| GPT-6 Luna High | 21 | 4.5% | 18.6% | USD 0.07 | 32.8k |

Fuentes:
- https://artificialanalysis.ai/models/comparisons/gpt-6-1-terra-high-vs-gpt-6-1-sol-high
- https://artificialanalysis.ai/models/comparisons/gpt-6-1-terra-high-vs-gpt-6-luna-high
- https://developers.openai.com/api/docs/guides/model-selection
- https://help.openai.com/en/articles/20001516-managing-usage-with-gpt-6-astra-in-work-and-codex

### Referencias adicionales: Argon y Astra (evaluaciones de fabricantes)

La ficha de Gemini 4 Argon publicada por Google DeepMind (octubre de 2026) incluye esta comparación **dentro del mismo marco de evaluación**:

| Benchmark | Gemini 4 Argon | GPT-6 Astra |
| --- | ---: | ---: |
| DeepSWE v1.1 | 77.9% | 74.1% |
| FrontierSWE v2 | 55.0% | 65.5% |
| Terminal-Bench 4.0 | 57.4% | 58.2% |
| Vibe Code Bench | 91.9% | 89.6% |

Fuente primaria: https://deepmind.google/models/model-cards/gemini-4-argon/  
Fuente de Astra: https://openai.com/index/gpt-6-astra/

**Advertencia:** las tablas de fabricante son evidencia orientativa, no prueba de que un modelo sea mejor en todos los proyectos. No mezclar resultados de diferentes versiones de benchmark, niveles de esfuerzo o plataformas.

### Cuotas y rendimiento real por tarea

OpenAI documenta para Plus una referencia aproximada por ventana de cinco horas de **5–45 mensajes locales con Astra**, **15–160 con GPT-6.1 Sol** y **350–3,000 con GPT-6 Luna**, además de posibles límites semanales. No usar estas cifras para pronosticar con precisión el número de tareas completadas; pueden variar según carga y plan. No hay equivalencia autorizada aquí para Terra, Hydrogen, Flash o Argon.

Fuente: https://help.openai.com/en/articles/20001516-managing-usage-with-gpt-6-astra-in-work-and-codex

Para enrutar, considerar la disponibilidad real y medir **tareas aprobadas por cuota consumida**, reintentos, duración y errores. Un modelo que utiliza más tokens por intento puede ser más eficiente si termina el lote sin retrabajo.

**No inferir del costo API una cuota real del plan.** La medida de eficiencia operativa es número de tareas o lotes **aprobados**, incluyendo reintentos, tiempo, consumo observado del producto y defectos. Cifras de distintos benchmarks/esfuerzos no son equivalentes. Los cupos se verifican en cada producto.

## Perfil de capacidades ARC (abstracto y estable)

| Capacidad | Enrutamiento sugerido |
| --- | --- |
| ROUTER | GPT-6 Luna Low; Gemini 3.8 Flash |
| FOCUSED | GPT-6 Luna para mecánica acotada; GPT-6.1 Terra o Gemini Flash para cambios de código |
| ADVANCED | GPT-6.1 Terra High, Gemini Flash High, o Hydrogen High si disponible y medido |
| EXPERT | GPT-6.1 Sol High; Gemini 4 Argon High como alternativa avanzada |
| FRONTIER | GPT-6 Astra o Gemini 4 Argon si el caso y la cuota justifican escalar |

## Límites

- Primero definir problema, dependencias y criterios de aceptación. Después recomendar **un modelo y un nivel de pensamiento específicos** con alternativa y motivo breve, **fuera del prompt copiable**. **No entregar lotes sin recomendación concreta.**
- No agrupar tareas sólo por modelo ni por número. Los lotes necesitan dependencias resueltas, cambios compatibles y aceptación verificable.
- Si dos intentos no aportan evidencia nueva, detener/elevar la tarea; no continuar gastando cuota reiterando el mismo enfoque.
- Si el modelo preferido está agotado, el usuario decide el destino; no interrogar al agente ejecutor sobre plataforma o modelo.
- Ninguna recomendación cambia automáticamente el modelo seleccionado, ni concede autorización para liberar, migrar o editar datos productivos.
- AXIOM es opcional y no requisito de ARC.
