# Entscheidungen

## Produkt
- **Alle Catches öffentlich** — kein privat-Feature. Totale Transparenz = Community-Fundament.
- **Kollaborativ, nicht kompetitiv** — keine Rankings.
- **Wöchentlicher Streak** (kein täglicher) — Vogelbeobachtung ist Freizeit.
- **Der Catch** — User erfasst eine (Hör-)Begegnung mit einem Vogel, der wichtigste Moment
- **Kein Spam** — schon gecatchte Vögel werden nicht erneut aktiv gepusht
- **3-Starter: weich** — 1 Catch reicht um Dex zu öffnen, 3 Starter sind Empfehlung.
- **Cold Start akzeptiert** — leere Karte ist Beta-Narrative "neue Karte bepflanzen".
- **Folgen und Freundschaften** — man kann beliebigen Usern folgen, bei gegenseitigen Folgen ist es eine Freundschaft.
- **Map ist Default-Tab**: App-Start zeigt sofort Community-Activity (Karte mit Catches) — erzeugt FOMO, Erkundungsdrang, motiviert rausgehen.
- **Catch-Geste: Pokéball-Throw-Mechanik**: Vorschlag-Card wird per Swipe nach oben geworfen (nicht "Confirm"-Button). Der Wurf-Moment schafft Commitment, Magie und Spielgefühl — zentral für Mias Aha-Erlebnis.
- **Mikrofon als primäre CTA im Catch-Tab**: Shazam-Metapher ist kulturell bekannt (alle Generationen können damit umgehen), senkt mentale Hürde für Casual User.
- **Bird-Dex zeigt Gesamtzahl aller DACH-Arten**: Pokédex-Effekt — "34 / 312" schafft Progression-Gefühl und Gier nach mehr. Gesamtzahl ist fix, nicht personalisiert.
- **Species-Detail: "Auf Karte zeigen"-Button (gefiltert)**: Nahtlose Navigation zwischen Dex-Exploration und Map-Realität — Nutzer kann sofort sehen, wo die gefundene Art wahrscheinlich zu sehen ist.
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
