# Estándar de pruebas y evidencia

Verificar lo necesario para el comportamiento y riesgo afectados. No imponer comandos, herramientas o porcentajes universales de cobertura. Cada proyecto documenta sus comandos reales y requisitos de entorno.

## Profundidad según cambio

Aplicar los [niveles definidos en ENGINEERING_STANDARD](ENGINEERING_STANDARD.md#niveles-de-cambio): comprobación directa para lo trivial, comportamiento afectado para lo funcional, dependencias/compatibilidad para lo estructural y evidencia reforzada/recuperación/verificación posterior para lo crítico. La selección depende del riesgo real, sin replicar aquí la clasificación ni generar pruebas irrelevantes.

Reclasificar cuando la sesión descubre mayor riesgo. [Terminado](ENGINEERING_STANDARD.md#criterios-de-terminado-proporcionales) exige aceptación y evidencia pertinente; un build o un commit solos no bastan, ni se exige DB/E2E a una corrección documental menor. Usar el [vocabulario de evidencia](ENGINEERING_STANDARD.md#vocabulario-de-evidencia) en los resultados.

## Selección proporcional

| Cambio | Evidencia esperada cuando aplica |
| --- | --- |
| Documentación | Exactitud frente a fuentes, enlaces, coherencia, alcance del diff y comprobación de formato |
| Lógica pura | Casos de éxito, límites y errores que distinguen comportamiento correcto |
| Integración/API | Contratos de entrada/salida, error, timeout/reintento y persistencia según efecto |
| Datos/autorización | Acceso permitido y denegado, alcance, restricciones, migración y compatibilidad |
| Operación crítica | Atomicidad/compensación, duplicación/concurrencia y conservación de historial cuando necesario |
| UI | Recorrido afectado, estados, responsive y accesibilidad de controles pertinentes |
| Publicación | Destino/versión y smoke de recorrido real definido en DEPLOYMENT_STANDARD |

Lint/typecheck/build comprueban aspectos estáticos; no demuestran autorizaciones, bridge, DB, archivos ni experiencia completa. Un health endpoint puede demostrar disponibilidad de proceso, no conexión de todos sus servicios.

## Entorno seguro

Identificar destino antes de correr pruebas. Usar datos ficticios y entorno aislado; comprobar comandos que escriben, borran o restauran. No resetear un entorno con datos operativos para preparar tests. No usar secretos/credenciales reales en fixtures ni copiar datos privados a Git.

Cuando no hay entorno local completo, documentar sandbox/ensayo y límites. Una prueba manual es válida si tiene pasos, resultado y evidencia; no llamarla automatizada. Si hace falta respaldo, éste debe ser privado, independiente y restaurable según el riesgo de la operación.

## Resultados

Registrar fecha, commit/base, entorno, comando o pasos, esperado/observado, resultado, omisiones y límites. Resultado: aprobada, fallida, omitida o no ejecutada. Exit code exitoso con tests omitidos no equivale a cobertura del recorrido omitido.

Una prueba con mocks demuestra el contrato simulado, no el servicio real. Un E2E que sólo abre una página no valida persistencia. Una prueba basada en datos previos puede no ser reproducible; registrar dependencia y limpiar fixtures creados, verificando que no se alteró información ajena.

## Qué pruebas escribir y cuándo repetir

Añadir tests cuando protegen un comportamiento relevante o una regresión probable; evitar tests que sólo repiten estructura interna. Para ajustes reversibles de bajo impacto, una comprobación directa/documental puede bastar. Ejecutar checks requeridos por el proyecto y ampliar sólo ante nuevos cambios, fallos o riesgos no resueltos.

Si cambia código después de probar, repetir las comprobaciones afectadas. Registrar fallos y evitar presentarlos como resueltos por inferencia. Los resultados anteriores sólo sirven como antecedente si el cambio invalida su evidencia.

## Criterio de salida

Aceptación demostrada con alcance explícito y fallos relevantes resueltos. Limitaciones pendientes se llevan a TODO/STATE y revisión. No publicar un cambio crítico con comprobaciones requeridas pendientes sin una decisión de riesgo y autorización válidas.