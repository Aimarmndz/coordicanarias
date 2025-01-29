
# Pautas de Accesibilidad de Contenido Web 2.0 (WCAG)

Las **WCAG 2.0** son un conjunto de pautas organizadas en **cuatro principios fundamentales (POUR)** para garantizar que el contenido web sea accesible para personas con diversas capacidades.
> **Nota:** (POUR) = P - Perceptible, O - Operable, U - Comprensible (Understandable), R - Robusto
---

## Principio 1: Perceptible
La información debe presentarse de manera que los usuarios puedan percibirla.

### Pauta 1.1: Alternativas Textuales
- **1.1.1 Contenido no textual (Nivel A)**: Proporcionar alternativas textuales para todo contenido no textual, excepto:
  - Controles o entrada de datos.
  - Contenido multimedia dependiente del tiempo.
  - Pruebas o ejercicios.
  - Experiencias sensoriales específicas.
  - CAPTCHA con alternativas.
  - Contenido decorativo o invisible.

### Pauta 1.2: Contenido Multimedia Dependiente del Tiempo
- **1.2.1 Solo audio y solo vídeo (pregrabado) (Nivel A)**: Alternativas equivalentes para contenido de solo audio o vídeo.
- **1.2.2 Subtítulos (pregrabado) (Nivel A)**: Subtítulos sincronizados para contenido multimedia.
- **1.2.3 Audiodescripción (Nivel A)**: Proveer audiodescripción o alternativa multimedia.
- **1.2.4 Subtítulos (directo) (Nivel AA)**: Subtítulos para contenido en vivo.
- **1.2.5 Audiodescripción (pregrabado) (Nivel AA)**: Audiodescripción para vídeos pregrabados.
- **1.2.6 Lengua de signos (pregrabada) (Nivel AAA)**: Proveer interpretación en lengua de signos.
- **1.2.7 Audiodescripción extendida (Nivel AAA)**: Proveer audiodescripción extendida cuando sea necesario.
- **1.2.8 Alternativa multimedia (Nivel AAA)**: Alternativas para todo contenido multimedia.
- **1.2.9 Solo audio (directo) (Nivel AAA)**: Alternativa para contenido de solo audio en directo.

### Pauta 1.3: Adaptabilidad
- **1.3.1 Información y relaciones (Nivel A)**: Estructura y relaciones deben ser programáticamente determinables.
- **1.3.2 Secuencia significativa (Nivel A)**: Mantener una secuencia lógica.
- **1.3.3 Características sensoriales (Nivel A)**: No depender únicamente de características sensoriales como color o tamaño.

### Pauta 1.4: Distinguible
- **1.4.1 Uso del color (Nivel A)**: No usar el color como único medio para transmitir información.
- **1.4.2 Control de audio (Nivel A)**: Proveer controles para pausar o detener audio reproducido automáticamente.
- **1.4.3 Contraste mínimo (Nivel AA)**: Relación mínima de 4.5:1 para texto y fondo.
- **1.4.4 Variar tamaño de texto (Nivel AA)**: Permitir ajustar tamaño de texto hasta un 200 % sin pérdida de contenido.
- **1.4.5 Imágenes de texto (Nivel AA)**: Usar texto en lugar de imágenes, salvo en logotipos.
- **1.4.6 Contraste mejorado (Nivel AAA)**: Relación mínima de contraste 7:1.
- **1.4.7 Fondo de audio bajo o inexistente (Nivel AAA)**: Reducir fondo de audio en grabaciones.
- **1.4.8 Presentación visual (Nivel AAA)**: Ofrecer opciones de personalización para texto y colores.
- **1.4.9 Imágenes de texto sin excepción (Nivel AAA)**: Limitar imágenes de texto solo a casos esenciales.

---

## Principio 2: Operable
Los componentes y la navegación deben ser funcionales para todos los usuarios.

### Pauta 2.1: Accesible a través del teclado
- **2.1.1 Teclado (Nivel A)**: Toda funcionalidad debe ser operable mediante teclado.
- **2.1.2 Sin trampa de teclado (Nivel A)**: Asegurar que el usuario puede salir de cualquier componente.
- **2.1.3 Teclado sin excepción (Nivel AAA)**: Funcionalidad accesible sin excepciones.

### Pauta 2.2: Tiempo suficiente
- **2.2.1 Límite de tiempo ajustable (Nivel A)**: Permitir ajustar, desactivar o extender límites de tiempo.
- **2.2.2 Pausar, detener, ocultar (Nivel A)**: Proveer controles para detener o pausar contenido en movimiento.
- **2.2.3 Sin tiempo (Nivel AAA)**: Eliminar dependencias de tiempo en el contenido.
- **2.2.4 Interrupciones (Nivel AAA)**: Permitir posponer o eliminar interrupciones.
- **2.2.5 Reautentificación (Nivel AAA)**: Permitir reanudar actividades tras expirar una sesión.

