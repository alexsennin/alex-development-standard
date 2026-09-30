# Estándar de publicación y despliegue

Desplegar significa aplicar una versión o cambio a un entorno de ejecución: aplicación, script, configuración, datos, archivos operativos o DNS. Publicar significa hacer disponible un entregable en un destino externo identificado, incluida una rama Git; no toda publicación es un despliegue. Usar el [vocabulario de evidencia](ENGINEERING_STANDARD.md#vocabulario-de-evidencia). Los mecanismos concretos se documentan en cada proyecto. Commit, push, merge y despliegue son operaciones distintas aunque una automatización las conecte.

## Antes de desplegar

1. Identificar entorno/destino, versión exacta, artefacto, configuración y cambios de datos necesarios.
2. Cumplir aceptación y comprobaciones del cambio; presentar diff/resultado concreto revisable.
3. Comprobar autorización aplicable para ese destino y alcance. Reutilizar autorización vigente; no asumir que una tarea local autoriza desplegar ni pedir confirmación redundante.
4. Revisar automatizaciones disparadas por push/merge, permisos, secretos y compatibilidad entre aplicación/datos.
5. Definir recuperación ante fallo. Si hay datos/archivos críticos, respaldo independiente, acceso seguro y restauración comprobada cuando corresponde.
6. Definir evidencia posterior y condiciones para detener, revertir o compensar.

Local-first es una opción frecuente; si el stack depende de un servicio remoto, trabajar en sandbox/preview autorizado. No hacer pasar un ensayo por Producción ni usar Producción como entorno de prueba por defecto.

## Ejecución

Desplegar sólo el artefacto y cambios acordados al destino identificado. Conservar identificador del despliegue/script/configuración y versión. Separar migraciones/datos cuando requieren orden y compatibilidad. No aplicar cambios de esquema o permisos remotos incidentalmente durante una entrega documental.

Una recuperación puede exigir rollback de código, migración compensatoria o restore; no prometer reversión automática de datos. Registrar fallo y evitar reintentos ciegos que dupliquen operaciones.

## Verificación posterior

- El proveedor confirma el artefacto/destino esperado y, cuando se expone, la versión/commit.
- El dominio/URL o punto de entrada resuelve y responde de forma prevista.
- El recorrido afectado funciona en el destino, incluyendo autenticación y denegaciones pertinentes.
- Escrituras persisten y las lecturas posteriores las muestran cuando el cambio lo requiere; usar pruebas seguras acordadas.
- Migraciones/configuración coinciden con la aplicación y no presentan errores relevantes.

“READY”, HTTP 200 o un build exitoso aislados no demuestran esas condiciones. Si alguna no pudo comprobarse, marcar verificación parcial y señalar paso pendiente. No añadir operaciones sobre datos reales para obtener evidencia sin autorización.

## Registro y cierre

PROJECT_STATE/handoff indican destino, fecha, versión, resultado de despliegue, comprobaciones de Producción y pendientes. No copiar valores secretos. Mantener tarea de despliegue separada si la entrega actual sólo preparó el cambio.

Código remoto y backup de DB/archivos son evidencias distintas. “Respaldado” debe indicar qué se respaldó, dónde de forma no secreta, cuándo y qué restauración fue demostrada.