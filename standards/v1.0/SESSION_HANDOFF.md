# Cierre de sesión y handoff obligatorio

El handoff es obligatorio para sesiones relevantes y transfiere un estado comprobable y una siguiente acción a otro chat/agente. Puede ser muy breve en cambios pequeños; su profundidad sigue el [nivel de cambio](ENGINEERING_STANDARD.md#niveles-de-cambio). No es una transcripción ni una nueva lista histórica dentro de PROJECT_STATE.

## Procedimiento antes de terminar

1. Comprobar PROJECT_STATE.md y actualizarlo sólo si cambió el estado relevante: resultado, trabajo en curso, problemas o próxima acción.
2. Actualizar TODO.md sólo si cambió el trabajo futuro/en curso o su estado; no crear una tarea artificial para un ajuste trivial.
3. Registrar decisiones relevantes si las hubo, diferenciando propuesta y aceptación; no registrar cada commit como decisión.
4. Actualizar arquitectura/diseño si cambió su contrato o apariencia; si no aplica, indicarlo.
5. Ejecutar pruebas pertinentes y registrar resultados/omisiones/entorno. Si aparecen fallos, corregir o dejar estado incompleto explícito.
6. Revisar Git: rama/diff, cambios ajenos, secretos, archivos generados y estado de checks.
7. Crear commits descriptivos por unidad según política/alcance; señalar archivos sin commit y su razón. Un ajuste trivial puede integrarse en la siguiente unidad prevista, con estado explícito.
8. Hacer push cuando corresponde por política/alcance; el trabajo importante debe respaldarse en el remoto autorizado. Si no aplica, explicarlo brevemente.
9. Verificar SHA remoto cuando sea posible; si no, decir “push informado como exitoso; referencia remota no confirmada” u otro estado preciso.
10. Registrar siguiente paso concreto con archivo/flujo, tarea y criterio que debe verificar el receptor.

Si el cierre queda interrumpido, publicar un handoff parcial que señale el paso pendiente. No afirmar “terminado y respaldado” si falta commit/push/evidencia requerida. [Actualizar sólo la verdad que cambió](PROJECT_DOCUMENTATION.md#regla-contra-la-sobredocumentación) también aplica al cierre.

## Handoff mínimo

Para Nivel 1 y cambios simples, puede usarse este bloque sin archivo adicional. En Commit/Push indicar rama/estado y cambios ajenos si los hay; añadir sólo una línea de destino/Producción si hubo publicación operativa, que debe reclasificarse por riesgo.

```text
Objetivo:
Resultado:
Prueba: comprobación y resultado/límite
Commit: SHA o pendiente/no aplica; estado Git y cambios ajenos
Push: confirmado / pendiente / no aplica; destino y razón cuando corresponda
Pendiente:
Siguiente paso:
```

## Handoff completo

Referencia principal para niveles 2, 3 y 4. Mantener los campos pertinentes y marcar no aplica de forma breve; enlazar evidencia en vez de duplicarla. El nivel 4 añade riesgo/recuperación y autorización aplicable.

```text
Fecha / proyecto / tarea:
Objetivo y aceptación:
Construido y archivos cambiados:
Estado de tarea: en revisión / bloqueada / cerrada
Evidencia: implementado; probado; publicado (destino); desplegado; verificado en Producción
Verificación: método, versión, entorno, resultado y límites
Problemas vigentes / pendientes y dependencias:
Nivel de cambio; riesgo, autorización y recuperación cuando aplican:
Decisiones registradas: IDs y estado
Documentación actualizada / no aplica:
Git: rama, commit(s), working tree limpio o sucio y motivo
Cambios de la entrega sin commit: ninguno o rutas/razón
Commits sin push: ninguno o lista/razón
Remoto: destino, SHA esperado/observado y momento; confirmado o no
Despliegue: no realizado / intento fallido / realizado, destino y versión
Producción: no verificada / verificada parcialmente / verificada, evidencia
Siguiente paso: acción concreta, tarea, ruta/flujo y aceptación
```

Este formato puede aparecer en el reporte final; PROJECT_STATE conserva únicamente información presente relevante y enlaza registros existentes. Datos sensibles permanecen fuera de Git.

## Distinciones obligatorias

Working tree limpio no prueba push. Push no prueba merge. Merge no prueba despliegue. Despliegue “listo” no prueba sesión, autorización o persistencia. Producción disponible no prueba que sirva el commit esperado. Cambios ajenos sin commit se describen y preservan, no se incluyen para aparentar cierre limpio.

En operaciones con DB/archivos: añadir estado de backup/restore/migraciones si aplica; no mezclar “código en remoto” con “datos respaldados”.

## Inicio de la siguiente sesión

Usar la [Plantilla de inicio de sesión](CONTEXT_MANAGEMENT.md#plantilla-de-inicio-de-sesión), leer handoff y documentos mínimos, comprobar Git/destino contra el registro, revisar si cambió la versión y revalidar evidencia afectada. Tomar la siguiente acción como recomendación dentro del alcance actual; no repetir pasos completados sin razón ni ejecutar un despliegue cuya autorización falta.

Si falta un dato necesario, continuar análisis independiente y pedir la información concreta. Si un estado anterior resulta desactualizado, corregirlo con evidencia sin borrar decisiones históricas.