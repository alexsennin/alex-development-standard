# Gestión de cambios e iteración

ALEX DEVELOPMENT STANDARD v1.1 separa dos conceptos:

- **Nivel (1–4):** mide riesgo, impacto, reversibilidad y destino.
- **Modo:** determina cuánto proceso y contexto cargar en este momento.

## Modos

| Modo | Uso | Contexto | Verificación | Producción |
| --- | --- | --- | --- | --- |
| PATCH | bug pequeño, UI, texto, navegación, ajuste acotado | mínimo necesario | focal | prohibida |
| FEATURE | función/flujo nuevo o cambio funcional acotado | módulo + contratos afectados | comportamiento afectado | prohibida salvo transición explícita a RELEASE |
| SYSTEM | DB, auth, RLS, arquitectura, integración, infraestructura, migración | amplio y pertinente | dependencias/compatibilidad | no implícita |
| CHECK | cerrar una ronda de iteración | diff acumulado + estado pertinente | suite proporcional acumulada | no |
| RELEASE | publicar/desplegar versión validada | entrega + entornos + release state | pre/post deploy | sí, con autorización aplicable |

## Clasificación

El agente infiere PATCH, FEATURE o SYSTEM. Si hay duda material entre dos, usa el de mayor impacto sólo para la parte dudosa. No convertir automáticamente toda la sesión al modo más pesado por una dependencia aislada.

El usuario puede forzar el modo con `PATCH:`, `FEATURE:`, `SYSTEM:`, `CHECK:` o `RELEASE:`. No son comandos técnicos; son intenciones metodológicas.

## PATCH

1. Confirmar repositorio/área afectada y preservar cambios ajenos.
2. Leer sólo instrucciones y código necesarios para localizar la causa.
3. Hacer el cambio mínimo coherente.
4. Ejecutar prueba focal pertinente.
5. Informar resultado y cualquier riesgo descubierto.

No releer toda la arquitectura, revisar historial remoto de migraciones, ejecutar suites completas, actualizar STATE/TODO/DECISIONS ni preparar despliegue salvo que la verdad correspondiente haya cambiado. Si el cambio toca DB/auth/infra, escalar a SYSTEM.

## FEATURE

Recuperar contexto del módulo y contratos afectados; definir aceptación observable; implementar por unidades revisables; probar el flujo afectado; actualizar sólo documentación cuya verdad cambió. Puede acumularse con otros cambios durante una ronda antes de CHECK.

## SYSTEM

Aplicar análisis de dependencias, arquitectura, datos, autorización, compatibilidad y recuperación pertinentes. Las migraciones pueden diseñarse y probarse en local/aislado. Tocar Producción sigue requiriendo RELEASE.

## CHECK — consolidación

CHECK significa “esta ronda está lista para revisión”.

1. Revisar diff acumulado y alcance.
2. Detectar regresiones, cambios accidentales y secretos.
3. Ejecutar pruebas acumuladas pertinentes; no repetir pruebas que sigan siendo válidas sin razón.
4. Actualizar documentación cuya verdad cambió.
5. Identificar migraciones/configuración pendientes.
6. Crear commit(s) y push cuando la política/alcance lo indiquen.
7. Actualizar RELEASE_STATE cuando exista y haya cambiado.
8. Entregar estado: listo para RELEASE, bloqueado o requiere nueva iteración.

CHECK no despliega.

## RELEASE — entrega

RELEASE ejecuta DEPLOYMENT_STANDARD. Debe identificar versión, destino, automatizaciones, migraciones/configuración, autorización, recuperación y evidencia posterior. Si un push dispara Producción, ese push forma parte de RELEASE y no de un PATCH/CHECK ordinario.

## Economía de contexto

1. **Contexto progresivo:** empezar con lo mínimo suficiente y ampliar por evidencia.
2. **No redescubrir:** si una verdad estable ya está documentada y no hay señal de divergencia, usarla.
3. **No revalidar por ritual:** revalidar cuando el cambio pueda invalidar evidencia previa.
4. **Agrupar trabajo costoso:** suites amplias, revisión integral, documentación de estado y preparación de release se concentran en CHECK.
5. **Separar desarrollo de operación:** preparar una migración no equivale a aplicarla; crear código no equivale a desplegarlo.
6. **Escalar, no reiniciar:** si PATCH descubre impacto estructural, conservar lo aprendido y continuar como SYSTEM sin repetir investigación válida.

## Relación modo/nivel

No existe equivalencia rígida. Un PATCH suele ser Nivel 1–2; FEATURE suele ser Nivel 2; SYSTEM suele ser Nivel 3. RELEASE añade consecuencias de Nivel 4 cuando toca Producción/datos reales. El nivel puede elevar controles sin obligar a releer contexto irrelevante.
