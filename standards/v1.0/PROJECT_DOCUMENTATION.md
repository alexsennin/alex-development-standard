# Documentación de cada proyecto

Este contrato se aplica al adoptar v1; los archivos se redactan con hechos del proyecto. No copiar la documentación del repositorio de referencia ni convertir esta metodología en el contexto de todos los productos.

## Contenido mínimo por archivo

| Archivo | Contenido requerido |
| --- | --- |
| AGENTS.md | Lecturas previas, identificación del entorno/Git, límites de autorización, convenciones locales, comandos realmente disponibles y enlace al cierre; conservar instrucciones generadas/aplicables |
| PROJECT_CONTEXT.md | Propósito, usuarios, stack actual, restricciones, convenciones, mapa general y enlaces a fuentes operativas no secretas |
| PROJECT_STATE.md | Fecha, estado presente, funcionalidades, problemas vigentes, trabajo en curso, siguiente acción, última verificación relevante y estados de entrega |
| ARCHITECTURE.md | Implementación actual, componentes/flujos/contratos, datos y responsabilidades; arquitectura objetivo y transición en sección separada |
| TODO.md | ID, prioridad, problema, dependencia, criterio de aceptación y estado; responsable/evidencia cuando ayuda |
| DECISIONS.md | ID, fecha, estado, contexto, opciones, decisión, razón, consecuencias y referencias; sustitución conservando historia |

Si hay UI: DESIGN_SYSTEM.md describe principios/identidad/interacción; TOKENS.md valores implementados y origen; COMPONENTS.md inventario/API/estados; LAYOUTS.md sólo si añade claridad a patrones estructurales. Si no hay UI, registrar no aplica y no crear documentos vacíos.

README del proyecto actúa como entrada: propósito breve, instalación/ejecución verificadas y enlaces de contexto. Runbooks, changelog, diagramas o referencias se añaden sólo cuando reducen carga o aclaran una operación; no imponer archivos de relleno.

## Actualización y responsabilidad

El agente que cambia comportamiento actualiza sólo la documentación cuya verdad cambió. El revisor comprueba coherencia; el dueño del proyecto valida decisiones nuevas cuando corresponde. PROJECT_STATE se reemplaza por la fotografía presente; Git conserva versiones anteriores.

Una tarea resuelta sale de la lista activa o pasa a sección acotada de cerradas con referencia. Razones duraderas viven en DECISIONS; instrucciones de ejecución en AGENTS/runbook; un resultado actual en STATE. Enlazar en vez de repetir párrafos que divergirán.

## Regla contra la sobredocumentación

**Actualizar únicamente los documentos cuya verdad haya cambiado.** Documentar debe preservar contexto útil, no producir actividad administrativa. Evaluar relevancia y [nivel de cambio](ENGINEERING_STANDARD.md#niveles-de-cambio); no editar todos los archivos al cerrar por rutina.

- Un ajuste CSS menor normalmente no cambia arquitectura, decisiones ni contexto; puede no requerir PROJECT_STATE si no altera el estado relevante. Su comprobación y resultado caben en el handoff mínimo.
- Una modificación de autenticación posiblemente cambia arquitectura, estado, decisiones, pruebas y tareas. Actualizar las partes realmente afectadas, sin repetir el mismo contenido en todas.
- No crear archivos vacíos porque el estándar los menciona. Al adoptar, cubrir responsabilidades con contenido útil o indicar una ausencia/no aplica de forma breve en el punto de entrada.
- No duplicar información: preferir enlaces. PROJECT_STATE no es bitácora; DECISIONS no es historial de cada commit; TODO no es changelog.
- No inventar tareas o decisiones para justificar un cambio simple. Una decisión formal sólo corresponde a una razón duradera o un cambio importante.

Si se comprobó que ningún documento cambió de verdad, declarar “documentación vigente; sin actualización necesaria” en el handoff. El formato de reporte también debe ser proporcional; no crear un archivo adicional por cada comprobación trivial.

## Registro de evidencia

Una afirmación de verificación incluye fecha, versión/commit o base, entorno, método, resultado y límites. Usar los términos [implementado, probado, publicado, desplegado y verificado en Producción](ENGINEERING_STANDARD.md#vocabulario-de-evidencia), indicando alcance y límites. Documentos no verificados se etiquetan; no completar huecos inventando funcionalidades o resultados.

Cuando el estado describe el commit que todavía se va a crear, usar el commit base o referencia a HEAD/registro final de Git; no intentar escribir el SHA del propio commit dentro de él. Evitar ciclos interminables de commits sólo para actualizar esa autorreferencia.

## Calidad documental

Comprobar enlaces relativos, nombres/rutas, consistencia entre documentos, comandos contra configuración y diff. No incluir credenciales, datos privados, logs sin filtrar o URLs con tokens. Ejemplos deben ser ficticios y los placeholders explícitos.

La revisión debe permitir a otro agente responder qué hace el proyecto, cómo funciona, qué es presente/futuro, qué puede cambiar y cómo comprobar/cerrar una tarea sin leer conversaciones anteriores.

[CONTEXT_MANAGEMENT.md](CONTEXT_MANAGEMENT.md) define fronteras; [SESSION_HANDOFF.md](SESSION_HANDOFF.md), la transferencia final.