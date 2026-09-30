# Adopción de ALEX DEVELOPMENT STANDARD v1

Procedimiento para aplicar la metodología en un repositorio existente o nuevo. La metodología v1.0 está aprobada para piloto; el piloto aún no se ha iniciado. Este documento prepara la adopción; no autoriza modificar otros repositorios ni instalar herramientas/skills.

## Etapas

1. **Inventario:** identificar propósito, stack, estructura, estado Git, fuentes operativas, entornos y reglas existentes. Leer documentación vigente antes de crear nada.
2. **Brechas:** clasificar hechos, propuestas, deuda y documentación obsoleta; ubicar equivalentes a los seis documentos mínimos y reglas de diseño cuando aplican.
3. **Plan de adopción:** definir alcance, archivos, criterios de aceptación, dependencias y política de publicación del proyecto. Conservar instrucciones válidas y generadas.
4. **Contexto mínimo:** completar los documentos con datos propios. Usar responsabilidades de PROJECT_DOCUMENTATION, no copiar contenido del ejemplo.
5. **Adaptación técnica:** registrar comandos comprobados, pruebas, entornos y despliegue según stack; no inventar integraciones.
6. **Piloto:** ejecutar una tarea pequeña autorizada de extremo a extremo, clasificada por nivel de cambio, con revisión y handoff proporcional.
7. **Revisión:** comprobar que otro agente puede recuperar contexto, verificar resultado y continuar; corregir fricciones sin imponer refactor innecesario.
8. **Declaración:** registrar versión adoptada, excepciones y fecha/responsable. Sólo entonces considerar adoptado el estándar.

## Separación de capas

Núcleo universal: principios, contexto, tareas, decisiones, pruebas, Git, autorización/publicación y handoff proporcional. Adaptación tecnológica: runtime/framework, comandos, contratos, migraciones y herramientas concretas. Adaptación de producto: usuarios, dominio, datos, idiomas/moneda/zona, identidad y comportamiento.

Una adaptación para web, automatización de hojas o servicios de datos puede elegir herramientas distintas. Ninguna requiere Next, Apps Script, Supabase, Vercel ni un layout específico para cumplir el núcleo. Cuando no exista ejecución local completa, documentar sandbox autorizado y evidencia real.

## Preservación e independencia

Integrar con AGENTS/instrucciones existentes sin eliminarlas. Si el proyecto utiliza otra ubicación documental, mapear explícitamente cada responsabilidad y ofrecer los seis puntos de entrada para recuperación; no duplicar archivos que competirán como autoridad.

Elegir cómo distribuir/versionar el paquete (copia versionada, enlace, repo común u otro mecanismo) mediante decisión posterior. Registrar versión de origen para evitar actualizaciones silenciosas. No sincronizar automáticamente todos los consumidores ni trasladar IDs, URLs operativas, cuentas, datos o marca del proyecto de referencia.

## Aceptación de adopción

- Los seis documentos describen hechos propios y tienen responsabilidades claras.
- STATE refleja presente, TODO criterios verificables y DECISIONS razones duraderas.
- Actual/objetivo y probado/publicado están separados.
- Herramientas/comandos/destinos se comprobaron; secretos y datos privados quedaron fuera.
- Una tarea piloto cumple aceptación y cierre, incluyendo estado Git/remoto/Producción explícitos.
- Otro agente puede determinar siguiente paso sin leer el chat.
- Excepciones y deuda no se presentan como cumplimiento total.

Para un proyecto nuevo sin funcionalidades, documentar “sin implementación” y verificar lo que existe; no inventar pruebas ni un despliegue para llenar el checklist.

## Siguiente paso para el piloto

Alex debe elegir el proyecto/tarea piloto y autorizar su alcance. La aprobación para piloto no autoriza todavía migrar otros repositorios. La creación de una base central o skill es una tarea posterior con su alcance propio; esta entrega no migra proyectos ni cambia funcionalidades.