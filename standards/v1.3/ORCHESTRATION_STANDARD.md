# Orquestación de capacidad e inteligencia

ALEX DEVELOPMENT STANDARD v1.3 añade una tercera dimensión operativa sin sustituir modos ni niveles:

- **Modo** (`PATCH/FEATURE/SYSTEM/CHECK/RELEASE`): qué proceso seguir y cuánto contexto cargar.
- **Nivel** (`1–4`): riesgo, impacto, reversibilidad, destino y controles.
- **Capacidad**: qué clase de modelo y esfuerzo de razonamiento necesita cada actividad o microtarea.

**Complejidad cognitiva y riesgo operativo no son equivalentes.** Una sentencia simple sobre datos reales puede ser Nivel 4; un análisis arquitectónico local puede exigir capacidad experta sin tocar Producción.

## Objetivo

Reservar modelos de mayor capacidad para reducir incertidumbre, diagnosticar, decidir y diseñar; convertir problemas complejos en unidades de comportamiento suficientemente acotadas para que modelos más eficientes las implementen y verifiquen con menor costo/contexto.

## Clases de capacidad

| Clase | Uso principal | Regla |
| --- | --- | --- |
| **ROUTER** | interpretar intención, detectar señales de riesgo y decidir si hace falta más análisis | barata y conservadora; si existe incertidumbre material, escala en vez de adivinar |
| **FOCUSED** | implementación mecánica/acotada con especificación clara | contexto mínimo, alcance cerrado, verificación focal |
| **ADVANCED** | lógica moderada, integración acotada, depuración con hipótesis razonable | mayor razonamiento sin asumir arquitectura nueva |
| **EXPERT** | causa raíz, arquitectura, contratos, decisiones complejas y planificación | reducir incertidumbre y producir instrucciones ejecutables |
| **FRONTIER** | ambigüedad extrema, decisiones de alto impacto o problema no resuelto tras análisis experto | uso excepcional; no es el default de programación |

Las clases son estables aunque cambien nombres comerciales. El proyecto/runtime mantiene un **perfil de mapping** actualizado.

### Mapping operativo de referencia — 2026-10-06

| Clase | Mapping sugerido |
| --- | --- |
| ROUTER | GPT-6 Luna · Bajo |
| FOCUSED | GPT-6 Luna · Alto |
| ADVANCED | GPT-6 Luna · Muy Alto o Máximo según naturaleza |
| EXPERT | Sol / GPT-6.1 Sol con razonamiento proporcional |
| FRONTIER | Astra cuando el problema justifique capacidad frontier |

El mapping no es una escalera rígida. **Más reasoning y un modelo más capaz son decisiones diferentes.** Ante diagnóstico/arquitectura puede ser mejor escalar a EXPERT que mantener un modelo eficiente en Máximo.

## Intake y clasificación inicial

El router empieza con el mínimo contexto razonable: solicitud, `AGENTS.md` y estado focal disponible. Determina intención, modo probable, nivel/riesgos evidentes y si la causa/solución es suficientemente clara.

- PATCH/Nivel 1 inequívoco puede enrutar directamente a FOCUSED y continuar sin plan ceremonial.
- Causa desconocida, varios subsistemas posibles, contratos/datos/auth/infra o decisiones arquitectónicas requieren escalar análisis antes de editar.
- Pocos archivos o ausencia de SQL no prueban baja complejidad ni bajo riesgo.

## Arquitecto → ejecutores

Cuando se requiere EXPERT/FRONTIER, su responsabilidad preferente es: reproducir/reunir evidencia; separar hechos e inferencias; identificar causa probable/raíz; diseñar solución; identificar riesgos/dependencias/compatibilidad; definir aceptación/pruebas; dividir por fases y microtareas; asignar capacidad y reasoning inicial.

El arquitecto no debe permanecer implementando tareas mecánicas sólo por haber realizado el análisis. Una vez reducida la incertidumbre, delegar a FOCUSED/ADVANCED cuando sea suficiente.

## Microtareas

Una microtarea debe ser pequeña para ejecutarse sin redescubrir el sistema, pero completa para dejar un comportamiento coherente. Debe declarar cuando aporte valor: objetivo, comportamiento esperado, contexto mínimo/contratos, límites, dependencias, aceptación, prueba, capacidad/modelo-reasoning y condición de escalamiento.

No dividir sólo por archivo, línea, import o función si rompe coherencia. Acciones mecánicas que juntas producen un comportamiento verificable pertenecen normalmente a la misma microtarea.

## Fases y checkpoints

Las microtareas relacionadas se agrupan en fases con resultado coherente. Para FEATURE compleja/SYSTEM, el plan debe ser visible antes de ejecutar cuando permita detectar malentendidos, modificar prioridades o limitar alcance.

El usuario puede autorizar una fase, varias o todo el plan. Dentro de ese alcance, el orquestador puede cambiar de agentes/modelos y continuar automáticamente sin pedir permiso en cada handoff. Un checkpoint reaparece al terminar el alcance autorizado o ante una condición de parada.

PATCH/Nivel 1 no requiere checkpoint adicional por rutina. FEATURE clara puede ejecutarse con plan interno breve.

## Escalamiento dinámico

Empezar con la capacidad mínima suficiente. Escalar cuando aparezca incertidumbre material, falle la hipótesis, cambien contratos/arquitectura, dos intentos equivalentes no resuelvan la causa o surja riesgo que el ejecutor no pueda justificar.

Al escalar: detener parche repetitivo; transferir objetivo/evidencia/hipótesis/intentos; conservar contexto válido; reanalizar con mayor capacidad; producir especificación corregida; y volver a capacidad eficiente para implementación cuando se resuelva la incertidumbre.

**No repetir el mismo enfoque más de dos veces sin nueva evidencia.** Escalar una microtarea no obliga a subir toda la sesión.

## Condiciones de parada

Detener la parte afectada y elevarla ante operación destructiva no contemplada; Producción/datos reales fuera del alcance; divergencia de migraciones/esquema/contratos; riesgo de auth/permisos/secretos; estado inseguro del destino; evidencia que contradice el plan; o necesidad de ampliar dominio/alcance.

## Autorización y delegación

La autorización del usuario se aplica a **qué** se hace y **dónde**, no a cada cambio interno de modelo. Un orquestador puede delegar automáticamente dentro de fases autorizadas. La delegación nunca concede RELEASE implícito, escritura en Producción, migración operativa, acceso adicional, ampliación de alcance ni operación destructiva no prevista.

`SYSTEM` sigue separado de `RELEASE`. `CHECK` sigue siendo el punto natural de consolidación.

## Runtime automático y compatibilidad manual

El Standard define comportamiento objetivo y no depende de una interfaz concreta.

- **Routing automático:** un orquestador/multiagente asigna modelo y reasoning por actividad y transfiere contexto.
- **Compatibilidad manual:** si el runtime no permite cambio automático, el agente solicita cambio de modelo/reasoning sólo en puntos de capacidad relevantes. La limitación no cambia modos, niveles, fases ni criterios.

El objetivo es que el usuario exprese intención, revise/ajuste planes cuando corresponda y autorice alcance; no que actúe como router permanente.

## Validación

La capacidad asignada no sustituye pruebas. Cada microtarea verifica aceptación; cada fase verifica coherencia; CHECK revisa diff acumulado; RELEASE aplica autorización y controles de destino. Para cambios críticos puede corresponder una revisión EXPERT independiente o segunda pasada explícita, pero no para tareas triviales.