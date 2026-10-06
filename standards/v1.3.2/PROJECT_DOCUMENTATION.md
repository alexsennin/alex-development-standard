# Documentación de cada proyecto

Este contrato se aplica al adoptar v1.3.2. Los documentos se redactan con hechos del proyecto consumidor; no son copias del estándar central.

## Ubicación recomendada

```text
<TARGET_ROOT>/
├── AGENTS.md
├── README.md
├── <código y configuración>
└── project-methodology/
    ├── PROJECT_CONTEXT.md
    ├── PROJECT_STATE.md
    ├── ARCHITECTURE.md
    ├── TODO.md
    ├── DECISIONS.md
    ├── ENVIRONMENTS.md        # cuando aplica
    ├── RELEASE_STATE.md       # cuando aplica
    └── design/
        ├── DESIGN_SYSTEM.md
        ├── TOKENS.md
        ├── COMPONENTS.md
        └── LAYOUTS.md
```

`AGENTS.md` se mantiene en la raíz porque actúa como punto de descubrimiento y ejecución para agentes. Debe enlazar a los documentos de `project-methodology/`.

El resto de la memoria persistente del proyecto se concentra por defecto en `project-methodology/` para no dispersar documentación metodológica entre código/configuración de la raíz.

Si un repositorio ya posee una estructura documental equivalente y válida, la adopción puede mapear responsabilidades en lugar de mover todo por fuerza. Debe existir una única autoridad clara para cada responsabilidad.

## Contenido mínimo por archivo

| Ruta recomendada | Contenido requerido |
| --- | --- |
| `AGENTS.md` | Lecturas previas, identificación del entorno/Git, límites de autorización, convenciones locales, comandos realmente disponibles y enlace a `project-methodology/` |
| `project-methodology/PROJECT_CONTEXT.md` | Propósito, usuarios, stack actual, restricciones, convenciones, mapa general y enlaces a fuentes operativas no secretas |
| `project-methodology/PROJECT_STATE.md` | Fecha, estado presente, funcionalidades, problemas vigentes, trabajo en curso, siguiente acción, última verificación relevante y estados de entrega |
| `project-methodology/ARCHITECTURE.md` | Implementación actual, componentes/flujos/contratos, datos y responsabilidades; arquitectura objetivo separada |
| `project-methodology/TODO.md` | ID, prioridad, problema, dependencia, criterio de aceptación y estado |
| `project-methodology/DECISIONS.md` | ID, fecha, estado, contexto, opciones, decisión, razón, consecuencias y referencias |

Si hay UI y aporta valor:

| Ruta recomendada | Contenido |
| --- | --- |
| `project-methodology/design/DESIGN_SYSTEM.md` | Principios, identidad, jerarquía, interacción y accesibilidad |
| `project-methodology/design/TOKENS.md` | Valores implementados, origen, nombres semánticos y variantes |
| `project-methodology/design/COMPONENTS.md` | Componentes/clases, API/variantes/estados, consumidores y límites |
| `project-methodology/design/LAYOUTS.md` | Estructuras repetidas, anchos, overflow y adaptación cuando aporte claridad |

No crear `design/` si no hay UI o no aporta información útil.

## README del proyecto

El README del producto sigue siendo entrada humana: propósito breve, instalación/ejecución verificadas y enlaces relevantes. No debe convertirse en copia de la metodología.

## Actualización y responsabilidad

El agente que cambia comportamiento actualiza sólo la documentación cuya verdad cambió. PROJECT_STATE se reemplaza como fotografía presente; Git conserva versiones anteriores.

Razones duraderas viven en DECISIONS; instrucciones de ejecución en AGENTS/runbooks; trabajo futuro en TODO; estado actual en STATE.

## Regla contra la sobredocumentación

**Actualizar únicamente los documentos cuya verdad haya cambiado.**

- Un ajuste CSS menor normalmente no cambia arquitectura, decisiones ni contexto.
- Una modificación de autenticación puede cambiar arquitectura, estado, decisiones, pruebas y tareas.
- No crear archivos vacíos porque el estándar los menciona.
- No duplicar información: preferir enlaces.
- PROJECT_STATE no es bitácora; DECISIONS no es historial de commits; TODO no es changelog.
- No inventar tareas o decisiones para justificar cambios simples.

Si ningún documento cambió de verdad, declarar “documentación vigente; sin actualización necesaria” en el handoff.

## Calidad documental

Comprobar enlaces relativos, nombres/rutas, consistencia, comandos contra configuración y diff. No incluir credenciales, datos privados, logs sin filtrar o URLs con tokens.

La documentación debe permitir que otro agente responda qué hace el proyecto, cómo funciona, qué es presente/futuro, qué puede cambiar y cómo continuar sin leer conversaciones anteriores.


## Estado de entornos y releases

Cuando existen varios entornos o despliegues, `ENVIRONMENTS.md` puede registrar destinos, propósito, fuentes de configuración no secretas y límites de escritura. `RELEASE_STATE.md` sólo aporta valor cuando hay varios componentes, migraciones pendientes o diferencias entre entornos que deben seguirse; contiene un estado compacto y no se actualiza por cada reemplazo sencillo de archivos. No son bitácoras y no duplican secretos.
