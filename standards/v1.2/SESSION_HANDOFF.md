# Cierre de sesión y handoff obligatorio

El handoff transfiere un estado comprobable y una siguiente acción a otro chat/agente. Su profundidad sigue el [nivel de cambio](ENGINEERING_STANDARD.md#niveles-de-cambio).

## Cierre proporcional al modo

Durante una ronda PATCH/FEATURE, una respuesta breve con cambio, prueba y pendiente puede bastar. No forzar commit, push, actualización de STATE o handoff completo después de cada corrección. CHECK es el punto natural para consolidar la ronda. SYSTEM y la ruta ampliada de RELEASE mantienen cierre reforzado. La ruta rápida de RELEASE usa el [registro breve de publicación](DEPLOYMENT_STANDARD.md#ruta-rápida-paso-a-paso).

## Procedimiento de CHECK, SYSTEM o RELEASE ampliado

1. Comprobar `project-methodology/PROJECT_STATE.md` y actualizarlo sólo si cambió el estado relevante.
2. Actualizar `project-methodology/TODO.md` sólo si cambió el trabajo futuro/en curso o su estado.
3. Registrar decisiones relevantes en `project-methodology/DECISIONS.md` cuando corresponda.
4. Actualizar `project-methodology/ARCHITECTURE.md` y/o `project-methodology/design/` sólo si cambió su verdad.
5. Ejecutar pruebas pertinentes y registrar resultados/omisiones/entorno.
6. Revisar Git: TARGET_REPO, rama, diff, cambios ajenos, secretos, archivos generados y checks.
7. Crear commits descriptivos por unidad según política/alcance.
8. Hacer push cuando corresponde; el trabajo importante debe respaldarse en el remoto autorizado.
9. Verificar SHA remoto cuando sea posible.
10. Registrar siguiente paso concreto.

`AGENTS.md` sólo se modifica si cambian instrucciones, rutas, comandos, convenciones o límites del agente.

## Handoff mínimo

```text
Objetivo:
Resultado:
Prueba:
Commit:
Push:
Pendiente:
Siguiente paso:
```

## Handoff completo

```text
Fecha / proyecto / tarea:
Objetivo y aceptación:
Construido y archivos cambiados:
Estado de tarea:
Evidencia:
Verificación:
Problemas vigentes / pendientes:
Nivel de cambio; riesgo/autorización/recuperación cuando aplican:
Decisiones registradas:
Documentación actualizada / no aplica:
Git: rama, commit(s), working tree y cambios ajenos:
Cambios sin commit:
Commits sin push:
Remoto:
Despliegue:
Producción:
Siguiente paso:
```

## Distinciones obligatorias

Working tree limpio no prueba push. Push no prueba merge. Merge no prueba despliegue. Despliegue no prueba verificación en Producción.

## Inicio de la siguiente sesión

Usar la [Plantilla de inicio de sesión](CONTEXT_MANAGEMENT.md#plantilla-de-inicio-de-sesión), leer `AGENTS.md` y recuperar contexto desde `project-methodology/`.
