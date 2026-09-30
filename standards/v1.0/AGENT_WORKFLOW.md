# Flujo de trabajo de agentes

Aplicar los principios de [ENGINEERING_STANDARD.md](ENGINEERING_STANDARD.md). La profundidad del flujo sigue el [nivel de cambio](ENGINEERING_STANDARD.md#niveles-de-cambio); para Nivel 1 puede resolverse con comprobación y handoff breves, sin formularios ni aprobaciones extra. El flujo puede iterar cuando aparece nueva evidencia; no debe convertirse en una ceremonia que bloquee cambios simples.

```text
Contexto → Análisis → Plan → Implementación → Pruebas → Revisión
        → Documentación → Commit → Push → Handoff
```

## Etapas y resultados

| Etapa | Qué ocurre | Resultado verificable para avanzar |
| --- | --- | --- |
| Contexto | Leer AGENTS, contexto, estado, arquitectura, TODO, decisiones pertinentes y diseño si hay UI; revisar Git/historial y destino | Estado actual comprendido, diferencias/ausencias identificadas, cambios ajenos registrados |
| Análisis | Recorrer flujo afectado, contratos, dependencias y autoridad de datos; comprobar hipótesis | Problema reproducible o evidencia suficiente; separar hechos, inferencias y dudas |
| Plan | Definir tarea, archivos previstos, límites, dependencias, aceptación y pruebas | Plan proporcional; decisiones pendientes y autorización necesaria identificadas |
| Implementación | Cambiar unidades pequeñas preservando comportamiento; actualizar plan si surge evidencia | Diff concreto dentro del alcance, sin ampliar tarea silenciosamente |
| Pruebas | Ejecutar verificaciones pertinentes contra destino seguro | Resultados y omisiones con evidencia; fallos corregidos o limitación registrada |
| Revisión | Evaluar diff, aceptación, permisos, regresiones, datos y riesgos del cambio | Resultado revisable; sin problemas críticos desconocidos presentados como éxito |
| Documentación | Actualizar sólo documentos cuya verdad cambió | Otro agente puede entender presente y siguiente paso sin leer el chat |
| Commit | Seleccionar rutas de la entrega y crear unidades descriptivas | Commit trazable; trabajo ajeno y secretos excluidos |
| Push | Publicar cuando corresponde en remoto/rama autorizados y verificar referencia | Cuando corresponde: resultado remoto registrado; si falla, pendiente explícito |
| Handoff | Ejecutar procedimiento de cierre y entregar información de continuación | Receptor sabe qué validar/hacer y qué no está terminado |

Documentar no se pospone hasta perder contexto: decisiones y estado de tarea se registran durante el trabajo; la fase Documentación revisa consistencia final. Un cambio sólo documental se implementa y valida como documentación, sin exigir pruebas de aplicación irrelevantes.

## Roles conceptuales

| Rol | Responsabilidad | Entrega |
| --- | --- | --- |
| Arquitecto | Comprender límites, opciones, dependencias y consecuencias | Plan y decisiones justificadas; actual/objetivo separados |
| Implementador | Producir cambio mínimo que cumpla aceptación | Diff y verificación inicial |
| Revisor | Cuestionar supuestos y comprobar evidencia/regresiones | Hallazgos accionables o aprobación de alcance explícito |
| Documentador | Mantener memoria persistente y preparar transferencia | Documentos coherentes y handoff |

Puede ser un mismo agente en fases distintas o agentes diferentes cuando la delegación está autorizada. La revisión del mismo agente debe incluir una pasada explícita del diff y criterios; no se presenta como revisión independiente. Si colaboran varios, asignar dueño de tarea/archivos, evitar ediciones concurrentes conflictivas y designar integrador; el integrador comprueba el resultado combinado. No duplicar pruebas por ritual.

## Durante una sesión

Comunicar objetivo al comenzar y hallazgos/cambios de alcance durante el trabajo. Nuevas indicaciones del usuario corrigen el plan sin borrar el objetivo vigente salvo cancelación o sustitución clara. Si falta información, continuar trabajo independiente; no ejecutar lo que dependa de la respuesta requerida.

Ante fallos repetidos, reconsiderar hipótesis, consultar documentación instalada/oficial aplicable y reducir el problema. No insistir ciegamente ni introducir una reescritura para evitar entenderlo.

## Entrada de un chat nuevo

Seguir [CONTEXT_MANAGEMENT.md](CONTEXT_MANAGEMENT.md) y [SESSION_HANDOFF.md](SESSION_HANDOFF.md). Ningún agente empieza a modificar código sólo a partir del último mensaje si desconoce el estado del repositorio.