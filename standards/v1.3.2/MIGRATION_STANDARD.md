# Migraciones y cambios de datos persistentes

Este protocolo se usa cuando la entrega cambia esquema, datos, permisos persistentes o contratos entre aplicación y almacenamiento. No se ejecuta para una [despliegue sencillo sólo de archivos](DEPLOYMENT_STANDARD.md#ruta-rápida-paso-a-paso). Cada proyecto define comandos y proveedor; estas reglas describen el resultado necesario.

## Preparar una migración

1. Identificar fuente, destino, artefacto nuevo y dependencias. El archivo en Git no prueba que se aplicó; el historial remoto tampoco prueba por sí solo que el esquema y los datos tienen el efecto esperado.
2. Crear una unidad nueva con identificador único y ordenable según el proyecto. Una migración aplicada en un entorno compartido no se renombra ni reescribe: una corrección va en otra migración hacia delante.
3. Probar en un entorno aislado la secuencia pertinente, incluidos permisos y compatibilidad con la aplicación activa. Si el cambio depende de datos existentes, usar una copia o muestra segura que permita comprobar sus invariantes. No destruir una base local operativa para simular una base vacía.
4. Identificar qué migraciones son realmente parte de esta entrega. No revisar todo el historial remoto en cada corrección de UI o código sin efectos persistentes.

## Aplicar en un entorno compartido

1. Antes de escribir, comparar la secuencia candidata con el historial y los efectos observados del destino. Confirmar proyecto/entorno por identificador; no inferirlo de un alias local.
2. Aplicar una sola secuencia revisada, en orden, desde el artefacto acordado. Si una herramienta propone cambios distintos, se detiene la operación y se explica la diferencia.
3. Ante historial divergente, comparar identificadores, contenido SQL, dependencias, permisos y efectos. No reejecutar, marcar como aplicada, borrar ni editar una migración para silenciar la herramienta. Corregir metadatos sólo cuando evidencia independiente demuestre que el efecto ya está aplicado y se preserve el historial original.
4. Si hay datos reales o una operación difícil de revertir, definir respaldo y restauración o compensación antes de aplicar. Delimitar filas y escrituras con identidad estable, transacción, bloqueo o idempotencia según el caso; un conteo previo no protege contra cambios concurrentes.
5. Después, comprobar historial, esquema, invariantes de datos, permisos y comportamiento afectado. Registrar destino, artefacto, resultado y límites sin volcar datos privados ni secretos.

## Cambios por capas

Cuando base, funciones y aplicación se publican por mecanismos distintos, revisar sólo las capas que cambia la entrega y seguir una secuencia compatible. Normalmente se amplía primero el contrato de datos de modo que los consumidores activos sigan funcionando; se publican y comprueban los consumidores nuevos; y se retira el contrato anterior en otra entrega, cuando ya no tenga usuarios. No es necesario que todos los componentes lleven el mismo número de versión: importa que las combinaciones activas sean compatibles.

Para declarar que Local, Git y Producción están alineados en una entrega de varias capas, identificar la revisión de código, el estado de persistencia pertinente, las funciones desplegadas que intervienen y el artefacto que realmente responde en Producción. Si el proveedor no permite conocer una revisión, indicarlo como límite. Un `main` actualizado o HTTP 200 no demuestra esa alineación.
