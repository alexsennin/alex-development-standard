# Gestión de contexto

**El chat es memoria temporal y el repositorio es memoria persistente.** Guardar hechos, restricciones, decisiones y tareas que permiten continuar; evitar almacenar conversaciones enteras, secretos o conocimiento duplicado.

## Contratos de los documentos mínimos

| Archivo del proyecto | Responsabilidad exacta | Cambia cuando | No contiene |
| --- | --- | --- | --- |
| AGENTS.md | Instrucciones ejecutables para trabajar: lectura, límites, comandos verificados, convenciones y cierre | Cambia el procedimiento o una restricción | Historial de sesiones ni estado diario |
| PROJECT_CONTEXT.md | Propósito, usuarios, stack, restricciones, convenciones y estructura general | Cambia una base relativamente estable | Listado cambiante de tareas/resultados de pruebas |
| PROJECT_STATE.md | Fotografía del presente con evidencia y siguiente acción | Cambia el estado relevante, trabajo en curso o siguiente paso | Diario interminable de commits/chats |
| ARCHITECTURE.md | Componentes, flujos, contratos, datos, límites de responsabilidad y entornos; actual separado de objetivo | Cambia estructura/contrato o plan aceptado | Promesas futuras presentadas como implementadas |
| TODO.md | Trabajo futuro/en curso con ID, prioridad, problema, dependencia, aceptación y estado | Se crea, avanza, bloquea o resuelve una tarea | Resultados detallados de sesión o razones arquitectónicas completas |
| DECISIONS.md | Decisiones de producto/arquitectura con contexto, opciones, razones y consecuencias | Se acepta, rechaza o sustituye una decisión | Lista de tareas o fotografía del despliegue |

El [contrato documental](PROJECT_DOCUMENTATION.md) define contenido mínimo y mantenimiento, con actualización sólo si cambió la verdad; este documento define recuperación y relación entre fuentes.

## PROJECT_CONTEXT: estabilidad

Debe cambiar poco. Describe qué se construye, para quién y bajo qué restricciones. Declara stack actual y convenciones comprobadas, no el stack deseado. Enlaza estructura detallada en ARCHITECTURE para no duplicarla. Si un dato estable cambia, documentar la decisión y actualizar ambos sólo en su responsabilidad.

## PROJECT_STATE: sólo presente

Debe contener fecha, estado actual, funcionalidades presentes, problemas conocidos, trabajo en curso, siguiente paso recomendado y última verificación relevante con fecha/entorno/versión/resultado/límite. También registra estado de entrega (Git/remoto/despliegue) cuando sirve al handoff.

Reemplazar la fotografía anterior al actualizar. Conservar su historia en Git, decisiones y changelog cuando exista. No copiar todos los commits ni añadir un bloque por sesión indefinidamente. Los problemas aún vigentes permanecen, aunque provengan de sesiones antiguas.

## Recuperación entre chats y agentes

1. Identificar repositorio, rama, remoto, versión y modificaciones actuales sin exponer secretos.
2. Leer los seis documentos mínimos y diseño según tarea; seguir enlaces de la parte afectada.
3. Revisar commits relevantes y contrastar documentos con implementación/destino que se trabajará.
4. Identificar trabajo ajeno, pendientes bloqueados y qué verificaciones siguen válidas para esa versión.
5. Formular objetivo/aceptación y siguiente acción; sólo entonces editar.

No asumir que la copia del chat, una nota de memoria o un estado de servicio declarado refleja el presente. Verificar hechos de alta deriva: versiones, despliegue, migraciones aplicadas, ramas remotas, disponibilidad. Si no se pueden verificar, marcar dato como observado anteriormente/no confirmado.

## Plantilla de inicio de sesión

Bloque corto y copiable para un chat nuevo con cualquier agente. Las rutas siguen el mapa documental del proyecto si sus nombres o ubicación difieren. Si faltan documentos, comprobar la implementación y señalar la ausencia; no inventar contexto ni crear archivos vacíos.

```text
Antes de modificar código:
1. Lee AGENTS.md y las instrucciones aplicables del repositorio.
2. Lee PROJECT_CONTEXT.md, PROJECT_STATE.md, ARCHITECTURE.md, TODO.md y DECISIONS.md.
3. Para UI, revisa DESIGN_SYSTEM.md, TOKENS.md, COMPONENTS.md y LAYOUTS.md cuando existan.
4. Revisa rama, remoto, estado Git y últimos commits relevantes.
5. Contrasta documentación con implementación y entorno que se trabajará.
6. Identifica cambios ajenos, trabajo sin cerrar y evidencia que requiere revalidación.

Después resume brevemente: estado actual; objetivo de esta sesión;
archivos o módulos potencialmente afectados; riesgos y nivel de cambio;
dependencias; criterio de aceptación; pruebas previstas.
Separa hechos comprobados de supuestos. No modifiques código hasta completar
esta recuperación de contexto. Continúa luego dentro del alcance autorizado.
```

El resumen no es una petición automática de aprobación ni requiere un documento nuevo. Su profundidad depende del nivel de cambio.

## Conflictos y evidencia

Instrucciones aplicables del usuario determinan alcance; políticas del proyecto determinan trabajo dentro de ese alcance. Código, historial y observación del destino fundamentan hechos. Un documento desactualizado no se corrige cambiando el producto para que coincida. Investigar discrepancia, registrar cuál es la evidencia y actualizar la documentación pertinente; pedir aclaración sólo si cambia una decisión que no puede resolverse con el alcance autorizado.

Cuando termina el contexto disponible, dejar objetivo, correcciones, tareas completadas, evidencia y pendientes mediante [handoff](SESSION_HANDOFF.md). El resumen de chat ayuda a recuperar, pero no sustituye la comprobación de archivos y Git.