# Estándar de diseño

La metodología exige coherencia y evidencia visual; no impone paleta, tipografía, radios, navegación horizontal/lateral, biblioteca UI ni breakpoints de un producto concreto.

## Antes de modificar UI

Comprender usuarios, tarea, estados y restricciones de acceso. Leer sistema de diseño/identidad existentes e inspeccionar componentes/layouts usados por el flujo. Identificar selector/componente y criterio visual/funcional de aceptación; preservar decisiones aprobadas fuera del alcance.

Si no existe diseño documentado, extraer lo implementado y distinguir inconsistencias de decisiones aceptadas. Una elección visual nueva se propone/valida según alcance; no inventar estilos por pantalla ni copiar la marca del proyecto de referencia.

## Documentar y reutilizar

| Documento del proyecto | Contenido |
| --- | --- |
| DESIGN_SYSTEM.md | Principios, identidad, jerarquía, interacción y accesibilidad |
| TOKENS.md | Valores exactos, origen, nombres semánticos y variantes; implementado separado de propuesto |
| COMPONENTS.md | Componentes/clases disponibles, API/variantes/estados, consumidores y límites |
| LAYOUTS.md si aporta | Estructuras repetidas, restricciones de ancho, overflow y adaptación |

Reutilizar tokens/patrones existentes. Comprobar cascada, especificidad, orden y responsive; una primera coincidencia CSS no prueba el valor final. Si hay valores literales, no afirmar que son tokens implementados. Tokenizar o extraer primitivas sólo con razón/consumidores y comprobación de equivalencia.

No congelar deuda visual como estándar. Overrides acumulados, contrastes insuficientes o controles inconsistentes son hallazgos que se priorizan, no decisiones a replicar.

## Comportamiento de componentes

Definir default, hover, focus, disabled, loading, error, empty, success y selected cuando aplica. Diferenciar ausencia de datos de fallo. Conservar entrada útil ante error; evitar éxito antes de confirmación del sistema. Acciones destructivas y transacciones muestran contexto/consecuencia adecuados al dominio.

Mantener etiquetas, nombres accesibles para iconos, orden de teclado, foco visible, semántica de tablas y modales, lectura de errores y contraste comprobable. Responsive conserva acciones e información esencial y usa overflow cuando resulte adecuado. Probar contenidos reales de longitud representativa con datos ficticios.

La UI refleja acceso; el backend/destino autorizado lo aplica. Exportaciones y detalles privados respetan permisos/alcance, no sólo campos ocultos visualmente.

## Verificación y referencias

Elegir viewports relevantes por contenido y patrones, incluidos límites de transición; no fijar un número universal. Verificar flujo/teclado/foco/modal/scroll y estados afectados. Si se afirma conformidad con una norma de accesibilidad, declarar versión, alcance y evidencia; no certificarla por inspección superficial.

Capturas/referencias tienen fecha, versión, pantalla/flujo, viewport y datos ficticios/anonimizados. No almacenar información privada como material reusable. Sin comprobación en navegador, describir revisión estática y su límite.

Cambios de identidad/patrón se registran en DECISIONS y documentos pertinentes. El diseño reusable es el método para decidir/reutilizar/verificar; los valores pertenecen a cada proyecto.