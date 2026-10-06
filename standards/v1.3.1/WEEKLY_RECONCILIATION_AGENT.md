# Agente de conciliación semanal

Este agente es una función **opcional** de ALEX Development Standard para proyectos que tienen Local/Git/Producción o servicios publicados por separado. Una tarea programada puede ejecutarlo una vez por semana; definirlo en el estándar no activa por sí solo ninguna tarea. La programación, proyectos incluidos y permisos se acuerdan al adoptarlo. Un proyecto sólo local no necesita este agente.

## Objetivo

Detectar diferencias relevantes entre lo que se desarrolló, lo que está en Git y lo que realmente responde en Producción, sin repetir una auditoría completa en cada corrección. La conciliación es una **fotografía fechada**; no reemplaza el preflight de una publicación posterior ni prueba que los datos de dos entornos deban ser idénticos.

## Contrato de operación

- **Sólo lectura.** Puede consultar repositorios, estado de despliegues, historiales de migraciones y métricas o invariantes ya definidos. No hace push, merge, deploy, `db push`, `migration repair`, importaciones, borrados, restores, cambios de configuración ni escrituras en datos reales.
- **Alcance declarado.** Cada proyecto opta por participar e identifica repositorio/ramas, destinos de Producción, proveedor, componentes activos, revisión o entrega que se espera activa y fuentes de evidencia. No descubrir y auditar todos los proyectos de la cuenta por defecto.
- **Menor costo primero.** Comienza por la última fotografía válida y metadatos de Git/despliegue. Profundiza en DB, funciones o datos sólo cuando esas capas existen y una diferencia o regla del proyecto lo justifica. No recorre cada tabla ni descarga datos personales por rutina.
- **Evidencia separada.** Reporta código local, Git remoto, artefacto desplegado, esquema/historial, servicios independientes y datos operativos como hechos distintos. Un commit de documentación posterior al artefacto de aplicación no es por sí solo una incidencia.
- **Límites visibles.** Si faltan permisos, credenciales o identificadores, marca la capa como no verificada. No infiere estado sano de HTTP 200, `main`, un deployment READY o una fila del historial aislada.
- **Sin corrección automática.** Ante una discrepancia propone la acción mínima y quién debe autorizarla; la ejecución ocurre en otra tarea con el protocolo pertinente.

## Ejecución semanal

1. Leer las instrucciones del proyecto y la ficha de entornos vigente. Confirmar que está incluido en el piloto y que los destinos son los esperados.
2. Obtener una fotografía ligera: rama/commit local y remoto pertinentes, cambios sin commit, última revisión de aplicación realmente desplegada, estado de servicios independientes y, si aplica, IDs de migración del destino. Identificar la fuente y fecha de cada dato.
3. Comparar por capa con la entrega que el proyecto esperaba tener activa y con la última conciliación confiable si está disponible. Si no existe una línea base accesible, indicarlo y crear una primera fotografía sin suponer que `main` debe coincidir con Producción. No exigir que Local y Producción tengan los mismos datos operativos.
4. Investigar sólo diferencias materiales: cambios de código que deberían estar desplegados, migraciones pendientes o divergentes, funciones incompatibles, destino equivocado, fallos del flujo crítico o evidencia insuficiente para afirmar alineación. Si una diferencia es esperada, registrarla como tal y no alertar repetidamente.
5. Emitir un resultado corto con estado **alineado**, **diferencia esperada**, **requiere acción** o **no verificable**, más evidencia y siguiente paso. Decir **alineado** sólo para las capas efectivamente comprobadas. Conservar la fecha de la fotografía sin convertir `PROJECT_STATE.md` en una bitácora semanal.

## Cuándo avisar

Enviar una primera línea base breve al iniciar el piloto. Después, avisar sólo ante diferencia nueva o agravada, fallo de la revisión, cambio de estado que resuelva una incidencia o decisión requerida. Si todo sigue igual y no hay acción, permanecer en silencio; el historial de la tarea conserva la ejecución. No enviar resúmenes semanales repetidos por calendario.

Una incidencia debe indicar: **proyecto y entorno; capa afectada; esperado y observado; fuente/fecha; riesgo práctico; acción propuesta; verificación pendiente**. No incluir secretos, tokens, datos personales ni volcados de base.

## Relación con RELEASE

El agente semanal no es puerta obligatoria para la [ruta rápida de publicación](DEPLOYMENT_STANDARD.md#ruta-rápida-paso-a-paso). Un RELEASE usa evidencia actual del cambio y destino, aunque hubo una conciliación reciente. Si el hallazgo semanal revela un riesgo que afecta una entrega, el RELEASE correspondiente lo trata antes de publicarla. El agente tampoco autoriza ni ejecuta Producción por sí mismo.

## Instrucción reutilizable para programarlo

```text
Una vez por semana, concilia en modo de solo lectura los proyectos
explícitamente incluidos en el piloto. Lee sus instrucciones y fichas de
entornos. Compara Git, artefacto activo, migraciones y servicios sólo donde
apliquen; empieza por metadatos y profundiza ante diferencias materiales.
Distingue cambios esperados de incidencias. No escribas código, datos,
configuración ni Producción; no hagas deploy, push, merge ni reparaciones.
En la primera ejecución deja una línea base breve. Después mantente en
silencio si no hay cambios relevantes y avisa sólo ante una discrepancia
nueva, un fallo de verificación, una resolución o una decisión necesaria.
Incluye evidencia fechada y el siguiente paso concreto.
```
