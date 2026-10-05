# Informe de aprobación v1.2

Fecha: 2026-10-05. Estado: **vigente y recomendada para adopción gradual**, por decisión de Alex. No se adopta automáticamente en proyectos consumidores; v1.1 permanece como referencia histórica.

## Motivo

Las correcciones iterativas ya tenían una ruta ligera en v1.1, pero el protocolo de RELEASE seguía describiendo un preflight general. En los proyectos revisados, esto mezcló publicaciones de sólo código con conciliación de migraciones y versiones de funciones. También hubo solicitudes donde el trabajo de validación desplazó la prioridad de tener un MVP local usable.

## Cambios incorporados

- Ruta rápida de Producción para cambios reversibles sólo de archivos de aplicación, con revisión del diff, prueba pertinente, destino conocido, identificador automático y comprobación del flujo afectado.
- Ruta ampliada únicamente para las capas implicadas en datos, contratos, permisos, configuración o servicios independientes.
- Sin números manuales de versión, etiquetas, changelog, `RELEASE_STATE.md`, respaldo de DB ni revisión de historial de migraciones en la ruta rápida.
- Guía breve para pedir correcciones locales, consolidar rondas y autorizar una publicación con alcance claro.
- Agente opcional de conciliación semanal en solo lectura, con línea base y avisos únicamente ante diferencias relevantes.
- Cierre documental sólo cuando cambió la verdad de un documento.

## Compatibilidad y límites

La v1.2 conserva el resto de v1.1 como paquete completo. No altera v1.0 ni v1.1. Se integraron al protocolo central las reglas generales de migraciones y publicación por capas de la v1.2 escrita dentro de MonduColores; sus comandos y límites propios permanecen en ese proyecto. La aprobación central no modifica ni declara adoptado automáticamente a MonduColores u otros productos, y no ejecuta despliegues de aplicaciones.
