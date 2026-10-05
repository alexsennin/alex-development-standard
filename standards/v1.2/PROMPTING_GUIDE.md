# Cómo pedir trabajo de vibecoding

Un pedido útil indica **qué resultado quieres ver** y **dónde debe quedar**. El agente debe inferir los comandos y controles técnicos; la persona usuaria no necesita escribir PATCH, CHECK o RELEASE ni enumerar cada prueba.

## Cinco datos que evitan vueltas

1. **Proyecto y destino:** nombre/repositorio y Local, Preview o Producción.
2. **Resultado observable:** pantalla, flujo o dato que debe cambiar; ejemplo concreto si hay un error.
3. **Límite:** qué texto, diseño, datos o módulo se debe conservar; qué queda fuera.
4. **Criterio de aceptación:** cómo reconocer que quedó bien. Una captura, error reproducible o ejemplo antes/después ayuda.
5. **Acción al terminar:** dejar listo para que lo pruebes, consolidar una ronda o publicar en un destino concreto.

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

### Publicar una entrega sencilla

```text
Publica en Producción los cambios de [rama/PR o funciones concretas] de
[proyecto]. Si sólo cambian archivos de la aplicación y cumple la ruta rápida,
usa el despliegue habitual, verifica [pantalla/flujo] y dime qué quedó activo.
Si detectas migraciones, cambios en datos, permisos o servicios aparte,
aplica los controles pertinentes a esas capas y reporta el resultado.
```

«Publica» o «aplica en Producción» ya expresa autorización para esa entrega y destino. Una petición de «revisa», «prepara» o «diseña el plan» pide un resultado revisable, no un despliegue. Si el usuario delimita otra autorización, prevalece su alcance literal.

## Respuesta esperada del agente

Para una corrección: **qué cambió, prueba focal, dónde probar, pendiente real**. Para una publicación sencilla: **destino, revisión disponible, flujo comprobado y límite concreto**. Para datos o cambios estructurales: añadir compatibilidad, recuperación y verificaciones pertinentes. Evitar listas de SHA, versiones de funciones, migraciones y servicios ajenos a la entrega.
