# Entscheidungen

## Produkt
- **Alle Catches öffentlich** — kein privat-Feature. Totale Transparenz = Community-Fundament.
- **Kollaborativ, nicht kompetitiv** — keine Rankings.
- **Wöchentlicher Streak** (kein täglicher) — Vogelbeobachtung ist Freizeit.
- **Auto-Catch: NEIN** — nur Alert, User bestätigt manuell (Datenqualität + Erlebnismoment).
- **3-Starter: weich** — 1 Catch reicht um Dex zu öffnen, 3 Starter sind Empfehlung.
- **Cold Start akzeptiert** — leere Karte ist Beta-Narrative "neue Karte bepflanzen".
- **Phase 2 (kein V1-Scope):** Hintergrundmodus (iOS zu komplex) | Custom-Illustrationen | On-Device TFLite

## Tech-Stack
- **Mobile:** Expo (React Native) + TypeScript
- **Backend:** Supabase (PostGIS, Realtime, Auth, Storage)
- **Karten:** Mapbox GL | **Styling:** NativeWind

## Ton-ID
- **BirdNET-Analyzer auf VPS** (Hetzner CX22, ~4€/Monat) — App schickt 3s-Chunks per HTTP, Server antwortet mit JSON.
- BirdNET-Output: `"Cyanistes caeruleus_Eurasian Blue Tit"` → split `_` → `scientific_name`-Lookup.
- On-Device TFLite: Phase 2 (erfordert native Swift/Kotlin Audio-Bridge).

## Vogel-Datenbank
- **Quelle:** eBird-Taxonomie CSV — alle EU-Arten laden, `is_local = true` für ~300 DACH-Arten.
- **PK:** eBird `species_code` (z.B. `eurblu`) — stabiler als laufende ID, von xeno-canto verstanden.
- **Match-Anker:** `scientific_name` (UNIQUE) — BirdNET-Output-Lookup.
- **Pflege:** ausschließlich via `seed_birds.ts` (UPSERT) — nie manuell im Dashboard.
- **Bilder:** Wikimedia Commons API im Seed-Script, `photo_credit` in DB. Phase 2: AI-Styling.

## Geografie & Sprache
- **DACH zuerst** — ~300 `is_local`-Arten im Dex. Alle EU-Arten in DB vorhanden.
- **i18n von Anfang an** — alle UI-Strings in `i18next`, keine Hard-coded Texte. Vogelnamen in DB: DE + EN + wissenschaftlich.
