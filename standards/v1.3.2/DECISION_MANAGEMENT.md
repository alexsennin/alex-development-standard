# Gestión de decisiones

DECISIONS.md conserva razones duraderas de arquitectura y producto. No todo detalle de implementación necesita una decisión formal.

## Cuándo registrar

Cambios de contratos/datos/autorización, elección o sustitución de stack/proveedor, estrategia de publicación/recuperación, cambios visuales de identidad o patrón, excepciones operativas y tradeoffs difíciles de revertir. Un ajuste rutinario compatible con reglas existentes se explica en tarea/commit, sin inventar una decisión nueva.

## Registro mínimo

```text
ID / título:
Fecha:
Estado: propuesta / aceptada / rechazada / sustituida
Contexto y problema:
Opciones consideradas:
Decisión y razón:
Consecuencias: beneficio, costo, riesgo y límite
Alcance: qué proyecto/capa afecta y qué queda fuera
Validación: responsable y evidencia de aceptación cuando corresponde
Referencias: tarea, archivos, commit o fuente
Sustituye / sustituida por:
```

Las opciones deben ser reales y pertinentes; no añadir alternativas absurdas para justificar una elección. Distinguir decisión de necesidad observada y de hipótesis todavía no comprobada.

## Ciclo

Proponer → revisar cuando corresponde → aceptar o rechazar → implementar mediante tarea → verificar. Una decisión aceptada puede estar pendiente de implementación; una solución implementada puede seguir pendiente de aceptación de producto. Registrar esos estados sin equipararlos.

Si cambia una decisión, conservar su contexto y marcarla sustituida con enlace al nuevo ID. Actualizar contexto/arquitectura/diseño cuando corresponda y tareas de transición. No borrar el pasado para aparentar que siempre se eligió lo mismo.

## Adaptación del estándar

Una excepción a la versión adoptada del ALEX Development Standard identifica regla, motivo, responsable, alcance, riesgo, duración o condición de revisión y alternativa compensatoria. No permite ignorar restricciones de seguridad/autorización aplicables. La propuesta de adoptar o cambiar una metodología no se presenta como aprobación humana ya recibida.

El registro de cada proyecto describe sus decisiones. Las mejoras de la metodología se revisan en su propio alcance/versionado, sin modificar automáticamente repositorios consumidores.

[CONTEXT_MANAGEMENT.md](CONTEXT_MANAGEMENT.md) evita duplicación; [TASK_MANAGEMENT.md](TASK_MANAGEMENT.md) convierte una decisión en trabajo verificable.