### Pauta 2.3: Ataques
- **2.3.1 Tres destellos o por debajo del umbral (Nivel A)**: Evitar contenido que destelle más de tres veces por segundo.
- **2.3.2 Tres destellos (Nivel AAA)**: Prohibir destellos en todo contenido.

### Pauta 2.4: Navegabilidad
- **2.4.1 Saltar bloques (Nivel A)**: Proveer un mecanismo para saltar bloques repetidos.
- **2.4.2 Página titulada (Nivel A)**: Las páginas deben tener títulos claros.
- **2.4.3 Orden de foco (Nivel A)**: El orden de navegación debe preservar la lógica y funcionalidad.
- **2.4.4 Propósito de un vínculo (Nivel A)**: El propósito del vínculo debe ser claro.
- **2.4.5 Múltiples medios (Nivel AA)**: Proveer más de un medio para localizar contenido.
- **2.4.6 Encabezados y etiquetas (Nivel AA)**: Usar encabezados descriptivos y etiquetas claras.
- **2.4.7 Foco visible (Nivel AA)**: Proveer un indicador visible para el foco del teclado.
- **2.4.8 Ubicación (Nivel AAA)**: Incluir información de orientación.
- **2.4.9 Propósito del vínculo solo (Nivel AAA)**: Asegurar que el texto del vínculo sea suficiente para describirlo.
- **2.4.10 Encabezados de sección (Nivel AAA)**: Usar encabezados para organizar contenido.

---

## Principio 3: Comprensible
El contenido debe ser fácil de entender.

### Pauta 3.1: Legible
- **3.1.1 Idioma de la página (Nivel A)**: El idioma debe poder determinarse programáticamente.
- **3.1.2 Idioma de partes (Nivel AA)**: El idioma de cada pasaje debe indicarse.
- **3.1.3 Palabras inusuales (Nivel AAA)**: Proveer definiciones para palabras inusuales.
- **3.1.4 Abreviaturas (Nivel AAA)**: Explicar las abreviaturas utilizadas.
- **3.1.5 Nivel de lectura (Nivel AAA)**: Ofrecer versiones simplificadas de contenido complejo.
- **3.1.6 Pronunciación (Nivel AAA)**: Indicar pronunciación cuando sea necesario.

### Pauta 3.2: Predecible
- **3.2.1 Con foco (Nivel A)**: Recibir el foco no debe provocar cambios inesperados.
- **3.2.2 Con entrada de datos (Nivel A)**: Cambiar configuraciones no debe alterar el contexto sin advertencia.
- **3.2.3 Navegación consistente (Nivel AA)**: Mantener consistencia en mecanismos de navegación.
- **3.2.4 Identificación consistente (Nivel AA)**: Usar identificadores consistentes para elementos similares.
- **3.2.5 Cambio a petición (Nivel AAA)**: Cambios en el contexto deben activarse solo por el usuario.

### Pauta 3.3: Ayuda a la entrada de datos
- **3.3.1 Identificación de errores (Nivel A)**: Identificar y describir errores de entrada.
- **3.3.2 Etiquetas o instrucciones (Nivel A)**: Proveer etiquetas claras para entrada de datos.
- **3.3.3 Sugerencia tras error (Nivel AA)**: Proveer sugerencias para corregir errores.
- **3.3.4 Prevención de errores (Nivel AA)**: Prevenir errores en tareas importantes.
- **3.3.5 Ayuda contextual (Nivel AAA)**: Proveer ayuda específica en el contexto.
- **3.3.6 Prevención de todos los errores (Nivel AAA)**: Diseñar para minimizar errores.

---

## Principio 4: Robusto
El contenido debe ser lo suficientemente robusto para ser interpretado por tecnologías actuales y futuras.

### Pauta 4.1: Compatible
- **4.1.1 Interpretación (Nivel A)**: El contenido debe tener una estructura válida y única.
- **4.1.2 Nombre, rol, valor (Nivel A)**: Los componentes de interfaz deben exponer nombre, rol y estado.

---

## Niveles de Conformidad
- **Nivel A**: Requisitos básicos.
- **Nivel AA**: Accesibilidad avanzada.
- **Nivel AAA**: Máxima accesibilidad.

## Recursos Adicionales
- [WCAG 2.0 en W3C](https://www.w3.org/TR/WCAG20/)
