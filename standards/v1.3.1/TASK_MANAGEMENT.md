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