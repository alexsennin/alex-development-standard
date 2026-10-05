# ALEX DEVELOPMENT STANDARD v1.2 — Engineering Standard

Documento raíz. Estado: **propuesta v1.2 para revisión**, 2026-10-05. La v1.1 sigue siendo la versión central recomendada hasta que se apruebe esta propuesta. Piloto no iniciado; no adoptado universalmente. Independiente de lenguaje, framework, proveedor, dominio e identidad visual.

## Principios obligatorios

1. Comprender el proyecto antes de editar: propósito, estado, restricciones, arquitectura actual y tareas.
2. Cada tarea tiene problema, alcance y criterio de aceptación verificable. Una intención vaga se concreta antes de implementar.
3. Realizar cambios pequeños que puedan revisarse y comprobarse por unidad. No reescribir módulos completos sin demostrar necesidad y acordar alcance.
4. Preservar cambios ajenos y funcionalidades existentes; no borrar ni alterar comportamiento fuera del objetivo sin justificación.
5. Separar implementación actual, arquitectura objetivo y propuesta. Una descripción futura no es evidencia de implementación.
6. Reutilizar contratos, componentes y convenciones cuando encajen. La duplicación o el acoplamiento accidental no se convierten en reglas por existir.
7. Validar antes de publicar. Elegir comprobaciones que demuestren el comportamiento afectado; no confundir compilación con recorrido funcional.
8. Local, Git remoto y Producción son estados independientes. Identificar el destino y la revisión disponible de cada uno cuando intervengan; no crear una numeración manual de versiones por rutina.
9. El chat es memoria temporal y el repositorio es memoria persistente. Guardar conocimiento útil en documentos pertinentes sin convertirlos en transcripciones.
10. Documentar decisiones importantes y mantener trazabilidad problema → tarea → cambio → verificación → commit → entrega, y despliegue cuando aplica.
11. No dejar trabajo importante únicamente en local. Commit, push y verificación remota forman parte del cierre cuando corresponde según la política del proyecto; el trabajo importante debe respaldarse en remoto. Si están bloqueados, informar el estado incompleto.
12. Proteger secretos y datos personales; usar fixtures aislados. Git respalda código, no garantiza respaldo de datos o archivos operativos.
13. Validar autorización en la autoridad efectiva del sistema, no sólo en presentación. Cuando hay datos compartidos o sensibles, comprobar también alcance y denegaciones.
14. Cuando una operación requiere integridad entre varios cambios, preservar atomicidad, idempotencia o compensación adecuada; no imponer un mecanismo de DB específico.
15. Comunicar evidencia y límites con precisión. “No verificado”, “omitido” y “falló” son resultados distintos.
16. **Actualizar únicamente los documentos cuya verdad haya cambiado.** La documentación preserva contexto útil, no actividad administrativa; aplicar [la regla contra la sobredocumentación](PROJECT_DOCUMENTATION.md#regla-contra-la-sobredocumentación).

## Autonomía y límites

El agente ejecuta el alcance autorizado y resuelve decisiones rutinarias de implementación. Sólo pide información o autorización que falte realmente; no vuelve a pedirla si ya fue otorgada. No amplía dominio, sustituye diseño o publica en un destino diferente por su cuenta.

Despliegues, migraciones operativas y otras acciones con consecuencias externas siguen la política del proyecto y la autorización aplicable. Preparar el resultado revisable antes de pedir aprobación final. Los roles conceptuales no autorizan delegación automática.

## Marco adaptable

El núcleo establece resultados, no carpetas de código, proveedores o comandos universales. Cada proyecto declara stack, entorno de trabajo seguro, herramientas, comandos comprobados, estrategia de ramas y publicación. En stacks sin ejecución local completa, usar sandbox o entorno de ensayo identificado; no simular persistencia ni afirmar prueba local inexistente.

Una arquitectura debe responder a necesidades y restricciones. Refactor justificado por riesgo, mantenibilidad o un cambio concreto, con migración gradual y comprobación. No imponer capas, microservicios o librería de componentes como requisito universal.

## Modos de trabajo y economía de contexto

Antes de aplicar la carga completa del proceso, clasificar la intervención por **modo de trabajo**. El modo regula cuánto contexto, análisis y cierre cargar; el nivel de cambio sigue regulando el riesgo. Ver [CHANGE_MANAGEMENT.md](CHANGE_MANAGEMENT.md).

- **PATCH:** corrección acotada y reversible. Cargar sólo contexto directamente necesario; no reauditar arquitectura, entornos, despliegue o DB si no están afectados.
- **FEATURE:** funcionalidad o flujo nuevo/acotado. Analizar módulo, contratos y dependencias afectados; ampliar contexto sólo cuando la evidencia lo exija.
- **SYSTEM:** cambios de arquitectura, datos, auth, permisos, infraestructura, integraciones o migraciones. Aplicar recuperación y análisis amplios pertinentes.
- **CHECK:** consolidar una ronda de cambios: revisar diff conjunto, ejecutar verificaciones acumuladas pertinentes y dejar una versión candidata a entrega.
- **RELEASE:** operación explícita de publicación/despliegue. Es el único modo que habilita operaciones de Producción y sigue DEPLOYMENT_STANDARD.

El agente debe inferir PATCH/FEATURE/SYSTEM cuando sea claro. CHECK y RELEASE requieren intención explícita del usuario o una autorización ya vigente e inequívoca. **Una petición de corregir o implementar no implica autorización para desplegar.**

Principio de economía de contexto: no releer, revalidar ni reconstruir información estable sin una razón ligada al cambio. Escalar el modo si durante el trabajo aparece mayor impacto.

## Niveles de cambio

Esta es la definición principal; [tareas](TASK_MANAGEMENT.md) y [pruebas](TESTING_STANDARD.md) la aplican sin copiarla. Clasificar por impacto, alcance, reversibilidad y destino, no sólo por cantidad de líneas. Si concurren varios niveles, aplicar el más alto pertinente; los ejemplos no son permisos para rebajar riesgo.

| Nivel | Tipo y ejemplos | Profundidad requerida |
| --- | --- | --- |
| 1 — Cambio trivial | Texto, documentación menor, ajuste visual pequeño o configuración no crítica; alcance reducido, bajo riesgo y reversión fácil | Aceptación breve, comprobación directa y revisión del diff; documentación sólo si cambió su verdad; handoff mínimo |
| 2 — Cambio funcional | Bug, feature, cambio de flujo o refactor acotado | Criterio verificable, pruebas del comportamiento afectado, revisión del diff y documentación pertinente; handoff completo proporcional |
| 3 — Cambio estructural | Arquitectura, autenticación, autorización, contratos, DB, integraciones, migraciones o cambios importantes de diseño | Mayor análisis de dependencias/compatibilidad, decisiones explícitas cuando corresponde, pruebas más amplias y revisión de consecuencias |
| 4 — Cambio crítico | Datos reales, pagos, seguridad o permisos críticos, migración destructiva, DNS u operación difícil de revertir en Producción | Riesgo identificado, autorización aplicable, estrategia de recuperación, evidencia reforzada y verificación posterior |

Los niveles regulan análisis, documentación, pruebas, revisión, autorización y recuperación. **No generan formularios ni documentos extra por sí solos.** No requieren agentes separados ni aprobaciones redundantes. Nivel 1 no lleva la carga documental de Nivel 4; aceptación y evidencia pueden quedar en el diff y el handoff breve.

Un cambio estructural puede ser crítico por destino o consecuencias. Publicar un texto o ajuste visual reversible en Producción puede seguir la [ruta rápida](DEPLOYMENT_STANDARD.md#ruta-rápida-paso-a-paso), con confirmación del destino y prueba posterior, sin heredar el proceso de una migración crítica. Si el riesgo aumenta durante la sesión, reclasificar y ajustar plan/verificación antes de continuar la parte afectada.

## Criterios de terminado proporcionales

- Aceptación cumplida; escribir código, compilar o crear un commit por sí solos no completan una tarea.
- Comprobaciones pertinentes al nivel y comportamiento afectados, con resultado y límites; no exigir pruebas irrelevantes para un cambio trivial.
- Diff dentro del alcance y cambios ajenos preservados.
- Sólo los documentos cuya verdad cambió están actualizados; no editar todos los documentos por rutina.
- Estado Git explícito, commits de la entrega según política y push cuando corresponde. No dejar trabajo importante únicamente en local; si falta respaldo/revisión requerido, registrar cierre incompleto.
- Handoff proporcional: mínimo para cambios simples, completo para funcionales/estructurales/críticos; destino, recuperación y verificación posterior cuando aplican.

Una tarea implementada puede estar pendiente de revisión o despliegue. Si el alcance era preparar una entrega, puede cerrarse sin desplegar, dejando el despliegue pendiente explícito. Un cierre bloqueado puede entregar trabajo útil, pero no se declara completamente respaldado o publicado.

## Vocabulario de evidencia

| Término | Significado en v1.2 |
| --- | --- |
| Implementado | Cambio presente en código/configuración/documentación; no demuestra ejecución correcta |
| Probado | Comprobación pertinente ejecutada, con resultado, versión y entorno; indicar aprobación, fallo y límites |
| Publicado | Entregable disponible en un destino externo identificado, por ejemplo una rama Git; no equivale a desplegado |
| Desplegado | Versión aplicada al entorno de ejecución identificado; no demuestra recorrido funcional |
| Verificado en Producción | Comprobaciones pertinentes ejecutadas sobre la versión/destino de Producción; indicar alcance y si fue parcial |

Son hechos independientes, no una etiqueta única de progreso. Una publicación en Git no se llama despliegue; una versión desplegada puede seguir sin verificación en Producción. “Debe” identifica requisito; “recomendado”, práctica adaptable; “cuando aplica”, condición que se debe evaluar, no una excepción implícita.

## Documentos que desarrollan estas reglas

[Flujo de agentes](AGENT_WORKFLOW.md), [contexto](CONTEXT_MANAGEMENT.md), [Git](GIT_WORKFLOW.md), [documentación](PROJECT_DOCUMENTATION.md), [handoff](SESSION_HANDOFF.md), [decisiones](DECISION_MANAGEMENT.md), [tareas](TASK_MANAGEMENT.md), [pruebas](TESTING_STANDARD.md), [despliegue](DEPLOYMENT_STANDARD.md), [diseño](DESIGN_STANDARD.md) y [adopción](PROJECT_ADOPTION.md).
