# Reporte de creación y cierre de ALEX DEVELOPMENT STANDARD v1.0

Fecha: 2026-09-30. Estado formal: **ALEX DEVELOPMENT STANDARD v1.0 — aprobado para piloto**. Piloto aún no iniciado.

## Origen

La metodología se extrajo inicialmente de patrones observados en `alexsennin/mundo-de-colores-inventario`, separando principios reutilizables de stack, dominio, identidad y deuda técnica.

## Principios consolidados

- comprender contexto antes de editar;
- cambios pequeños y aceptación verificable;
- preservar trabajo ajeno;
- separar implementación actual, objetivo y propuesta;
- evidencia proporcional por nivel de cambio;
- contexto persistente en el repositorio;
- decisiones/tareas trazables;
- Git/remoto separados de despliegue/Producción;
- handoff proporcional;
- evitar sobredocumentación.

## Convención estructural añadida antes del piloto

Por decisión de Alex, la documentación específica de cada proyecto consumidor se organiza por defecto así:

```text
<TARGET_ROOT>/
├── AGENTS.md
└── project-methodology/
    ├── PROJECT_CONTEXT.md
    ├── PROJECT_STATE.md
    ├── ARCHITECTURE.md
    ├── TODO.md
    ├── DECISIONS.md
    └── design/
        ├── DESIGN_SYSTEM.md
        ├── TOKENS.md
        ├── COMPONENTS.md
        └── LAYOUTS.md
```

Motivo: mantener la raíz del proyecto limpia y separar claramente código/configuración de la memoria metodológica del producto.

`AGENTS.md` permanece en la raíz como puerta de entrada para agentes. `design/` se crea sólo cuando exista UI y aporte valor.

Esta convención se incorporó antes de iniciar el primer piloto, por lo que permanece dentro de v1.0. Una vez iniciado el piloto, cambios posteriores de metodología deberán versionarse explícitamente.

## Separación SOURCE / TARGET

- SOURCE_REPO: `alexsennin/alex-development-standard`, sólo lectura durante adopciones.
- SOURCE_VERSION: `standards/v1.0/`.
- TARGET_REPO: repositorio del producto, único lugar de escritura de la adopción.

Una adopción debe detenerse si SOURCE_REPO y TARGET_REPO son iguales.

## Uso

**Proyecto nuevo:** inicializar contexto real bajo `project-methodology/`, dejando AGENTS en raíz.

**Proyecto existente:** inventariar documentación previa, resolver autoridad y mover/adaptar de forma segura sin duplicar ni refactorizar funcionalidad sólo para adoptar.

## Estado

v1.0 está lista para piloto. La efectividad práctica sigue pendiente de ejecutar una adopción en un proyecto consumidor y una tarea pequeña de extremo a extremo.
