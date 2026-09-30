# Uso de ALEX Development Standard

Este repositorio es la **fuente canónica de la metodología**. No es un proyecto consumidor y no debe convertirse en uno.

## Regla principal

- `alexsennin/alex-development-standard` = **SOURCE_REPO / solo lectura durante adopciones**.
- El repositorio donde se desarrolla un producto = **TARGET_REPO / único lugar donde se crean o modifican archivos del proyecto**.

Durante una adopción, un agente puede leer `standards/v1.0/`, pero no debe editar, copiar encima ni adaptar esos archivos dentro de este repositorio.

## Protección conceptual de versiones

`standards/v1.0/` se considera una versión publicada e inmutable.

Si la metodología cambia:
- no sobrescribir v1.0;
- crear una nueva versión, por ejemplo `standards/v1.1/`;
- documentar diferencias y compatibilidad.

## Antes de adoptar en un proyecto

El agente debe comprobar y declarar:

1. SOURCE_REPO: `alexsennin/alex-development-standard`
2. SOURCE_VERSION: `standards/v1.0/`
3. TARGET_REPO: repositorio del producto
4. TARGET_ROOT: raíz del repositorio del producto
5. Rama y estado Git del TARGET_REPO

Si SOURCE_REPO y TARGET_REPO son el mismo repositorio, debe detenerse y no escribir nada.

## Qué se crea en el TARGET_REPO

Según aplique:
- `AGENTS.md`
- `PROJECT_CONTEXT.md`
- `PROJECT_STATE.md`
- `ARCHITECTURE.md`
- `TODO.md`
- `DECISIONS.md`

Si hay UI y aporta valor:
- `DESIGN_SYSTEM.md`
- `TOKENS.md`
- `COMPONENTS.md`
- `LAYOUTS.md`

Estos archivos describen al proyecto consumidor. No son copias del estándar.

## Qué nunca debe ocurrir durante una adopción

- editar `standards/v1.0/`;
- transformar este repositorio en documentación de un producto;
- crear archivos de contexto del producto dentro de este repositorio;
- copiar branding, dominio o deuda técnica de otro proyecto;
- hacer commits en SOURCE_REPO como parte de la adopción del TARGET_REPO.

La adopción termina únicamente con cambios en TARGET_REPO.
