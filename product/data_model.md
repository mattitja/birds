# Data Model (Conceptual)

Not SQL yet — entities, attributes, relationships.

## Entities

**User**: id, username, avatar_url, created_at, home_city, xp, level (derived)

**Bird**: id, common_name (DE/EN), scientific_name, family, description, photo_url, audio_sample_url, typical_regions[], typical_months[], rarity_score (common/uncommon/rare/very_rare), fun_facts[]

**Catch**: id, user_id, bird_id, caught_at, location (PostGIS Point), method (naked_eye/binoculars/heard_only/photo/sound_id), note?, photo_url?, visibility (public/friends/private), is_first_for_user

**Friendship**: id, requester_id, addressee_id, status (pending/accepted/blocked), created_at

**Badge**: id, key (slug), name, description, icon_url, trigger_condition

**UserBadge**: id, user_id, badge_id, earned_at

**Notification**: id, user_id, type (rare_bird_nearby/friend_catch/new_follower/weekly_recap/milestone), payload (JSON), read_at?, created_at

## Relationships
```
User ──< Catch >── Bird        (many-to-many through Catch)
User ──< Friendship >── User   (self-referential)
User ──< UserBadge >── Badge   (many-to-many)
User ──< Notification          (one-to-many)
```

## Key Queries
1. Public catches of species X near location Y within radius Z → heatmap, map pins
2. All catches by user X → profile/collection
3. Catches by friends of user X in last 7 days → activity feed
4. Has user X caught species Y? → new species check
5. Hottest species in city Z this month → trending
6. All catches within bounding box → map viewport

## DB Notes
- Catches need PostGIS geography type for spatial queries
- Bird table seeded from eBird taxonomy + xeno-canto
- Rarity is region-dependent → may need BirdRegionRarity join table later
- Notifications via DB triggers or edge functions, not app logic
