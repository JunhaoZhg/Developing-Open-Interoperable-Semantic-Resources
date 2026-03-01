# Casos de Uso - Recurso Semántico Pokémon

Este documento describe los escenarios de uso que guían el desarrollo de la ontología, identificando a los actores involucrados y el flujo de información necesario para cumplir con los objetivos del sistema.

## Caso de Uso 1: Identificación de Pokémon con alto potencial de combate.
* **Actor:** Entrenador Pokémon
* **Descripción:** El usuario desea identificar qué Pokémon son los mejores "atacantes" y "defensores" para su equipo. Para ello, necesita filtrar los Pokémon que tengan los valores más altos en las estadísticas de HP, Attack, Sp. Atk, Defense, Sp. Defense y Speed, dependiendo del tipo elemental.
* **Flujo de Actividad:** El sistema permite ordenar y filtrar los Pokémon según sus capacidades ofensivas y defensivas y tipo elemental.

## Caso de Uso 2: Planificación de expediciones de captura por región
* **Actor:** Entrenador Pokémon
* **Descripción:** El usuario desea organizar sus viajes de captura optimizando sus recursos (Pokeballs). Para ello, necesita saber qué Pokémon están disponibles en una región específica y conocer la dificultad de captura basándose en su capture_rate.
* **Flujo de Actividad:** El sistema permite filtrar la lista de Pokémon por su región de origen y tipo elemental, mostrando el ratio de captura para que el entrenador decida si la expedición es viable.
