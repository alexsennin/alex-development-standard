# AXIOM — Development Orchestration Runtime

AXIOM es un **runtime opcional** para ejecutar ARC Development Standard con routing automático de capacidad. ARC no requiere AXIOM y también se aplica desde Codex o Antigravity. **AXIOM no es un modelo**: coordina Codex CLI y decide qué modelo/reasoning usar en cada actividad.

## Relación de componentes
```text
ARC Development Standard  → define reglas
AXIOM                      → aplica/orquesta reglas
Codex CLI                  → ejecuta trabajo sobre el repositorio
Modelos                    → aportan capacidad ROUTER/FOCUSED/ADVANCED/EXPERT/FRONTIER
```

## Economía
La configuración predeterminada de AXIOM usa **Codex CLI autenticado con la cuenta de ChatGPT**, no una API key. De ese modo el uso se contabiliza contra la cuota de Codex incluida en el plan del usuario. Si se configura una API key propia, deja de ser el perfil económico predeterminado y aplican las condiciones/precios de API.

## Flujo de AXIOM (solo cuando se utiliza)
1. El usuario ejecuta `axiom` desde `TARGET_ROOT` y expresa la intención.
2. AXIOM carga `CORE.md`, `AGENTS.md` y el contexto mínimo.
3. ROUTER clasifica modo/nivel/capacidad y emite salida estructurada; no implementa.
4. Si la tarea es FOCUSED/ADVANCED y está suficientemente especificada, AXIOM ejecuta el worker correspondiente.
5. Si requiere EXPERT/FRONTIER, AXIOM lanza análisis de sólo lectura, obtiene diagnóstico, fases y Execution Packets.
6. Cuando el plan visible requiere checkpoint, el usuario autoriza una fase, varias o todo el plan.
7. AXIOM ejecuta cada microtarea con la capacidad asignada y puede escalar sin reiniciar.
8. AXIOM ejecuta validación proporcional y entrega el resultado.

## Permisos por rol
| Rol | Edición de repo | Propósito |
| --- | --- | --- |
| ROUTER | no | clasificación estructurada |
| EXPERT/FRONTIER arquitecto | no por defecto | diagnóstico, arquitectura, plan, Execution Packets |
| FOCUSED/ADVANCED executor | sí, workspace seguro | implementación acotada |
| Reviewer | no | verificación/revisión |
| RELEASE worker | sólo con autorización explícita | despliegue/aplicación al destino autorizado |

ROUTER no debe disponer de permisos de escritura. Esto permite usar una capacidad barata para clasificación sin convertirla accidentalmente en el agente de programación.

## Checkpoints
- PATCH/Nivel 1 inequívoco puede ejecutarse sin plan visible.
- FEATURE compleja/SYSTEM muestran plan cuando la descomposición aporta valor.
- El usuario puede autorizar `fase 1`, `fases 1-3` o `todo`.
- Cambios materiales de alcance/destino/riesgo invalidan la autorización para la parte modificada.

## Producción
AXIOM no interpreta `publica`, `push` o `sube` como autorización de Producción. Sólo `despliega en Producción` / `aplica en Producción` o autorización equivalente habilita RELEASE.

## Modo inicial
- **AXIOM:** ROUTER puede usar la capacidad económica definida en MODEL_PROFILE (actualmente Luna Bajo), porque su ejecución es aislada y sin escritura.
- **Otros entornos:** Codex y Antigravity usan directamente CORE, TASK_MANAGEMENT y MODEL_PROFILE; no deben replicar automáticamente este flujo AXIOM.

## Estado de implementación
Este documento describe el contrato específico de AXIOM, no una dependencia general de ARC. La implementación de referencia debe ser local, secuencial inicialmente y conservadora: routing, planificación, ejecución local y validación antes de añadir concurrencia o RELEASE automático.