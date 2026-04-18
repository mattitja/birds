# Data Model (Conceptual)

Not SQL yet — entities, attributes, relationships.

## Entities

**User**: id, username, avatar_url, created_at, home_city, xp, level (derived)

**Bird**: species_code (PK, eBird code, z.B. "eurblu"), scientific_name (UNIQUE — BirdNET-Match-Anker), name_de, name_en, family_de, family_en, description_de?, fun_facts_de[]?, photo_url?, photo_credit?, audio_sample_url?, typical_months[], rarity_score (common/uncommon/rare/very_rare), is_local (Boolean — DACH-Filter für MVP)

**Catch**: id, user_id, bird_id, caught_at, location (PostGIS Point), method (naked_eye/binoculars/heard_only/photo/sound_id), note?, photo_url?, is_first_for_user

## Relationships
```
User ──< Catch >── Bird        (many-to-many through Catch)
```

## Key Queries
1. Catches of species X near location Y within radius Z → heatmap, map pins
2. All catches by user X → profile/collection
3. Catches by friends of user X in last 7 days → activity feed
4. Has user X caught species Y? → new species check
5. Hottest species in city Z this month → trending
6. All catches within bounding box → map viewport

## DB Notes
- Catches: PostGIS geography type für Spatial Queries
- Bird: seeded via `seed_birds.ts` (UPSERT) — nie manuell im Dashboard
- `is_local = true` für ~300 DACH-Arten (Dex + Suche). BirdNET erkennt trotzdem alle Arten.
