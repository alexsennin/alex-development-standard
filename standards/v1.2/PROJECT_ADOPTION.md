# Adopción de ALEX DEVELOPMENT STANDARD v1.2

Procedimiento para aplicar la metodología en un repositorio existente o nuevo. La v1.2 está vigente y disponible para adopción gradual. Cada proyecto debe contrastar su estado real y decidir qué adaptar; publicar el estándar central no cambia automáticamente repositorios consumidores.

El [agente de conciliación semanal](WEEKLY_RECONCILIATION_AGENT.md) es opcional: sólo se programa para proyectos y destinos elegidos expresamente, después de identificar sus fuentes de evidencia. La adopción documental del estándar no crea una automatización por sí misma.

## Preflight obligatorio

Antes de escribir:

1. Confirmar SOURCE_REPO = `alexsennin/alex-development-standard`.
2. Confirmar SOURCE_VERSION = `standards/v1.2/`.
3. Confirmar TARGET_REPO y TARGET_ROOT.
4. Confirmar rama, remoto, HEAD y estado Git de TARGET_REPO.
5. Confirmar TARGET_REPO != SOURCE_REPO.

Si SOURCE_REPO y TARGET_REPO son iguales, detenerse sin modificar nada.

## Estructura de adopción recomendada

```text
<TARGET_ROOT>/
├── AGENTS.md
├── README.md
├── <código/configuración>
└── project-methodology/
    ├── PROJECT_CONTEXT.md
    ├── PROJECT_STATE.md
    ├── ARCHITECTURE.md
    ├── TODO.md
    ├── DECISIONS.md
    ├── ENVIRONMENTS.md        # si aplica
    ├── RELEASE_STATE.md       # si aplica
    └── design/
        ├── DESIGN_SYSTEM.md
        ├── TOKENS.md
        ├── COMPONENTS.md
        └── LAYOUTS.md
```

`AGENTS.md` permanece en raíz y enlaza a `project-methodology/`. Los documentos de diseño se crean sólo si aplican.

## Etapas

1. **Inventario:** identificar propósito, stack, estructura, estado Git, fuentes operativas, entornos y reglas existentes.
2. **Brechas:** clasificar hechos, propuestas, deuda y documentación obsoleta; ubicar equivalentes a las responsabilidades mínimas.
3. **Plan de adopción:** definir alcance, archivos, criterios de aceptación, dependencias y política de publicación.
4. **Contexto mínimo:** crear/adaptar `AGENTS.md` y `project-methodology/` con datos propios; no copiar contenido del estándar.
5. **Adaptación técnica:** registrar comandos comprobados, pruebas, entornos y despliegue según stack.
6. **Piloto:** ejecutar una tarea pequeña autorizada de extremo a extremo con nivel de cambio y handoff proporcional.
7. **Revisión:** comprobar que otro agente puede recuperar contexto y continuar.
8. **Declaración:** registrar versión adoptada, excepciones y fecha/responsable.

## Proyecto existente con documentos dispersos

Si ya existen PROJECT_CONTEXT, PROJECT_STATE, ARCHITECTURE, TODO, DECISIONS o documentos visuales en la raíz u otra carpeta:

- inventariarlos primero;
- identificar cuál contiene la verdad vigente;
- moverlos a `project-methodology/` sólo si el movimiento es seguro y no rompe automatizaciones/enlaces;
- actualizar enlaces desde AGENTS/README cuando corresponda;
- no duplicar versiones que compitan como autoridad;
- preservar historial mediante Git.

La organización es una convención, no autorización para un refactor funcional.

## Preservación e independencia

No copiar los documentos normativos del SOURCE_REPO dentro de TARGET_REPO. El proyecto consumidor registra únicamente su contexto, estado, arquitectura, tareas, decisiones y diseño propios.

## Aceptación de adopción

- SOURCE_REPO quedó sin modificaciones.
- TARGET_REPO contiene una única autoridad documental clara.
- AGENTS.md referencia la metodología y dirige a `project-methodology/`.
- STATE refleja presente, TODO criterios verificables y DECISIONS razones duraderas.
- Actual/objetivo y probado/publicado están separados.
- Herramientas/comandos/destinos comprobados; secretos fuera.
- Otro agente puede determinar el siguiente paso sin leer el chat.

Para un proyecto nuevo sin funcionalidades, documentar “sin implementación”; no inventar pruebas o despliegues.

## Siguiente paso para el piloto

Elegir una tarea pequeña y de bajo riesgo en TARGET_REPO. La adopción documental no autoriza modificar SOURCE_REPO ni desplegar Producción.
