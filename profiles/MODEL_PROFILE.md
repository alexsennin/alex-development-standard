# MODEL PROFILE — vigente para ALEX v1.3.2 / AXIOM

Fecha del perfil: 2026-10-06. Este archivo es **operativo, no normativo**. Puede actualizarse cuando cambie el catálogo de modelos sin crear una nueva versión del ALEX Development Standard.

| Capability | Modelo / reasoning actual |
| --- | --- |
| ROUTER | GPT-6 Luna · Bajo |
| FOCUSED | GPT-6 Luna · Alto |
| ADVANCED | GPT-6 Luna · Muy Alto; Máximo sólo cuando la naturaleza de ejecución lo justifique |
| EXPERT | GPT-6.1 Sol con reasoning proporcional; Sol equivalente si es la opción disponible |
| FRONTIER | Astra cuando la ambigüedad/impacto justifique capacidad frontier |

Reglas:
- No tratar reasoning como escalera obligatoria antes de cambiar de modelo.
- Para causa raíz/arquitectura, preferir EXPERT antes que forzar indefinidamente un modelo eficiente en Máximo.
- Para implementación especificada y mecánica, volver a FOCUSED/ADVANCED.
- El costo es señal de routing, nunca razón para rebajar seguridad, autorización o revisión obligatoria.
## Perfil por runtime

### AXIOM — automático
- ROUTER: GPT-6 Luna · Bajo; sólo clasificación estructurada, sin escritura.
- FOCUSED/ADVANCED/EXPERT/FRONTIER: AXIOM selecciona automáticamente según capability.

### Codex Desktop — compatibilidad manual
- Modelo inicial recomendado: **FOCUSED / GPT-6 Luna · Alto**.
- No iniciar con Luna Bajo esperando routing automático.
- Si el Standard requiere EXPERT/FRONTIER/ADVANCED diferente, el usuario cambia el selector manualmente.

AXIOM debe mantener los identificadores exactos de modelos como configuración reemplazable; si un nombre deja de estar disponible, se actualiza este perfil/runtime sin cambiar la metodología.