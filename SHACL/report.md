# SHACL Validation Report — Pokémon Ontology

**Course:** Developing Open, Interoperable Semantic Resources (UPM)
**Ontology IRI:** `http://example.org/pokemon#`
**Files delivered:**

- `shapes.ttl` — 10 SHACL shapes
- `data.ttl` — 7 conformant + 13 non-conformant Pokémon and value-class individuals
- `validation_report.ttl` — machine-readable SHACL validation report
- `report.md` — this human-readable report

**Validator used:** `pyshacl 0.30+` (SHACL Core + SHACL-SPARQL).
Command: `pyshacl -s shapes.ttl -d data.ttl -f human`.

---

## 1. Overview of the 10 SHACL shapes

Each shape was designed to validate a **different kind** of constraint, so that the deliverable shows the breadth of SHACL expressivity rather than ten variants of the same check.

| # | Shape | Target | Constraint kind | Why it matters |
|---|---|---|---|---|
| 1 | `PokemonShape` | `pokemon:Pokemon` | `sh:datatype` + `sh:minCount`/`sh:maxCount` + `sh:minInclusive`/`sh:maxInclusive` | The 6 base stats and `nombreForma` are mandatory; stats must be integers in the canonical Pokémon range [1, 255]. |
| 2 | `PokemonTypeShape` | `pokemon:Pokemon` | `sh:class` + `sh:nodeKind` + cardinality | Every Pokémon needs exactly one primary type and at most one secondary type, both pointing to instances of `pokemon:Tipo`. |
| 3 | `PokemonHiddenAbilityShape` | `pokemon:Pokemon` | `sh:datatype xsd:boolean` | The hidden-ability flag must be a boolean (true/false), not a string. |
| 4 | `PokemonNameShape` | `pokemon:Pokemon` | `sh:pattern` + `sh:minLength` / `sh:maxLength` | `nombreForma` must start with a capital letter and only contain letters, digits, spaces, hyphens or dots. |
| 5 | `PokemonBaseTotalShape` | `pokemon:Pokemon` | **`sh:sparql`** + numeric range | `baseTotal` must equal `hp + attack + defense + spAtk + spDef + speed`. This is a multi-property logical constraint that pure SHACL Core cannot express. |
| 6 | `RegionShape` | `pokemon:Region` | `sh:in` (closed enumeration) | Only the 7 regions present in DataSet2.csv are accepted. |
| 7 | `GenerationShape` | `pokemon:Generacion` | Integer range `[1, 7]` | The dataset only covers generations 1-7. |
| 8 | `ColorShape` | `pokemon:Color` | `sh:in` (closed enumeration) | Only the 10 official Pokémon colors are accepted. |
| 9 | `CaptureRateShape` | `pokemon:Pokemon` | Integer range `[3, 255]` | Capture-rate is an in-game integer in this range. Optional (no `minCount`). |
| 10 | `PokemonHabitatShape` | `pokemon:Pokemon` | `sh:nodeKind sh:IRI` + `sh:class pokemon:Habitat` | Habitat is optional (only gens 1-3 have habitat data) but, if present, must be an IRI of class `pokemon:Habitat`. |

The four kinds of constraints covered are therefore: **(a)** cardinality, **(b)** datatype, **(c)** value range / closed enumeration / pattern, **(d)** object-property class targeting and **(e)** SPARQL-based cross-property logical rule.

---

## 2. Sample data

The data graph contains:

- **Value-class individuals** (Tipo, Region, Generacion, EggGroup, CurvaDeExperiencia, Habitat, Habilidad, Color, FormaCorporal) needed to instantiate the object properties.
- **7 conformant Pokémon** (`Bulbasaur`, `Charmander`, `Squirtle`, `Pikachu`, `Charizard`, `Greninja`, `Pidgey`) populated from the real `pokemon.csv` and `DataSet2.csv` data.
- **13 non-conformant individuals** (10 broken Pokémon + 3 broken value-class instances `Orre`, `Gen9`, `ColorMagenta`) each carefully designed to **trigger one specific shape**.

---

## 3. Validation results

The validator returned **`sh:conforms = false`** with **15 validation results** (more than 13 because one Pokémon, `Bad_Attack_DatatypeWrong`, simultaneously triggers three numeric checks — see §4).

### 3.1 Mapping of detected violations to shapes

