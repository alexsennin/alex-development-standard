# Informe de aprobación v1.3

Fecha: 2026-10-06. Estado: **vigente y recomendada para adopción gradual**, por decisión de Alex. No se adopta automáticamente; v1.2 queda histórica.

## Motivo

v1.2 resolvió carga excesiva de contexto y despliegue, pero la selección de inteligencia seguía implícita. Usar modelos costosos durante toda la implementación desperdicia capacidad; pedir a modelos eficientes que descubran causa raíz/arquitectura aumenta iteraciones y parches.

## Cambios

- Capability routing separado de modo y nivel.
- Router económico y escalamiento conservador.
- Capacidad experta para diagnóstico/arquitectura/descomposición.
- Ejecución por microtareas verificables con capacidad mínima suficiente.
- Fases y autorización por alcance; delegación interna automática.
- Escalamiento dinámico, límite de intentos equivalentes y stop conditions.
- Compatibilidad manual para runtimes sin routing automático.

## Compatibilidad

v1.3 conserva PATCH/FEATURE/SYSTEM/CHECK/RELEASE, niveles 1–4, contexto progresivo, CHECK, RELEASE, despliegue y migraciones de v1.2. No introduce QUICK/STANDARD/CRITICAL. SYSTEM no implica RELEASE y cambiar de modelo no concede permisos operativos.