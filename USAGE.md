# Uso de ALEX Development Standard

Este repositorio es la **fuente canónica de la metodología**. No es un proyecto consumidor y no debe convertirse en uno.

## Regla principal

- `alexsennin/alex-development-standard` = **SOURCE_REPO / solo lectura durante adopciones**.
- El repositorio del producto = **TARGET_REPO / único lugar donde se crean o modifican archivos del proyecto**.

Durante una adopción, un agente lee `standards/v1.3/`, pero no edita este repositorio.

## Estado de v1.3

ALEX DEVELOPMENT STANDARD v1.3 es la versión vigente y recomendada para adopción gradual. Conserva PATCH/FEATURE/SYSTEM/CHECK/RELEASE, niveles 1–4 y economía de contexto de v1.2; v1.0–v1.2 quedan históricas.

La [v1.3](standards/v1.3/README.md) conserva despliegue/migraciones de v1.2 y añade [orquestación de capacidad](standards/v1.3/ORCHESTRATION_STANDARD.md): routing por microtarea, clases de capacidad, fases, escalamiento y delegación interna.

## Antes de adoptar

Comprobar: SOURCE_REPO; SOURCE_VERSION=`standards/v1.3/`; TARGET_REPO; TARGET_ROOT; `<TARGET_ROOT>/project-methodology`; rama y estado Git. Si SOURCE_REPO y TARGET_REPO son iguales, detenerse sin escribir.

## Uso cotidiano

El usuario pide resultados normalmente. El agente infiere modo/nivel y enruta capacidad. PATCH/Nivel 1 permanece ligero. FEATURE compleja/SYSTEM puede mostrar plan por fases; el usuario puede autorizar una, varias o todas. CHECK consolida la ronda y RELEASE sólo se usa para publicar/desplegar con la autorización aplicable.

Si el runtime no soporta routing automático de modelos, usar el mismo plan en compatibilidad manual sin cambiar la metodología.