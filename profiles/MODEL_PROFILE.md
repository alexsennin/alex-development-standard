# MODEL PROFILE — ARC (perfil operativo multiplataforma)

Este archivo es **operativo, no normativo**. Puede actualizarse cuando cambien modelos, cuotas y entornos sin cambiar las reglas de ARC. Los nombres listados representan las opciones preferidas del usuario; comprobar su disponibilidad exacta en el selector antes de utilizarlos.

## Preferencias de trabajo

| Capacidad / actividad | Preferencia en Antigravity | Preferencia en Codex |
| --- | --- | --- |
| ROUTER (clasificación sin escritura) | Gemini 3.8 Flash | GPT-6.1 Terra |
| FOCUSED (tareas concretas, bien acotadas) | Gemini 3.8 Flash | GPT-6.1 Terra |
| ADVANCED (ejecución con varias piezas, pruebas) | Gemini 3.8 Flash; escalar si no es suficiente | GPT-6.1 Terra; escalar si no es suficiente |
| EXPERT (diagnóstico, arquitectura y revisión de riesgo) | Gemini 4 Argon | GPT-6.1 Sol |
| FRONTIER (casos extraordinarios) | Mejor capacidad disponible justificada por el problema | Mejor capacidad disponible justificada por el problema |

**Principio:** recomendar el modelo de menor consumo esperado con capacidad suficiente para la tarea, sin reducir seguridad ni pruebas. La recomendación concreta se registra en `TASK_MANAGEMENT.md`/TODO de cada proyecto cuando aporte valor.

## Reglas de selección

- La **capacidad** se define por las tres dimensiones de CORE; la **marca/modelo** es una asignación operativa y reemplazable.
- Los cambios pequeños y de riesgo bajo pueden iniciarse directamente en FOCUSED; la incertidumbre de causa raíz, arquitectura, autenticación, permisos, pagos, migraciones, datos, Producción o infraestructura exige análisis EXPERT antes de editar según CORE.
- Un análisis EXPERT puede entregar un Execution Packet para que FOCUSED/ADVANCED implemente la parte segura.
- No escalar por ritual ni repetir un mismo intento más de dos veces sin evidencia nueva.
- Codex y Antigravity **no cambian de modelo automáticamente** por leer este documento. El usuario o las capacidades explícitas del entorno deciden el modelo activo.
- Si el modelo sugerido no está disponible, usar una alternativa de capacidad suficiente y registrar la desviación si afecta la tarea.
- No asumir equivalencias exactas de calidad, precios, tokens ni cuotas entre proveedores sin una medición comparable.

## AXIOM (opcional)

Si se ejecuta AXIOM, este puede elegir modelo y razonamiento automáticamente conforme a `standards/v1.3.2/AXIOM_RUNTIME.md` y su propia configuración. Esa automatización **no es un requisito de ARC**.

Los identificadores exactos de modelos y su disponibilidad pertenecen al adaptador/runtime que los invoque, no al contrato normativo de ARC.
