# Adopción de ARC DEVELOPMENT STANDARD v1.3.2

Procedimiento para aplicar la metodología en un repositorio existente o nuevo. **v1.3.2 es la versión obligatoria para todo trabajo nuevo o activo realizado bajo ARC Development Standard.** La publicación central no modifica automáticamente repositorios consumidores: cada repositorio debe adoptar explícitamente v1.3.2 antes de su siguiente cambio sustantivo.

El [agente de conciliación semanal](WEEKLY_RECONCILIATION_AGENT.md) es opcional: sólo se programa para proyectos y destinos elegidos expresamente, después de identificar sus fuentes de evidencia. La adopción documental del estándar no crea una automatización por sí misma.

## Preflight obligatorio

Antes de escribir:

1. Confirmar SOURCE_REPO = `alexsennin/alex-development-standard`.
2. Confirmar SOURCE_VERSION = `standards/v1.3.2/`.
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
6. **Primera ejecución real:** aplicar v1.3.2 sobre trabajo real del proyecto. Preferir AXIOM para routing automático; si no está instalado/disponible, usar Codex Desktop en compatibilidad manual sin cambiar la metodología.
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

## Entrada en operación

Tras declarar la adopción, continuar con la tarea real que motivó la sesión. Si se usa AXIOM, ejecutarlo desde `TARGET_ROOT`; debe detectar el proyecto, leer `AGENTS.md` y aplicar `CORE.md` antes de enrutar. No se exige un proyecto piloto separado. La adopción documental no autoriza modificar SOURCE_REPO ni desplegar Producción.
