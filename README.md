# ALEX Development Standard

Metodología personal de desarrollo mediante vibecoding y agentes.

## Regla de uso

Este repositorio es la **fuente canónica y de solo lectura durante adopciones**. Los archivos específicos de cada proyecto deben crearse únicamente en el repositorio objetivo.

Leer primero: [USAGE.md](USAGE.md).

## Versiones

- [v1.2](standards/v1.2/README.md) — **vigente / recomendado para adopción gradual** (2026-10-05)
- [v1.1](standards/v1.1/README.md) — versión histórica (2026-10-03)
- [v1.0](standards/v1.0/README.md) — versión histórica (2026-09-30)

## Estructura

```text
alex-development-standard/
├── README.md
├── USAGE.md
└── standards/
    ├── v1.0/  # referencia histórica
    ├── v1.1/  # referencia histórica
    └── v1.2/  # versión central recomendada
```

Las versiones publicadas bajo `standards/` son referencias de **la metodología**, no números que deban crearse para cada despliegue de una aplicación. Se conserva el historial del estándar para que cada proyecto sepa qué reglas adoptó. Una publicación sencilla de código puede usar sólo el commit o identificador automático del proveedor; ver la [ruta rápida](standards/v1.2/DEPLOYMENT_STANDARD.md#ruta-rápida-paso-a-paso). La adopción de v1.2 se decide por repositorio y no modifica automáticamente los proyectos existentes.
