# Gestión de cambios e iteración

ARC DEVELOPMENT STANDARD v1.3.2 separa tres dimensiones:

- **Nivel (1–4):** mide riesgo, impacto, reversibilidad y destino.
- **Modo:** determina cuánto proceso y contexto cargar en este momento.
- **Capacidad:** determina el modelo/clase de razonamiento apropiado para cada actividad o microtarea, sin alterar el riesgo ni la autorización.

## Modos

| Modo | Uso | Contexto | Verificación | Producción |
| --- | --- | --- | --- | --- |
| PATCH | bug pequeño, UI, texto, navegación, ajuste acotado | mínimo necesario | focal | prohibida |
| FEATURE | función/flujo nuevo o cambio funcional acotado | módulo + contratos afectados | comportamiento afectado | prohibida salvo transición explícita a RELEASE |
| SYSTEM | DB, auth, RLS, arquitectura, integración, infraestructura, migración | amplio y pertinente | dependencias/compatibilidad | no implícita |
| CHECK | cerrar una ronda de iteración | diff acumulado + estado pertinente | suite proporcional acumulada | no |
| RELEASE | desplegar/aplicar una entrega validada a un entorno | ruta rápida: cambio y destino; ampliada: capas implicadas | pre/post deploy proporcional | sí, con autorización aplicable |

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
5. Identificar migraciones/configuración pendientes sólo si el cambio o una dependencia conocida las incluye.
6. Crear commit(s) y push cuando la política/alcance lo indiquen.
7. Actualizar RELEASE_STATE cuando exista y haya cambiado.
8. Entregar estado: listo para RELEASE, bloqueado o requiere nueva iteración.

CHECK no despliega.

## RELEASE — entrega

RELEASE ejecuta [DEPLOYMENT_STANDARD](DEPLOYMENT_STANDARD.md#elegir-la-ruta-de-despliegue). Primero decide si basta la ruta rápida de archivos o si hay efectos de datos, contratos o varios destinos. La ruta rápida usa el identificador automático disponible, verificación focal y cierre breve; no requiere versión numerada, conciliación de migraciones ni respaldo de DB. La ruta ampliada comprueba únicamente las capas implicadas. Si un push dispara Producción, ese push forma parte de RELEASE y no de un PATCH/CHECK ordinario.

## Economía de contexto

1. **Contexto progresivo:** empezar con lo mínimo suficiente y ampliar por evidencia.
2. **No redescubrir:** si una verdad estable ya está documentada y no hay señal de divergencia, usarla.
3. **No revalidar por ritual:** revalidar cuando el cambio pueda invalidar evidencia previa.
4. **Agrupar trabajo costoso:** suites amplias, revisión integral, documentación de estado y preparación de release se concentran en CHECK.
5. **Separar desarrollo de operación:** preparar una migración no equivale a aplicarla; crear código no equivale a desplegarlo.
6. **Escalar, no reiniciar:** si PATCH descubre impacto estructural, conservar lo aprendido y continuar como SYSTEM sin repetir investigación válida.

## Tres dimensiones y rutas internas

**Modo, nivel y capacidad son los únicos tres ejes de clasificación.** La ruta rápida o ampliada no es un cuarto eje: es una decisión interna de `RELEASE` según los efectos reales de la entrega.

## Relación modo/nivel

No existe equivalencia rígida. Un PATCH suele ser Nivel 1–2; FEATURE suele ser Nivel 2; SYSTEM suele ser Nivel 3. RELEASE añade comprobaciones del destino; sólo exige controles de Nivel 4 cuando sus efectos son críticos. El nivel puede elevar controles sin obligar a releer contexto irrelevante.

## Relación con capability routing

La clasificación de modo y nivel ocurre antes o en paralelo a la selección de capacidad. No crear modos QUICK/STANDARD/CRITICAL: PATCH/FEATURE/SYSTEM/CHECK/RELEASE siguen siendo la única taxonomía de proceso.

Una parte dudosa puede escalar de capacidad sin convertir toda la sesión al modelo más costoso. Una microtarea fácil dentro de SYSTEM puede ejecutarse con capacidad focal sin rebajar controles estructurales. Aplicar [ORCHESTRATION_STANDARD.md](ORCHESTRATION_STANDARD.md).

**Escalar, no reiniciar** también aplica a modelos/agentes: transferir objetivo, evidencia, hipótesis probadas, resultado observado y contexto mínimo pertinente; no repetir investigación válida sólo porque cambia el ejecutor.