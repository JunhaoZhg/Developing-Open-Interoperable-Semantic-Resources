# Casos de Uso - Recurso Semántico Pokémon

Este documento describe los escenarios de uso que guían el desarrollo de la ontología, identificando a los actores involucrados y el flujo de información necesario para cumplir con los objetivos del sistema.

Nota: Sp significa "Special", usado con "Attack" o "Defense", por ejemplo, "Sp Attack" (special attack) o "Sp defense" (special defense). 
Hp significa "Health / Hit Points" (puntos de vida) 

## Caso de Uso 1: Identificación de Pokémon con alto potencial de combate.
* **Actor:** Entrenador Pokémon
* **Descripción:** El usuario desea identificar qué Pokémon son los mejores "atacantes" y "defensores" para su equipo. Para ello, necesita filtrar los Pokémon que tengan los valores más altos en las estadísticas de HP, Attack, Sp. Atk, Defense, Sp. Defense y Speed, dependiendo del tipo elemental.
* **Flujo de Actividad:** El sistema permite ordenar y filtrar los Pokémon según sus capacidades ofensivas y defensivas y tipo elemental.

## Caso de Uso 2: Planificación de expediciones de captura por región
* **Actor:** Entrenador Pokémon
* **Descripción:** El usuario desea organizar sus viajes de captura optimizando sus recursos (Pokeballs). Para ello, necesita saber qué Pokémon están disponibles en una región específica y conocer la dificultad de captura basándose en su capture_rate.
* **Flujo de Actividad:** El sistema permite filtrar la lista de Pokémon por su región de origen y tipo elemental, mostrando el ratio de captura para que el entrenador decida si la expedición es viable.

## Caso de Uso 3: Búsqueda de Pokémon por características físicas
* **Actor:** Entrenador Pokémon
* **Descripción:** El usuario desea buscar Pokémon filtrando por su color predominante y su forma corporal, por ejemplo para completar colecciones temáticas o identificar Pokémon visualmente similares.
* **Flujo de Actividad:** El sistema permite filtrar Pokémon por color y forma corporal, mostrando los que coincidan con los criterios seleccionados.

## Caso de Uso 4: Planificación de crianza
* **Actor:** Entrenador Pokémon
* **Descripción:** El usuario desea saber qué Pokémon son compatibles para la crianza y cuánta experiencia necesitan para alcanzar su nivel máximo, para optimizar su tiempo de entrenamiento.
* **Flujo de Actividad:** El sistema permite filtrar Pokémon por grupo de huevo para identificar compatibilidades de crianza, y consultar su curva de experiencia para estimar el esfuerzo de entrenamiento.

## Caso de Uso 5: Exploración por hábitat y habilidad
* **Actor:** Entrenador Pokémon
* **Descripción:** El usuario desea planificar expediciones a un tipo de entorno específico (cueva, bosque, mar, etc.) y seleccionar Pokémon con habilidades útiles para ese entorno.
* **Flujo de Actividad:** El sistema permite filtrar Pokémon por hábitat y consultar sus habilidades, para que el entrenador pueda preparar su equipo según el terreno de exploración.
