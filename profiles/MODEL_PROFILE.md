# MODEL PROFILE — ARC (perfil operativo multiplataforma)

**Tipo:** perfil operativo no normativo, revisable sin cambiar la versión metodológica de ARC.  
**Revisión:** 2026-11-13.  
**Fuentes normativas:** `standards/v1.3.2/CORE.md`, `ORCHESTRATION_STANDARD.md` y `TASK_MANAGEMENT.md`.  
**Operación por lotes y prompts neutrales:** [BATCH_ROUTING.md](BATCH_ROUTING.md).

## Regla central de enrutamiento

**El modelo y la plataforma son decisión exclusiva del usuario.** El orquestador presenta fuera del prompt una recomendación, alternativa y justificación. **NUNCA insertar nombres de modelos, proveedores, IDE, plataforma ni instrucciones para cambiar de modelo dentro del prompt copiable de ejecución o del prompt de retorno.** El agente receptor únicamente recibe las tareas y los criterios de trabajo; no se le consulta a qué modelo/plataforma enviarlo.

Los nombres de modelos son preferencias del usuario: comprobar disponibilidad en el selector. Elegir el modelo disponible de menor consumo/cuota **por tarea aprobada**, no por tokens aislados. Calidad, intentos, riesgo y límites del plan pueden alterar la recomendación.

## Matriz de trabajo y alternativas

| Trabajo | Recomendación principal | Alternativas según disponibilidad/cuota | Regla |
| --- | --- | --- | --- |
| Arquitectura, contratos de datos, alcance, clasificación EXPERT | GPT-6.1 Sol High | Gemini 4 Argon; GPT-6.1 Terra High para análisis acotado | EXPERT antes de editar si CORE detecta datos, pagos, auth, permisos, migraciones o Producción. |
| Auditoría independiente de lógica financiera, seguridad o cambios delicados | GPT-6.1 Sol High | Otra instancia con capacidad EXPERT y contexto independiente | Revisar evidencia directa y diff; no confiar en el relato del constructor. |
| Construcción corriente: UI, formularios, CRUD, funciones claras, pruebas | Gemini 3.8 Flash High | GPT-6.1 Terra High; GPT-6 Luna para porciones mecánicas acotadas | Mantener Flash cuando la cuota disponible permita más tareas aprobadas. |
| Integración entre módulos y depuración compleja con especificación clara | Gemini Hydrogen High (si está disponible) | GPT-6.1 Terra High; Gemini 3.8 Flash High si hay criterios suficientes; GPT-6.1 Sol para nuevo análisis EXPERT | Hydrogen es preferencia operativa a medir, no ganador universal ni permiso para omitir auditoría. |
| Correcciones focalizadas, cambios visuales concretos, pruebas en varios archivos relacionados | GPT-6.1 Terra High | Gemini 3.8 Flash High; GPT-6.1 Sol si es necesaria nueva arquitectura | Terra como alternativa entre el costo de Luna y la profundidad de Sol. |
| Tareas de alta frecuencia y bajo riesgo: documentación, triage, extracción, ajustes mecánicos | GPT-6 Luna Low/Medium | Gemini 3.8 Flash; GPT-6.1 Terra | No asignarle por defecto una integración autónoma compleja ni operaciones críticas. |
| Problema extraordinariamente ambiguo tras análisis EXPERT y nueva evidencia | Capacidad FRONTIER disponible | GPT-6.1 Sol High/Max u otra opción suficiente | Escalamiento excepcional, no por costumbre. |

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

**No inferir del costo API una cuota real del plan.** La medida de eficiencia operativa es número de tareas o lotes **aprobados**, incluyendo reintentos, tiempo, consumo observado del producto y defectos. Cifras de distintos benchmarks/esfuerzos no son equivalentes. Los cupos se verifican en cada producto.

## Perfil de capacidades ARC (abstracto y estable)

| Capacidad | Enrutamiento sugerido |
| --- | --- |
| ROUTER | GPT-6 Luna Low; Gemini 3.8 Flash |
| FOCUSED | GPT-6 Luna para mecánica acotada; GPT-6.1 Terra o Gemini Flash para cambios de código |
| ADVANCED | GPT-6.1 Terra High, Gemini Flash High, o Hydrogen High si disponible y medido |
| EXPERT | GPT-6.1 Sol High; Gemini 4 Argon como alternativa |
| FRONTIER | Capacidad superior disponible, sólo si evidencia lo exige |

## Límites

- Primero definir problema, dependencias y criterios de aceptación. Después recomendar modelo con motivo breve y alternativa, **fuera del prompt copiable**.
- No agrupar tareas sólo por modelo ni por número. Los lotes necesitan dependencias resueltas, cambios compatibles y aceptación verificable.
- Si dos intentos no aportan evidencia nueva, detener/elevar la tarea; no continuar gastando cuota reiterando el mismo enfoque.
- Si el modelo preferido está agotado, el usuario decide el destino; no interrogar al agente ejecutor sobre plataforma o modelo.
- Ninguna recomendación cambia automáticamente el modelo seleccionado, ni concede autorización para liberar, migrar o editar datos productivos.
- AXIOM es opcional y no requisito de ARC.
