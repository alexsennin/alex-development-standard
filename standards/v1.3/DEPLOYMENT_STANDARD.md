# Estándar de publicación y despliegue

Este documento se ejecuta operativamente en **RELEASE mode**. PATCH, FEATURE, SYSTEM y CHECK pueden preparar cambios, artefactos y migraciones, pero no autorizan por sí mismos operaciones sobre Producción. Dentro de RELEASE se elige la ruta rápida o la ruta ampliada según el cambio real.

Desplegar significa aplicar una versión o cambio a un entorno de ejecución: aplicación, script, configuración, datos, archivos operativos o DNS. Publicar significa hacer disponible un entregable en un destino externo identificado, incluida una rama Git; no toda publicación es un despliegue. Usar el [vocabulario de evidencia](ENGINEERING_STANDARD.md#vocabulario-de-evidencia). Los mecanismos concretos se documentan en cada proyecto. Commit, push, merge y despliegue son operaciones distintas aunque una automatización las conecte.

## Elegir la ruta de publicación

La clasificación se hace por efectos, no por número de archivos. Para una entrega que reúna varios cambios, evaluar el conjunto. Si un componente exige la ruta ampliada, separar entregas compatibles cuando sea práctico; no llamar sencilla a la entrega completa por contener también cambios visuales.

| Ruta | Cuándo aplica | Trabajo suficiente |
| --- | --- | --- |
| **Rápida: sólo archivos de aplicación** | Código o recursos estáticos que no cambian esquema, datos existentes, contratos de escritura, autorización, secretos, configuración, infraestructura ni servicios que se publican aparte; destino y mecanismo de despliegue conocidos; reversión del artefacto disponible | Diff y prueba pertinente, identificar destino y revisión de Git/artefacto, publicar por el mecanismo habitual, comprobar disponibilidad y recorrido afectado, registrar resultado breve |
| **Ampliada: datos, contratos o varios destinos** | Migraciones, importaciones/borrados, cambios en cómo se escriben o interpretan datos, auth/RLS, pagos, secretos, infraestructura, DNS, funciones/servicios independientes, incompatibilidad entre componentes o destino incierto | Preflight por capas afectadas, secuencia compatible, respaldo/recuperación según riesgo, validación y registro reforzados |

**Ruta rápida no exige** número de versión manual, etiqueta Git, changelog, `RELEASE_STATE.md`, cotejo de historiales de migraciones, respaldo de la base ni suite completa sólo por tocar Producción. El commit de Git, identificador de despliegue o revisión que emita el proveedor sirve para saber qué archivos quedaron activos y volver al artefacto anterior. No se inventa una versión numerada por cada reemplazo. Si el proveedor exige crear una versión para conservar la misma URL (por ejemplo, algunos despliegues de Apps Script), esa operación técnica sí se realiza.

Subir o reemplazar archivos es un mecanismo válido para la ruta rápida cuando el proyecto lo usa. Antes de hacerlo, confirmar el destino y que el conjunto de archivos corresponde a una revisión coherente; después, comprobar que la aplicación sirve el cambio. Si un push o merge despliega automáticamente, revisar esa automatización una vez y utilizarla, sin añadir un despliegue manual redundante.

La ausencia de migración **no basta** para elegir la ruta rápida: un cambio de código puede modificar ventas, permisos o cálculos sobre datos reales sin cambiar la estructura de la base. Ante ese efecto, usar la ruta ampliada sólo para las capas implicadas.

Ejemplos: corregir un texto, ajustar una tabla visual o reparar un filtro de lectura que usa el mismo contrato puede ir por la ruta rápida. Cambiar el cálculo del total de una venta, la autorización para editarla o la semántica de una escritura va por la ruta ampliada aunque no exista SQL nuevo. Agregar una columna o publicar una función independiente también va por la ruta ampliada.

## Ruta rápida paso a paso

1. Confirmar que los cambios incluidos cumplen la condición de sólo archivos y que la persona usuaria ya autorizó ese destino. Una orden como «aplica en Producción» autoriza esta entrega; no volver a pedir permiso para la misma operación.
2. Revisar el diff y la comprobación focal o CI ya válido. Identificar proyecto, URL, rama/commit o conjunto de archivos y el mecanismo que activa el despliegue.
3. Publicar con el flujo habitual del proyecto y guardar el identificador automático disponible (commit, deployment o versión impuesta por el proveedor). Si falla, volver al artefacto anterior conocido; no ejecutar operaciones de datos como supuesto rollback de código.
4. Confirmar que el destino sirve el artefacto nuevo y probar el recorrido afectado. Para un cambio visual, abrir la pantalla pertinente; para un bug, repetir el caso que fallaba. HTTP 200 por sí solo deja la verificación funcional pendiente.
5. Informar en pocas líneas: cambio, destino, identificador disponible, prueba posterior y límite concreto. Actualizar documentos del proyecto sólo si cambió su verdad.

No repetir búsquedas de versiones de DB, funciones o proyectos ajenos cuando ninguna de esas capas forma parte de la entrega. Si se descubre una dependencia durante el preflight, cambiar a la ruta ampliada y conservar la evidencia ya obtenida.

## Ruta ampliada

Aplicar las secciones siguientes de forma proporcional y sólo a las capas afectadas. Una migración sigue el [protocolo de migraciones](MIGRATION_STANDARD.md); un cambio de función independiente requiere identificar su despliegue y compatibilidad; una carga de datos exige límites, identidad de filas, integridad y recuperación. No convertir cada RELEASE en una conciliación total de todos los entornos.

## Antes de desplegar

1. Identificar entorno/destino, revisión o artefacto que se entregará, configuración y cambios de datos necesarios.
2. Cumplir aceptación y comprobaciones del cambio; presentar diff/resultado concreto revisable.
3. Comprobar autorización aplicable para ese destino y alcance. Reutilizar autorización vigente; no asumir que una tarea local autoriza desplegar ni pedir confirmación redundante.
4. Revisar automatizaciones disparadas por push/merge, permisos, secretos y compatibilidad entre aplicación/datos cuando sean parte del cambio.
5. Definir recuperación ante fallo. Si hay datos/archivos críticos, respaldo independiente, acceso seguro y restauración comprobada cuando corresponde.
6. Definir evidencia posterior y condiciones para detener, revertir o compensar.

Local-first es una opción frecuente; si el stack depende de un servicio remoto, trabajar en sandbox/preview autorizado. No hacer pasar un ensayo por Producción ni usar Producción como entorno de prueba por defecto.

## Ejecución

Desplegar sólo el artefacto y cambios acordados al destino identificado. Conservar el identificador disponible del despliegue/script/configuración. Separar migraciones/datos cuando requieren orden y compatibilidad; seguir una [secuencia compatible por capas](MIGRATION_STANDARD.md#cambios-por-capas) cuando la entrega cruce base, servicios y aplicación. No aplicar cambios de esquema o permisos remotos incidentalmente durante una entrega documental.

Una recuperación puede exigir rollback de código, migración compensatoria o restore; no prometer reversión automática de datos. Registrar fallo y evitar reintentos ciegos que dupliquen operaciones.

## Verificación posterior

- El proveedor confirma el artefacto/destino esperado y, cuando se expone, la versión/commit.
- El dominio/URL o punto de entrada resuelve y responde de forma prevista.
- El recorrido afectado funciona en el destino, incluyendo autenticación y denegaciones pertinentes.
- Escrituras persisten y las lecturas posteriores las muestran cuando el cambio lo requiere; usar pruebas seguras acordadas.
- Migraciones/configuración coinciden con la aplicación y no presentan errores relevantes.

“READY”, HTTP 200 o un build exitoso aislados no demuestran esas condiciones. Si alguna no pudo comprobarse, marcar verificación parcial y señalar paso pendiente. No añadir operaciones sobre datos reales para obtener evidencia sin autorización.

## Registro y cierre

El handoff indica destino, fecha, revisión disponible, resultado y comprobación posterior. `PROJECT_STATE` o `RELEASE_STATE` se actualizan sólo si existen y cambió un hecho que deben conservar; la ruta rápida puede cerrarse en la respuesta y el commit. No copiar valores secretos. Mantener tarea de despliegue separada si la entrega actual sólo preparó el cambio.

Código remoto y backup de DB/archivos son evidencias distintas. “Respaldado” debe indicar qué se respaldó, dónde de forma no secreta, cuándo y qué restauración fue demostrada.

## Migraciones y ciclo de iteración

Crear o probar una migración en entorno local/aislado forma parte del desarrollo. Aplicarla a Producción es una operación RELEASE. Mantener migraciones reproducibles y ordenadas, pero no consultar ni sincronizar el historial remoto en un PATCH o CHECK que no afecte datos. Si la entrega incluye migraciones, CHECK identifica las candidatas y RELEASE aplica el [protocolo pertinente](MIGRATION_STANDARD.md).
