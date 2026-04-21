# Justificación de Descarte de Campos de Datos

Este documento detalla los campos de los datasets originales y extendidos que han sido excluidos del proceso de especificación de requisitos por no alinearse con el alcance de los casos de uso definidos.

## Campos descartados de pokemon.csv (Dataset central)

* ## Data Field: id
 **Descripción:** Se descarta el identificador numérico interno ya que la identificación de especímenes se realiza mediante la columna "Form".

* ## Data Field: Index
 **Descripción:** Se descarta el índice por la misma razón que id; se usa "Form" como identificador.

* ## Data Field: Name
 **Descripción:** Se descarta la columna de Name, ya que usamos la columna "Form" que es mas especifico (un mismo pokemon puede tener diferentes formas y estadisticas diferentes).

## Campos descartados de DataSet2.csv

* ## Data Field: National
 **Descripción:** Se descarta el número de índice nacional ya que la identificación de especímenes se realiza mediante el nombre y la región en el Caso de Uso 2.

* ## Data Field: Male_Pct
 **Descripción:** Columna irrelevante para nuestras consultas, ya que no se han definido requisitos relacionados con la crianza o el dimorfismo sexual de los Pokémon.

* ## Data Field: Female_Pct
 **Descripción:** Columna irrelevante para nuestras consultas, ya que no se han definido requisitos relacionados con la crianza o el dimorfismo sexual de los Pokémon.

* ## Data Field: Types
 **Descripción:** Se descarta esta columna combinada en favor de las columnas específicas `type1` y `type2` para permitir filtros elementales más precisos en los requisitos funcionales.

* ## Data Field: Heigh
 **Descripción:** Se descarta la altura del espécimen al no tener impacto en las estadísticas de combate (Caso de Uso 1) ni en la logística de captura (Caso de Uso 2).

* ## Data Field: Weigh
 **Descripción:** Se descarta el peso del espécimen al no tener impacto en las estadísticas de combate (Caso de Uso 1) ni en la logística de captura (Caso de Uso 2).

* ## Data Field: Egg Steps
 **Descripción:** Columna irrelevante para nuestras consultas; la ontología no modela la eclosión de huevos ni mecánicas de crianza.

* ## Data Field: Exp_Points
 **Descripción:** Se descarta la experiencia base ya que el sistema se centra en las estadísticas base y no en la progresión de niveles del entrenador.

* ## Data Field: Base_Happiness
 **Descripción:** Descartamos esta columna por ser irrelevante para el cálculo del potencial ofensivo y no influir en el ratio de captura del Caso de Uso 2.

* ## Data Field: Normal_Dmg - Fairy_Dmg
 **Descripción:** Se descarta el bloque completo de multiplicadores de daño externo para simplificar el modelo, centrándose solo en las capacidades intrínsecas del Pokémon.

* ## Data Field: Mega Evolutions
 **Descripción:** Se descartan las mecánicas de megaevolución para mantener el enfoque en las formas base y la consistencia de los datos regionales.

* ## Data Field: isMega
 **Descripción:** Se descarta este indicador booleano al no incluirse formas Mega en los requisitos de filtrado de la ontología.

* ## Data Field: hasAlolan
 **Descripción:** Se descarta la información sobre variantes regionales de Alola para priorizar las formas estándar de cada generación según el Caso de Uso 2.

* ## Data Field: isAlolan
 **Descripción:** Se descarta la información sobre variantes regionales de Alola para priorizar las formas estándar de cada generación según el Caso de Uso 2.

* ## Data Field: Legendary
 **Descripción:** Se descarta esta clasificación para mantener la coherencia con los filtros de tipo elemental, región y ratio de captura sin añadir excepciones por rareza.

## Campos descartados de pokemon_species.csv (PokeAPI)

* ## Data Field: generation_id
 **Descripción:** Se descarta porque la generación ya se obtiene de DataSet2.csv (columna Generation).

* ## Data Field: evolves_from_species_id
 **Descripción:** Se descarta la cadena evolutiva al estar fuera del alcance de los casos de uso de combate y captura.

* ## Data Field: evolution_chain_id
 **Descripción:** Se descarta por la misma razón que evolves_from_species_id.

* ## Data Field: gender_rate
 **Descripción:** Se descarta al no haberse definido requisitos relacionados con el género del Pokémon.

* ## Data Field: capture_rate
 **Descripción:** Se descarta porque el ratio de captura ya se obtiene de DataSet2.csv (columna Capt_Rate).

* ## Data Field: base_happiness
 **Descripción:** Irrelevante para los casos de uso de combate y captura.

* ## Data Field: is_baby
 **Descripción:** Se descarta al no modelar las pre-evoluciones como categoría diferenciada en la ontología.

* ## Data Field: hatch_counter
 **Descripción:** Irrelevante; la ontología no modela mecánicas de crianza ni eclosión de huevos.

* ## Data Field: has_gender_differences
 **Descripción:** Se descarta al no haberse definido requisitos relacionados con el dimorfismo sexual.

* ## Data Field: growth_rate_id
 **Descripción:** Se descarta porque la curva de experiencia ya se obtiene de DataSet2.csv (columna Exp_Speed).

* ## Data Field: forms_switchable
 **Descripción:** Se descarta al no modelar el cambio de formas en la ontología.

* ## Data Field: is_legendary
 **Descripción:** Se descarta por la misma razón que el campo Legendary de DataSet2.csv.

* ## Data Field: is_mythical
 **Descripción:** Se descarta por la misma razón que Legendary; no se diferencia por rareza.

* ## Data Field: order
 **Descripción:** Campo de ordenación interna sin valor semántico para la ontología.

* ## Data Field: conquest_order
 **Descripción:** Campo específico del spin-off Pokémon Conquest, fuera del alcance de la ontología.

## Campos descartados de pokemon_abilities.csv (PokeAPI)

* ## Data Field: slot
 **Descripción:** Se descarta el orden del slot de habilidad al no ser relevante para los casos de uso; solo se modela qué habilidades tiene un Pokémon.

## Campos reincorporados (anteriormente descartados)

Los siguientes campos estaban descartados en versiones anteriores de este documento pero han sido reincorporados para generar clases adicionales en la ontología:

* ## Data Field: Egg Groups / Group 1 / Group 2
 **Motivo de reincorporación:** Se usan para generar la clase **EggGroup** y la relación `perteneceAEggGroup`.

* ## Data Field: Exp_Speed
 **Motivo de reincorporación:** Se usa para generar la clase **CurvaDeExperiencia** y la relación `tieneCurvaExperiencia`.
