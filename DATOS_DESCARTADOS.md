# Justificación de Descarte de Campos de Datos

Este documento detalla los campos de los datasets originales y extendidos que han sido excluidos del proceso de especificación de requisitos por no alinearse con el alcance de los casos de uso definidos.

* ## Data Field: National
* **Descripción:** Se descarta el número de índice nacional ya que la identificación de especímenes se realiza mediante el nombre y la región en el Caso de Uso 2.

* ## Data Field: Male_Pct
* **Descripción:** Columna irrelevante para nuestras consultas, ya que no se han definido requisitos relacionados con la crianza o el dimorfismo sexual de los Pokémon.

* ## Data Field: Female_Pct
* **Descripción:** Columna irrelevante para nuestras consultas, ya que no se han definido requisitos relacionados con la crianza o el dimorfismo sexual de los Pokémon.

* ## Data Field: Types
* **Descripción:** Se descarta esta columna combinada en favor de las columnas específicas `type1` y `type2` para permitir filtros elementales más precisos en los requisitos funcionales.

* ## Data Field: Heigh
* **Descripción:** Se descarta la altura del espécimen al no tener impacto en las estadísticas de combate (Caso de Uso 1) ni en la logística de captura (Caso de Uso 2).

* ## Data Field: Weigh
* **Descripción:** Se descarta el peso del espécimen al no tener impacto en las estadísticas de combate (Caso de Uso 1) ni en la logística de captura (Caso de Uso 2).

* ## Data Field: Egg Steps
* **Descripción:** Columna irrelevante para nuestras consultas; la ontología no modela la eclosión de huevos ni mecánicas de crianza.

* ## Data Field: Egg Groups
* **Descripción:** Columna irrelevante para nuestras consultas; la ontología no modela la eclosión de huevos ni mecánicas de crianza.

* ## Data Field: Group 1
* **Descripción:** Se descarta este campo de agrupación adicional por no estar vinculado a ninguna de las preguntas de competencia de captura o combate.

* ## Data Field: Group 2
* **Descripción:** Se descarta este campo de agrupación adicional por no estar vinculado a ninguna de las preguntas de competencia de captura o combate.

* ## Data Field: Exp_Points
* **Descripción:** Se descarta la experiencia base ya que el sistema se centra en las estadísticas base y no en la progresión de niveles del entrenador.

* ## Data Field: Exp_Speed
* **Descripción:** Se descarta la curva de crecimiento al estar fuera del alcance de los filtros de combate y captura definidos.

* ## Data Field: Base_Happiness
* **Descripción:** Descartamos esta columna por ser irrelevante para el cálculo del potencial ofensivo y no influir en el ratio de captura del Caso de Uso 2.

* ## Data Field: Normal_Dmg - Fairy_Dmg
* **Descripción:** Se descarta el bloque completo de multiplicadores de daño externo para simplificar el modelo, centrándose solo en las capacidades intrínsecas del Pokémon.

* ## Data Field: Mega Evolutions
* **Descripción:** Se descartan las mecánicas de megaevolución para mantener el enfoque en las formas base y la consistencia de los datos regionales.

* ## Data Field: isMega
* **Descripción:** Se descarta este indicador booleano al no incluirse formas Mega en los requisitos de filtrado de la ontología.

* ## Data Field: hasAlolan
* **Descripción:** Se descarta la información sobre variantes regionales de Alola para priorizar las formas estándar de cada generación según el Caso de Uso 2.

* ## Data Field: isAlolan
* **Descripción:** Se descarta la información sobre variantes regionales de Alola para priorizar las formas estándar de cada generación según el Caso de Uso 2.

* ## Data Field: Legendary
* **Descripción:** Se descarta esta clasificación para mantener la coherencia con los filtros de tipo elemental, región y ratio de captura sin añadir excepciones por rareza.
