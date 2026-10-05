# Flujo de trabajo de agentes

Aplicar los principios de [ENGINEERING_STANDARD.md](ENGINEERING_STANDARD.md). La profundidad del flujo sigue el [nivel de cambio](ENGINEERING_STANDARD.md#niveles-de-cambio); para Nivel 1 puede resolverse con comprobación y handoff breves, sin formularios ni aprobaciones extra.

El flujo depende del modo definido en [CHANGE_MANAGEMENT.md](CHANGE_MANAGEMENT.md):

```text
PATCH   → contexto focal → cambio → prueba focal → resultado
FEATURE → contexto módulo → análisis → implementación → pruebas → resultado
SYSTEM  → contexto amplio pertinente → análisis → plan → implementación → pruebas → revisión
CHECK   → diff acumulado → pruebas pertinentes → documentación necesaria → commit/push según política
RELEASE → preflight → autorización → publicación/migraciones → verificación → registro
```

La [conciliación semanal](WEEKLY_RECONCILIATION_AGENT.md) es un agente opcional de solo lectura, fuera del ciclo de implementación. No se invoca para cada PATCH/CHECK y no sustituye el preflight de RELEASE.

PATCH y FEATURE no deben ejecutar por rutina Commit → Push → Handoff completo después de cada microiteración. Esas operaciones pueden consolidarse en CHECK cuando el usuario está realizando una ronda interactiva de pruebas.

## Etapas y resultados

| Etapa | Qué ocurre | Resultado verificable para avanzar |
| --- | --- | --- |
| Contexto | Confirmar TARGET_REPO/Git; leer AGENTS.md y seguir sus enlaces a project-methodology/; revisar diseño si hay UI | Estado actual comprendido, diferencias/ausencias identificadas, cambios ajenos registrados |
| Análisis | Recorrer flujo afectado, contratos, dependencias y autoridad de datos; comprobar hipótesis | Problema reproducible o evidencia suficiente; separar hechos, inferencias y dudas |
| Plan | Definir tarea, archivos previstos, límites, dependencias, aceptación y pruebas | Plan proporcional; decisiones pendientes y autorización necesaria identificadas |
| Implementación | Cambiar unidades pequeñas preservando comportamiento; actualizar plan si surge evidencia | Diff concreto dentro del alcance, sin ampliar tarea silenciosamente |
| Pruebas | Ejecutar verificaciones pertinentes contra destino seguro | Resultados y omisiones con evidencia |
| Revisión | Evaluar diff, aceptación, permisos, regresiones, datos y riesgos | Resultado revisable |
| Documentación | Actualizar sólo documentos de project-methodology/ cuya verdad cambió; AGENTS sólo si cambian instrucciones | Otro agente puede comprender presente y siguiente paso sin leer el chat |
| Commit | Seleccionar rutas de la entrega y crear unidades descriptivas | Commit trazable |
| Push | Publicar cuando corresponde en remoto/rama autorizados | Resultado remoto registrado o pendiente explícito |
| Handoff | Ejecutar procedimiento de cierre | Receptor sabe qué validar/hacer y qué no está terminado |

## Roles conceptuales

Arquitecto, Implementador, Revisor y Documentador pueden ser fases del mismo agente o agentes diferentes cuando esté autorizado. La revisión del mismo agente debe incluir una pasada explícita sobre diff y criterios; no presentarla como revisión independiente.

## Entrada de un chat nuevo

Seguir [CONTEXT_MANAGEMENT.md](CONTEXT_MANAGEMENT.md). El agente debe conocer TARGET_REPO y evitar pisar trabajo ajeno. En PATCH/FEATURE puede usar la memoria persistente ya vigente y recuperar sólo el contexto directamente necesario; SYSTEM, CHECK y la ruta ampliada de RELEASE cargan el contexto pertinente a sus efectos. Una [ruta rápida de RELEASE](DEPLOYMENT_STANDARD.md#ruta-rápida-paso-a-paso) sólo necesita la entrega, el destino y la evidencia focal cuando no exista incertidumbre material.
