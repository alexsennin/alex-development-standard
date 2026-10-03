# Gestión de contexto

**El chat es memoria temporal y el repositorio es memoria persistente.** Guardar hechos, restricciones, decisiones y tareas que permiten continuar; evitar almacenar conversaciones enteras, secretos o conocimiento duplicado.

## Mapa documental recomendado

```text
<TARGET_ROOT>/
├── AGENTS.md
└── project-methodology/
    ├── PROJECT_CONTEXT.md
    ├── PROJECT_STATE.md
    ├── ARCHITECTURE.md
    ├── TODO.md
    ├── DECISIONS.md
    └── design/...
```

`AGENTS.md` es la puerta de entrada. Los demás documentos viven por defecto en `project-methodology/`.

## Contratos de los documentos mínimos

| Archivo | Responsabilidad exacta |
| --- | --- |
| `AGENTS.md` | Instrucciones ejecutables, rutas documentales, límites, comandos, convenciones y cierre |
| `project-methodology/PROJECT_CONTEXT.md` | Propósito, usuarios, stack, restricciones, convenciones y estructura estable |
| `project-methodology/PROJECT_STATE.md` | Fotografía del presente con evidencia y siguiente acción |
| `project-methodology/ARCHITECTURE.md` | Componentes, flujos, contratos, datos, responsabilidades y objetivo separado |
| `project-methodology/TODO.md` | Trabajo futuro/en curso con aceptación verificable |
| `project-methodology/DECISIONS.md` | Decisiones duraderas de producto/arquitectura |

## PROJECT_CONTEXT: estabilidad

Debe cambiar poco. Describe qué se construye, para quién y bajo qué restricciones. Declara stack actual y convenciones comprobadas, no el stack deseado.

## PROJECT_STATE: sólo presente

Debe contener fecha, estado actual, funcionalidades presentes, problemas conocidos, trabajo en curso, siguiente paso recomendado y última verificación relevante. No añadir un bloque histórico por sesión.

## Carga progresiva de contexto

No todos los cambios justifican leer toda la memoria del proyecto. Aplicar [CHANGE_MANAGEMENT.md](CHANGE_MANAGEMENT.md): PATCH lee la puerta de entrada y el módulo/contrato afectado; FEATURE añade arquitectura/estado pertinentes; SYSTEM, CHECK y RELEASE amplían la recuperación según riesgo. Si un documento estable ya fue leído en la sesión y no existe señal de cambio, no releerlo por rutina.

## Recuperación entre chats y agentes

1. Identificar TARGET_REPO, raíz, rama, remoto, HEAD y modificaciones.
2. Leer `AGENTS.md`.
3. Seguir sus rutas a `project-methodology/PROJECT_CONTEXT.md`, `PROJECT_STATE.md`, `ARCHITECTURE.md`, `TODO.md` y `DECISIONS.md`.
4. Para UI, leer `project-methodology/design/` cuando exista.
5. Revisar commits relevantes y contrastar documentos con implementación/destino.
6. Identificar trabajo ajeno, pendientes bloqueados y evidencia que debe revalidarse.
7. Formular objetivo/aceptación y siguiente acción; sólo entonces editar.

## Plantilla de inicio de sesión

```text
Antes de modificar código:

1. Confirma TARGET_REPO, TARGET_ROOT, rama, remoto, HEAD y estado Git.
2. Lee AGENTS.md.
3. Desde AGENTS.md, lee:
   - project-methodology/PROJECT_CONTEXT.md
   - project-methodology/PROJECT_STATE.md
   - project-methodology/ARCHITECTURE.md
   - project-methodology/TODO.md
   - project-methodology/DECISIONS.md
4. Si la tarea afecta UI, revisa project-methodology/design/ cuando exista.
5. Revisa últimos commits relevantes.
6. Contrasta documentación con implementación y entorno actual.
7. Identifica cambios ajenos, trabajo sin cerrar y evidencia que requiere revalidación.

Después resume brevemente:
- estado actual;
- objetivo de esta sesión;
- archivos/módulos potencialmente afectados;
- riesgos y nivel de cambio;
- dependencias;
- criterio de aceptación;
- pruebas previstas.

Separa hechos comprobados de supuestos.
Para SYSTEM/CHECK/RELEASE, no modificar hasta completar la recuperación pertinente. Para PATCH/FEATURE, usar una recuperación focal y ampliar sólo si aparecen dependencias, discrepancias o riesgo.
```

Si el proyecto adoptado utiliza rutas diferentes por una excepción documentada, seguir el mapa declarado en AGENTS.md en lugar de inventar otra estructura.

## Conflictos y evidencia

Código, historial y observación del destino fundamentan hechos. Un documento desactualizado no se corrige cambiando el producto para que coincida: investigar la discrepancia y actualizar la documentación pertinente.
