## Clases de la Ontología

La ontología se compone de 10 clases. El dataset central es `pokemon.csv` y se complementa con `DataSet2.csv` y varios archivos de [PokeAPI](https://github.com/PokeAPI/pokeapi/tree/master/data/v2/csv).

### 1. Pokémon
- **Descripción:** Cada espécimen individual con sus estadísticas base.
- **Origen:** `pokemon.csv` (dataset central)
- **Ejemplos de instancias:** Bulbasaur, Charmander, Pikachu

### 2. Tipo
- **Descripción:** Tipo elemental de un Pokémon. Existen 18 tipos distintos.
- **Origen:** `pokemon.csv` (columnas Type1, Type2)
- **Ejemplos de instancias:** Fire, Water, Grass, Electric, Dragon

### 3. Región
- **Descripción:** Región geográfica del mundo Pokémon donde se puede encontrar un Pokémon.
- **Origen:** `DataSet2.csv` (columna Region)
- **Enlace con dataset central:** por Name/Form
- **Ejemplos de instancias:** Kanto, Johto, Hoenn, Sinnoh, Unova, Kalos, Alola

### 4. Generación
- **Descripción:** Generación del videojuego en la que fue introducido el Pokémon.
- **Origen:** `DataSet2.csv` (columna Generation)
- **Enlace con dataset central:** por Name/Form
- **Ejemplos de instancias:** 1, 2, 3, 4, 5, 6, 7

### 5. EggGroup
- **Descripción:** Grupo de crianza al que pertenece un Pokémon. Determina con qué otros Pokémon puede reproducirse.
- **Origen:** `DataSet2.csv` (columnas Group1, Group2)
- **Enlace con dataset central:** por Name/Form
- **Ejemplos de instancias:** Monster, Water 1, Fairy, Dragon, Field

### 6. CurvaDeExperiencia
- **Descripción:** Tipo de curva de crecimiento que determina cuánta experiencia necesita un Pokémon para subir de nivel.
- **Origen:** `DataSet2.csv` (columna Exp_Speed)
- **Enlace con dataset central:** por Name/Form
- **Ejemplos de instancias:** Slow, Medium, Fast, Medium Slow, Medium Fast, Erratic, Fluctuating

### 7. Hábitat
- **Descripción:** Entorno natural donde habita el Pokémon. Solo disponible para Pokémon de las generaciones 1-3 (380 de 1061).
- **Origen:** `pokemon_habitats.csv` (PokeAPI)
- **Enlace con dataset central:** `pokemon.csv` (Form → minúsculas) → `pokemon_species.csv` (identifier) → habitat_id → `pokemon_habitats.csv`
- **Ejemplos de instancias:** cave, forest, grassland, mountain, rare, rough-terrain, sea, urban, waters-edge

### 8. Habilidad
- **Descripción:** Capacidad pasiva que posee un Pokémon y que afecta al combate o a la exploración. Existen 265+ habilidades distintas.
- **Origen:** `abilities.csv` + `pokemon_abilities.csv` (PokeAPI)
- **Enlace con dataset central:** `pokemon.csv` (Form → minúsculas) → `pokemon_species.csv` (identifier → id) → `pokemon_abilities.csv` (pokemon_id) → ability_id → `abilities.csv`
- **Ejemplos de instancias:** Overgrow, Blaze, Torrent, Chlorophyll, Intimidate

### 9. Color
- **Descripción:** Color predominante del Pokémon según la clasificación oficial.
- **Origen:** `pokemon_colors.csv` (PokeAPI)
- **Enlace con dataset central:** `pokemon.csv` (Form → minúsculas) → `pokemon_species.csv` (identifier) → color_id → `pokemon_colors.csv`
- **Ejemplos de instancias:** black, blue, brown, gray, green, pink, purple, red, white, yellow

### 10. FormaCorporal
- **Descripción:** Clasificación de la silueta o estructura corporal del Pokémon.
- **Origen:** `pokemon_shapes.csv` (PokeAPI)
- **Enlace con dataset central:** `pokemon.csv` (Form → minúsculas) → `pokemon_species.csv` (identifier) → shape_id → `pokemon_shapes.csv`
- **Ejemplos de instancias:** ball, squiggle, fish, arms, blob, upright, legs, quadruped, wings, tentacles, heads, humanoid, bug-wings, armor

## Resumen de enlace entre datasets

```
pokemon.csv (Form)
  │
  ├─[directo]─────► Type1, Type2 → clase Tipo
  │
  ├─[por Name]────► DataSet2.csv
  │                    ├── Region         → clase Región
  │                    ├── Generation     → clase Generación
  │                    ├── Group1, Group2 → clase EggGroup
  │                    └── Exp_Speed      → clase CurvaDeExperiencia
  │
  └─[minúsculas]──► pokemon_species.csv (identifier → id)
                       ├── habitat_id  ──► pokemon_habitats.csv   → clase Hábitat
                       ├── color_id    ──► pokemon_colors.csv     → clase Color
                       ├── shape_id    ──► pokemon_shapes.csv     → clase FormaCorporal
                       └── id = pokemon_id en pokemon_abilities.csv
                                              └── ability_id ──► abilities.csv → clase Habilidad
```
