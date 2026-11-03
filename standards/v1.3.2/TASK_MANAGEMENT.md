# Gestión de tareas

Toda tarea debe explicar un problema o resultado concreto y cómo se demostrará. TODO.md mantiene futuro y trabajo en curso, no conversaciones.

## Campos mínimos

| Campo | Responsabilidad |
| --- | --- |
| ID | Identificador estable y único dentro del proyecto |
| Prioridad | Urgencia/impacto con criterio del proyecto; no confundir prioridad con orden |
| Problema | Qué falla/falta, quién lo necesita y evidencia disponible |
| Dependencia | Dato, decisión, tarea o autorización necesaria; “ninguna” si aplica |
| Criterio de aceptación | Resultado observable y método para demostrarlo |
| Estado | Pendiente, en curso, bloqueada, en revisión o cerrada |

Añadir responsable, alcance/archivos, restricciones y referencias cuando ayudan. Los criterios no deben reproducir la implementación: “se añadió la función” no demuestra que resuelva el problema.

## Aplicar el nivel de cambio

Usar la [clasificación principal](ENGINEERING_STANDARD.md#niveles-de-cambio) para definir análisis, aceptación, pruebas, revisión y recuperación. Registrar el nivel en la tarea/handoff cuando aporta claridad; no añadir un formulario nuevo. Un Nivel 1 puede tener objetivo/aceptación breves en el diff o handoff, sin entrada artificial en TODO. Para niveles 2–4 mantener tarea trazable con profundidad proporcional.

Reclasificar si crecen riesgo, destino o consecuencias durante la sesión; resolver dependencias de autorización/recuperación antes de continuar la operación afectada. La prioridad ordena necesidades; el nivel determina carga de verificación, no urgencia.

## Ejemplo independiente del dominio

| ID | Prioridad | Problema | Dependencia | Aceptación | Estado |
| --- | --- | --- | --- | --- | --- |
| EXP-01 | Alta | Exportación pierde registros cuando el resultado supera una página | Contrato de paginación comprobado | Dataset ficticio multipágina se exporta completo sin duplicados; consulta no autorizada se rechaza | Pendiente |

“Mejorar UI” debe concretarse en una fricción observable, por ejemplo que una acción quede inaccesible al ancho mínimo soportado; aceptación: acción visible/usable por teclado y sin pérdida de datos en ese ancho.

## Estados y avance

Pendiente → en curso → en revisión → cerrada. Bloqueada indica condición externa concreta y siguiente acción para desbloquear; no usarlo sólo porque el trabajo es difícil. Definir qué revisión falta y quién la realiza. Cerrada requiere aceptación comprobada y cierre correspondiente; si el despliegue queda fuera, explicitar que el entregable está cerrado local/remoto y mantener una tarea de despliegue separada cuando hay trabajo futuro concreto.

Sólo iniciar dependencias resueltas o partes independientes. Actualizar estado con evidencia al finalizar sesión. Las tareas cerradas pueden salir de lista activa con referencia Git/decisión; no acumular backlog histórico ilimitado.

## Alcance y cambio

Dividir tareas grandes por unidades de comportamiento verificables. No dividir sólo por archivo si deja resultados incoherentes. Si surge trabajo fuera del objetivo, registrarlo y priorizarlo; no resolverlo silenciosamente salvo que sea necesario y ya autorizado para cumplir aceptación.

Una tarea documental requiere exactitud, referencias y contexto recuperable. Una tarea de datos requiere evidencia de integridad y destino. Elegir pruebas con [TESTING_STANDARD.md](TESTING_STANDARD.md).
## Microtareas para ejecución asistida

Cuando una tarea grande se descompone para asignar capacidad, cada microtarea debe seguir siendo una **unidad de comportamiento verificable**, no una línea, archivo o acción mecánica aislada. Debe incluir objetivo, contexto mínimo, límites, criterio de aceptación y dependencias suficientes para que otro agente pueda ejecutarla sin redescubrir la arquitectura.

Ejemplo adecuado: «evitar doble envío desde la interfaz», incluyendo estado, bloqueo, manejo de error y prueba de doble clic. Ejemplos demasiado finos: «crear variable», «añadir import», «cambiar línea 42».

Las microtareas pueden agruparse en fases. Una fase debe producir un estado coherente y verificable; no dividir por modelo si esa división deja el sistema inconsistente. La asignación de capacidad/modelo es metadato operativo y no sustituye problema, aceptación ni estado de la tarea.

## Evaluador de tarea: modelo recomendado

Durante la maquetación, apuntes y definición de tareas, el agente que esté activo puede **recomendar** un modelo para cada tarea antes de implementarla. Esto no crea un agente adicional, no exige AXIOM y funciona tanto en Codex como en Antigravity. La recomendación es metadato operativo: **no sustituye** modo, nivel de cambio, capacidad, criterios de aceptación, autorizaciones ni validaciones del Standard.

Añadir a la tarea el campo **Modelo recomendado** cuando ayude a decidir dónde ejecutarla. Formato breve: `Modelo recomendado: [modelo] — [motivo en una frase]`. Si el trabajo todavía es demasiado ambiguo, registrar `Por evaluar` y concretar primero el resultado esperado.

### Catálogo inicial de modelos (perfil práctico, revisable)

| Modelo | Recomendación inicial |
| --- | --- |
| Gemini 3.8 Flash | Ejecución habitual: UI, componentes, cambios localizados, pruebas, documentación y funciones bien especificadas. |
| GPT-6.1 Terra | Alternativa eficiente desde Codex para tareas focalizadas y ejecución con instrucciones claras. |
| GPT-6.1 Sol | Diagnóstico complejo, decisiones de arquitectura, análisis de impacto, migraciones delicadas y revisión de alto riesgo. |
| Gemini 4 Argon | Alternativa de razonamiento avanzado en Antigravity para arquitectura, depuración difícil o problemas de varios módulos. |

Estas asignaciones son **hipótesis operativas**, no una clasificación definitiva de rendimiento. No asumir que Argon o Sol es superior en todas las tareas. Elegir el modelo de **menor costo/cuota esperada que tenga capacidad suficiente**; cuando las cuotas reales de la suscripción no sean comparables, dar preferencia al modelo disponible en el entorno ya abierto, sin rebajar los controles requeridos. Los nombres de los modelos y su disponibilidad pueden cambiar; consultar el selector vigente antes de ejecutar.

### Decisión ligera antes de trabajar

1. Definir problema, resultado observable, dependencias y aceptación; no recomendar modelo sólo por el tamaño aparente del cambio.
2. Evaluar **incertidumbre técnica**, **alcance entre módulos**, **riesgo para datos/seguridad/Producción** y **claridad de las pruebas**. Respetar la clasificación de nivel y capacidad de CORE.
3. Si la tarea está bien especificada y es de bajo riesgo, preferir Gemini 3.8 Flash o GPT-6.1 Terra, según el entorno de trabajo.
4. Si la causa es incierta, involucra arquitectura o requiere capacidad EXPERT por CORE, recomendar GPT-6.1 Sol o Gemini 4 Argon **para el análisis previo**. Tras producir límites, plan y criterios claros, se puede recomendar Flash/Terra para implementar la parte segura.
5. Registrar un motivo de una frase, no un informe ni una puntuación artificial. Una tarea puede indicar `Análisis: Sol/Argon; ejecución: Flash/Terra` cuando realmente necesite etapas diferentes. Si no, basta un modelo.
6. Reevaluar sólo si cambian alcance, riesgo, evidencia o disponibilidad, o si el agente falla dos veces sin nueva información. No cambiar de modelo por ritual.

**Ejemplo de entrada en TODO.md**:

```md
- ID: UI-014
  Problema: El botón de confirmar no es visible en móvil.
  Aceptación: Visible y operable a 360 px, por teclado y sin afectar el formulario.
  Estado: Pendiente
  Modelo recomendado: Gemini 3.8 Flash — cambio de interfaz acotado con pruebas claras.
```

**Límite importante:** una recomendación no cambia automáticamente el modelo del IDE. Codex o Antigravity siguen ejecutando el modelo seleccionado por el usuario o por su propio entorno. Nunca asumir revisión independiente cuando el mismo agente evalúa y ejecuta.
