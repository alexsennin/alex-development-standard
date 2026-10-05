# Uso de ALEX Development Standard

Este repositorio es la **fuente canónica de la metodología**. No es un proyecto consumidor y no debe convertirse en uno.

## Regla principal

- `alexsennin/alex-development-standard` = **SOURCE_REPO / solo lectura durante adopciones**.
- El repositorio donde se desarrolla un producto = **TARGET_REPO / único lugar donde se crean o modifican archivos del proyecto**.

Durante una adopción, un agente puede leer `standards/v1.1/`, pero no debe editar, copiar encima ni adaptar esos archivos dentro de este repositorio.

## Estado de v1.1

ALEX DEVELOPMENT STANDARD v1.1 es la versión vigente recomendada. Introduce modos de iteración PATCH/FEATURE/SYSTEM/CHECK/RELEASE y economía de contexto. v1.0 permanece como referencia histórica inmutable.

La [propuesta v1.2](standards/v1.2/README.md) añade una ruta rápida de publicación para cambios sólo de archivos, una ruta ampliada con [protocolo de migraciones](standards/v1.2/MIGRATION_STANDARD.md), una [guía de pedidos](standards/v1.2/PROMPTING_GUIDE.md) y un [agente semanal opcional](standards/v1.2/WEEKLY_RECONCILIATION_AGENT.md). Aún no reemplaza v1.1 ni se adopta automáticamente en productos.

## Antes de adoptar en un proyecto

El agente debe comprobar y declarar:

1. SOURCE_REPO: `alexsennin/alex-development-standard`
2. SOURCE_VERSION: `standards/v1.1/`
3. TARGET_REPO: repositorio del producto
4. TARGET_ROOT: raíz del repositorio del producto
5. TARGET_METHODOLOGY_DIR: `<TARGET_ROOT>/project-methodology`
6. Rama y estado Git del TARGET_REPO

Si SOURCE_REPO y TARGET_REPO son el mismo repositorio, debe detenerse y no escribir nada.

## Estructura recomendada del proyecto consumidor

```text
<TARGET_ROOT>/
├── AGENTS.md
├── README.md
├── <código y configuración del proyecto>
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

`AGENTS.md` permanece en la raíz como **puerta de entrada** para agentes y debe enlazar a `project-methodology/`.

La carpeta `project-methodology/` contiene la memoria persistente y la aplicación local de la metodología. No contiene copias de los documentos normativos de ALEX DEVELOPMENT STANDARD.

`project-methodology/design/` existe sólo si el proyecto tiene UI y esos documentos aportan valor real. No crear archivos o carpetas vacíos para aparentar cumplimiento.

## Qué nunca debe ocurrir durante una adopción

- editar `standards/v1.1/` desde una sesión de adopción;
- transformar este repositorio en documentación de un producto;
- crear archivos de contexto del producto dentro de SOURCE_REPO;
- copiar los documentos normativos del estándar dentro del proyecto consumidor;
- copiar branding, dominio o deuda técnica de otro proyecto;
- hacer commits en SOURCE_REPO como parte de la adopción del TARGET_REPO.

La adopción termina únicamente con cambios en TARGET_REPO.


## Uso cotidiano tras adoptar v1.1

Durante pruebas iterativas, el usuario puede pedir correcciones normalmente; el agente infiere PATCH/FEATURE/SYSTEM. También puede declarar el modo explícitamente. Usar CHECK al terminar una ronda de correcciones y RELEASE sólo cuando se quiera publicar/desplegar. No ejecutar el protocolo completo de Producción durante PATCH o FEATURE.
