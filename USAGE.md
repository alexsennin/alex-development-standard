# Uso de ALEX Development Standard

ALEX DEVELOPMENT STANDARD **v1.3.2** es la versión vigente y de adopción obligatoria para trabajo nuevo o activo.

## Runtime recomendado
**AXIOM + Codex CLI** es la ruta oficial para aplicar capability routing automáticamente. AXIOM se ejecuta desde el directorio del proyecto y coordina modelos sin que el usuario opere el selector.

Codex CLI debe iniciar sesión con la cuenta de ChatGPT para el perfil económico predeterminado. En ese modo, el consumo utiliza la cuota de Codex del plan; no se configura una API key por defecto.

## Compatibilidad
Codex Desktop sigue siendo válido, pero el routing es manual. Iniciar con FOCUSED/Luna Alto; no usar Luna Bajo como modelo inicial esperando cambios automáticos.

## Adopción
1. SOURCE_VERSION = `standards/v1.3.2/`.
2. Leer `CORE.md` y `AXIOM_RUNTIME.md`.
3. Confirmar TARGET_REPO/TARGET_ROOT/rama/estado Git.
4. Leer `AGENTS.md` del proyecto.
5. Adoptar v1.3.2 antes del siguiente cambio sustantivo.

Proyectos reales iniciales: **Mundo de Colores, Docencia y Fema**.

## Producción
AXIOM no autoriza Producción por `publica`, `push` o `sube`. Sólo una instrucción explícita de desplegar/aplicar en Producción habilita RELEASE.