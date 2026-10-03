# Flujo de Git

Seguir los [niveles de cambio](ENGINEERING_STANDARD.md#niveles-de-cambio) y el [vocabulario de evidencia](ENGINEERING_STANDARD.md#vocabulario-de-evidencia); publicar en Git no equivale a desplegar. Git mantiene trazabilidad del trabajo; el remoto ofrece una copia compartida de commits. No respalda por sí solo DB, archivos operativos, secretos o servicios externos.

## Antes de editar

Comprobar repositorio, rama, remoto, HEAD, estado y commits relevantes. Registrar modificaciones preexistentes; no hacer reset, restore, clean, stash o checkout que las descarte sin autorización. Si se necesita aislamiento, usar rama/checkout/worktree adecuado a la política local.

Cada proyecto declara convención de ramas y modelo de integración. Una rama por objetivo es recomendada; el prefijo no forma parte del núcleo universal. No imponer main, una estrategia de PR o commits convencionales si el proyecto tiene otra política aceptada.

## Commit por unidad revisable

1. Revisar diff completo de la entrega y rutas modificadas.
2. Verificar formato, ausencia de secretos/datos privados y archivos generados accidentalmente.
3. Añadir rutas explícitas cuando el árbol tiene trabajo mixto.
4. Crear commit descriptivo del problema/resultado; enlazar ID de tarea cuando existe.
5. Comprobar el commit y cambios que permanecen fuera.

Separar unidades funcionales; no fragmentar artificialmente archivos que sólo funcionan juntos ni mezclar refactor no relacionado. Documentación requerida acompaña al cambio. No hacer commit vacío de “pruebas aprobadas” ni usar el mensaje como sustituto de evidencia.

## Push y verificación

Identificar remoto y rama exactos. Comprobar automatizaciones que dispara el push: previews, publicación, migraciones o jobs. Push no autoriza por sí solo merge ni despliegue; si publicar la rama activa un destino operativo, aplicar [DEPLOYMENT_STANDARD.md](DEPLOYMENT_STANDARD.md) antes de ejecutarlo.

Hacer push cuando corresponde según política/alcance; no dejar trabajo importante únicamente en local y publicarlo en el destino autorizado. Un cambio trivial puede integrarse en la siguiente unidad revisable prevista, con estado explícito y sin crear commits o documentos artificiales. Si se bloquea por acceso/red/política, conservar commits y registrar pendiente, error resumido y siguiente acción; no declarar respaldo remoto.

Ejemplo de comprobación, ajustando nombres reales del proyecto:

```bash
git status --short
git log -1 --oneline
git rev-parse HEAD
git ls-remote <remoto> refs/heads/<rama>
```

Una respuesta vacía de ls-remote no demuestra coincidencia. Comparar SHA completo con la referencia esperada; si no coincide, investigar sin forzar sobrescritura. Registrar momento/destino/resultado. No insertar credenciales en URLs o logs.

## Integración

Seguir revisión/checks y política de ramas protegidas. Resolver conflictos comprendiendo ambas intenciones y repetir verificaciones afectadas. No usar force push ni reescribir trabajo compartido sin autorización. Un PR debe explicar problema, comportamiento final, validación y límites; no transcribir el chat.

## Estados independientes al cerrar

Registrar working tree limpio/sucio y causa; archivos de entrega sin commit; commits locales sin push; SHA local/remoto; revisión/merge pendientes; despliegue y comprobación de Producción por separado. Árbol sucio por trabajo ajeno no significa que la entrega carezca de commit; árbol limpio no prueba push.

[SESSION_HANDOFF.md](SESSION_HANDOFF.md) contiene el formato de cierre, evitando duplicar el procedimiento aquí.