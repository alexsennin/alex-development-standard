# Cómo pedir trabajo de vibecoding

Un pedido útil indica **qué resultado quieres ver** y **dónde debe quedar**. El agente debe inferir los comandos y controles técnicos; la persona usuaria no necesita escribir PATCH, CHECK o RELEASE ni enumerar cada prueba.

## Cinco datos que evitan vueltas

1. **Proyecto y destino:** nombre/repositorio y Local, Preview o Producción.
2. **Resultado observable:** pantalla, flujo o dato que debe cambiar; ejemplo concreto si hay un error.
3. **Límite:** qué texto, diseño, datos o módulo se debe conservar; qué queda fuera.
4. **Criterio de aceptación:** cómo reconocer que quedó bien. Una captura, error reproducible o ejemplo antes/después ayuda.
5. **Acción al terminar:** dejar listo para prueba, consolidar una ronda, publicar en Git/artefactos o desplegar en un entorno explícito.

Cuando uno de estos datos falta, el agente debe comprobar lo inferible en el proyecto y preguntar sólo por lo que bloquea una decisión material. No pedir al usuario que describa arquitectura, versionado o comandos que el repositorio ya documenta.

## Pedidos copiables

### Corregir mientras pruebo Local

```text
En [proyecto], en Local, corrige [error o comportamiento] en [pantalla/flujo].
Para reproducirlo: [pasos o captura]. Debe quedar [resultado observable].
Conserva [texto/diseño/regla que no debe cambiar]. Corrige lo necesario,
prueba el flujo afectado y dime cómo volver a probarlo. Acumula las
correcciones de esta ronda; te diré «cierra la ronda» cuando termine de probar.
```

Durante la ronda se usa verificación focal. Al recibir «cierra la ronda», revisar el conjunto, ejecutar pruebas acumuladas pertinentes y respaldar/publicar el código según la política del proyecto. No repetir esa consolidación después de cada detalle.

### Función nueva o cambio de datos

```text
En [proyecto], necesito [flujo nuevo] para [usuario].
Entrada: [datos y fuente]. Resultado esperado: [ejemplo].
Reglas: [permisos, duplicados, cálculos y límites conocidos].
Trabaja primero en [Local/entorno aislado]. Entrégame el flujo usable y
separa lo que requiera migración, datos reales o Producción.
```

Para importaciones, indicar archivo/fuente, identificador confiable de cada fila, interpretación de valores ambiguos, tratamiento de duplicados y destino. Si faltan horas, identidades o reglas que cambian el resultado, resolverlas antes de escribir datos reales.

### Desplegar una entrega sencilla

```text
Despliega en Producción los cambios de [rama/PR o funciones concretas] de
[proyecto]. Si sólo cambian archivos de la aplicación y cumple la ruta rápida,
usa el despliegue habitual, verifica [pantalla/flujo] y dime qué quedó activo.
Si detectas migraciones, cambios en datos, permisos o servicios aparte,
aplica los controles pertinentes a esas capas y reporta el resultado.
```

**«Publica» nunca autoriza Producción.** «Publica», «haz push» o «sube la rama» se interpretan como Git/artefactos. Producción requiere una instrucción explícita como «despliega en Producción» o «aplica en Producción». Una petición de «revisa», «prepara» o «diseña el plan» pide un resultado revisable, no un despliegue. Si el usuario delimita otra autorización, prevalece su alcance literal.

## Autonomía por fases

En trabajo complejo, el usuario no necesita elegir modelos ni redactar microtareas. El agente/orquestador propone fases, criterios y asignación de capacidad. El usuario puede decir, por ejemplo, «ejecuta sólo la fase 1», «ejecuta fases 1 a 3» o «ejecuta todo el plan». Esa instrucción autoriza la ejecución interna de esas fases dentro de los límites existentes, pero no convierte SYSTEM en RELEASE ni autoriza operaciones externas no incluidas.

Si el runtime no puede cambiar modelos automáticamente, el mismo plan se usa en modo de compatibilidad manual: se indica el cambio de modelo/razonamiento sólo en los puntos donde realmente sea necesario, sin convertir al usuario en gestor de cada microtarea.

## Respuesta esperada del agente

Para una corrección: **qué cambió, prueba focal, dónde probar, pendiente real**. Para una publicación Git/artefacto: **destino, revisión disponible y límite concreto**. Para un despliegue: **entorno, revisión activa, flujo comprobado y límite concreto**. Para datos o cambios estructurales: añadir compatibilidad, recuperación y verificaciones pertinentes. Evitar listas de SHA, versiones de funciones, migraciones y servicios ajenos a la entrega.
