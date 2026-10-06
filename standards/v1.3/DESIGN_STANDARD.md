# Estándar de diseño

La metodología exige coherencia y evidencia visual; no impone paleta, tipografía, radios, navegación, biblioteca UI ni breakpoints de un producto concreto.

## Ubicación recomendada

Cuando el proyecto tiene UI y estos documentos aportan valor:

```text
project-methodology/
└── design/
    ├── DESIGN_SYSTEM.md
    ├── TOKENS.md
    ├── COMPONENTS.md
    └── LAYOUTS.md
```

No crear `design/` por obligación si no existe UI o no aporta información útil.

## Antes de modificar UI

Comprender usuarios, tarea, estados y restricciones. Leer el sistema de diseño/identidad existente e inspeccionar componentes/layouts del flujo. Preservar decisiones aprobadas fuera del alcance.

Si no existe diseño documentado, extraer lo implementado y distinguir inconsistencias de decisiones aceptadas. No inventar estilos por pantalla ni copiar la marca de otro proyecto.

## Documentar y reutilizar

| Ruta | Contenido |
| --- | --- |
| `project-methodology/design/DESIGN_SYSTEM.md` | Principios, identidad, jerarquía, interacción y accesibilidad |
| `project-methodology/design/TOKENS.md` | Valores exactos, origen, nombres semánticos y variantes |
| `project-methodology/design/COMPONENTS.md` | Componentes/clases disponibles, variantes, estados y límites |
| `project-methodology/design/LAYOUTS.md` | Estructuras repetidas, restricciones de ancho, overflow y adaptación cuando aporta claridad |

Reutilizar tokens/patrones existentes. No congelar deuda visual como estándar. Overrides acumulados, contrastes insuficientes o inconsistencias se registran como hallazgos, no como patrones a copiar.

## Comportamiento de componentes

Definir cuando aplica: default, hover, focus, disabled, loading, error, empty, success y selected. Mantener etiquetas, foco visible, semántica, accesibilidad y responsive.

## Verificación y referencias

Las capturas/referencias deben indicar fecha, versión, pantalla/flujo, viewport y usar datos ficticios/anonimizados. Sin comprobación en navegador, describir la revisión como estática y señalar su límite.

Cambios de identidad/patrón se registran en `project-methodology/DECISIONS.md` y en los documentos de diseño pertinentes.