| # | Shape | Focus node | Violated constraint component | Offending value | Diagnosis |
|---|---|---|---|---|---|
| 1 | `PokemonShape` (hp) | `pokemon:Bad_HP_OutOfRange` | `MaxInclusiveConstraintComponent` | `300` | hp = 300 > 255. |
| 2 | `PokemonShape` (attack) | `pokemon:Bad_Attack_DatatypeWrong` | `DatatypeConstraintComponent`, `MinInclusiveConstraintComponent`, `MaxInclusiveConstraintComponent` | `"fifty"` | String instead of integer; also fails range checks because the value is not numerically comparable to 1 or 255. |
| 3 | `PokemonShape` (speed) | `pokemon:Bad_MissingSpeed` | `MinCountConstraintComponent` | (no value) | `speed` property is missing. |
| 4 | `PokemonTypeShape` | `pokemon:Bad_NoPrimaryType` | `MinCountConstraintComponent` | (no value) | `tieneTipoPrimario` is missing. |
| 5 | `PokemonTypeShape` | `pokemon:Bad_TwoPrimaryTypes` | `MaxCountConstraintComponent` | (two values) | Two primary types declared; max allowed is 1. |
| 6 | `PokemonHiddenAbilityShape` | `pokemon:Bad_HiddenAbility_NotBoolean` | `DatatypeConstraintComponent` | `"yes"` | Plain literal "yes" is not `xsd:boolean`. |
| 7 | `PokemonNameShape` | `pokemon:Bad_NameLowercase` | `PatternConstraintComponent` | `"bad_name!"` | Starts in lowercase and contains `_` and `!`. |
| 8 | `PokemonBaseTotalShape` | `pokemon:Bad_BaseTotalSum` | `SPARQLConstraintComponent` | (sum mismatch) | `baseTotal=999` ≠ 60+60+60+60+60+60 = 360. |
| 9 | `RegionShape` | `pokemon:Orre` | `InConstraintComponent` | `"Orre"` | Region "Orre" is not in the closed enumeration. |
| 10 | `GenerationShape` | `pokemon:Gen9` | `MaxInclusiveConstraintComponent` | `9` | Generation 9 is outside [1,7]. |
| 11 | `ColorShape` | `pokemon:ColorMagenta` | `InConstraintComponent` | `"magenta"` | Color "magenta" is not in the closed enumeration. |
| 12 | `CaptureRateShape` | `pokemon:Bad_CaptureRateOutOfRange` | `MaxInclusiveConstraintComponent` | `500` | `captureRate=500` > 255. |
| 13 | `PokemonHabitatShape` | `pokemon:Bad_HabitatNotHabitat` | `ClassConstraintComponent` | `pokemon:Grass` | The IRI is an instance of `pokemon:Tipo`, not `pokemon:Habitat`. |

> The two extra results in the count of 15 correspond to the same `Bad_Attack_DatatypeWrong` focus node failing three numeric checks simultaneously (datatype, minInclusive, maxInclusive). All 10 shapes produced at least one violation.

### 3.2 Conformant individuals — no violations

The 7 valid Pokémon (`Bulbasaur`, `Charmander`, `Squirtle`, `Pikachu`, `Charizard`, `Greninja`, `Pidgey`) produced **zero** validation results, which confirms the shapes are not over-restrictive. In particular:

- `Greninja` and `Pidgey` show that the optional properties (`viveEnHabitat`, `tieneTipoSecundario`) really are optional.
- `Bulbasaur`'s `baseTotal = 318` matches `45 + 49 + 49 + 65 + 65 + 45 = 318`, confirming the SPARQL constraint passes when the data is correct.

---

## 4. Lessons learned and corrections applied during the exercise

The work was iterative. Below are the issues encountered and how they were resolved.

### 4.1 Unintended cascading violations on bad datatypes

When `pokemon:attack "fifty"` was first added, it produced **three** validation results instead of one (datatype, minInclusive and maxInclusive all failed). This is technically correct SHACL behaviour: a non-numeric literal cannot be compared, so range tests also fail. **Decision:** keep the shape as is — the behaviour is informative for the user, and splitting it would require artificially weakening the constraint. The report clearly notes this in §3.

### 4.2 Closed enumerations on value classes vs. on Pokémon

An earlier draft put `sh:in` directly on `pokemon:Pokemon` via `pokemon:disponibleEnRegion`, listing IRIs like `pokemon:Kanto`. This is brittle: every new region would require updating the shape. **Refactored to** target the value class itself (`pokemon:Region`) and check the closed list against the literal value of `nombreRegion`. The same refactor was applied to `Color`. Now adding a new instance of `pokemon:Region` only requires adding it to the data graph — provided its `nombreRegion` is in the closed list, no shape edit is needed.

### 4.3 SPARQL prefix declaration

The `PokemonBaseTotalShape` initially failed with `Unknown prefix 'pokemon'` because SHACL-SPARQL does **not** inherit the prefixes of the shapes graph. **Fix:** the shape now embeds an explicit `sh:prefixes [ sh:declare [ ... ] ]` block, which is the SHACL-spec-mandated way to make the prefix visible inside `sh:select`.

### 4.4 Habitat as optional, not mandatory

In the requirements (REQ-28 and the linkage document) it is explicitly stated that habitat data only exists for Pokémon of generations 1-3 (380 of 1061). An early shape used `sh:minCount 1` on `viveEnHabitat`, which would have flagged Greninja (Gen 6). **Corrected to** drop `sh:minCount` and keep only `sh:maxCount 1`, `sh:nodeKind sh:IRI` and `sh:class pokemon:Habitat`. After re-running, Greninja conforms while `Bad_HabitatNotHabitat` still fails as intended.

### 4.5 No data correction needed for the conformant block

The 7 valid Pokémon were taken directly from the source CSVs. Their stats and `baseTotal` match by construction (the games guarantee it), so no data fix was needed for that subset. The whole SPARQL constraint can therefore be used as a future **bulk integrity check** when ingesting the full dataset of 1,061 Pokémon.

---

## 5. Reproducing the validation

```bash
pip install pyshacl
pyshacl -s shapes.ttl -d data.ttl -f human    # human-readable report (the one shown above)
pyshacl -s shapes.ttl -d data.ttl -f turtle   # writes a sh:ValidationReport in Turtle
```

Expected outcome: `Conforms: False`, **15 validation results** distributed across the 10 shapes exactly as described in §3.1.
