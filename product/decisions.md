# Entscheidungs-Log

## Produktentscheidungen

**Kollaborativ statt kompetitiv**  
Keine Ranglisten. Hohes Missbrauchsrisiko (gefälschte Catches), schreckt Casual-User ab. Kollaborative Meilensteine statt Wettbewerb.

**Catches standardmäßig öffentlich**  
Community-Karte funktioniert nur mit Daten. Freunde/privat als Option. Datenschutz für sensible Sichtungen (Nistplätze) verfügbar.

**Wöchentlicher Streak, kein täglicher**  
Tägliche Streaks = Angst + Churn. Vogelbeobachtung ist Wochenend-/Freizeitaktivität.

**Ton-ID vor Foto-ID (V1)**  
Ton ist der Merlin-Hook — funktioniert passiv, viele Vögel werden gehört bevor sie gesehen werden. Reibungsärmste Methode für Einsteiger.

---

## Technische Entscheidungen

**Expo (React Native)**  
Cross-platform (iOS + Android), eingebaute Kamera/Mikrofon/Standort-APIs, TypeScript, großes Ökosystem, gute LLM-Trainingsdaten = besseres agentic Coding.  
Kompromiss: etwas weniger Performance als nativ — akzeptabel.

**Supabase als Backend**  
PostGIS eingebaut (Karte/Heatmap), Realtime (sozialer Feed), Auth (Social Login), Storage (Fotos), Row-Level-Security (Datenschutz). Gute Doku = gutes agentic Coding-Ziel.  
Kompromiss: Vendor-Lock-in — aktuell akzeptabel.

**Mapbox statt Google Maps / Leaflet**  
Heatmap-Layer, individuelles Styling, Clustering eingebaut, bessere Performance bei großen Datensätzen.  
Kompromiss: kostenpflichtig über Free Tier — für Kartenqualität es wert.

**Vogel-Bilder: Wikimedia Commons API für V1, optional AI-Styling später**  
Quelle: Wikipedia/Wikimedia API (100% Abdeckung EU-Vögel, CC-lizenziert, rechtssicher). Seed-Skript zieht Bild-URL + Fotografen-Credit direkt in die DB. Für höheren Pokémon-Vibe: später optional Stable Diffusion (Replicate/Fal.ai) um Foto → einheitliche Illustration zu transformieren.

**Vogel-DB: eBird/Clements Taxonomie als Quelle, eBird species_code als Primary Key**  
Quelle der Wahrheit: eBird-Taxonomie (Cornell Lab) als CSV-Download (~10.000 Arten). Wissenschaftlicher Name als BirdNET-Match-Anker (BirdNET-Output: `"Cyanistes caeruleus_Eurasian Blue Tit"` → split → scientific_name → DB-Lookup). eBird species_code (z.B. `eurblu`) als stabiler PK — überdauert taxonomische Updates, wird von xeno-canto + anderen APIs verstanden.  
Pflege: einziger Weg ist das `seed_birds.ts` Seed-Script (UPSERT) — kein manuelles Editieren im Dashboard.  
Umfang: alle europäischen Arten in die DB laden (Postgres lacht über 10.000 Zeilen). Frontend-Filter via `is_local`-Flag für ~250–300 DACH-Arten.

**Sprache: Deutschsprachiger Raum zuerst, Mehrsprachigkeit strukturell vorbereitet**  
MVP startet auf Deutsch (DE/AT/CH). Kein aktiver Aufwand für weitere Sprachen in V1.  
Aber: alle Strings in i18n-Struktur (z.B. `i18next`), Vogelnamen in der DB mehrsprachig angelegt (DE + wissenschaftlich als Pflichtfelder, EN + weitere als optionale Spalten). Kein Hard-coded Text im Code. Übersetzungen können nachgezogen werden ohne strukturelle Änderungen.

**Cold Start: Akzeptiert & Reframed als Narrative**  
Community-Karte startet leer. Das ist kein Bug, sondern Feature-Moment: neue Nutzer "pflanzen eine neue Karte". Erste Catches werden zum Community-Highlight. eBird-Seed-Daten nicht nötig.

**Illustrationen: MVP ohne Custom-Art, quelloffene Bilder stattdessen**  
Hochwertige Vogel-Aquarelle sind nicht im V1-Scope. Stattdessen: Wikimedia Commons + ggf. Pixabay/Unsplash für die Top-50 häufigen Arten. Sauberer, rechtssicherer, rechtszeitig. Custom-Illustrationen als Phase 2, wenn es sich lohnt.

**Background/Silent Mode: Phase 2 (raus aus V1)**  
iOS App Store Compliance zu streng, zu viel technische Komplexität (kontinuierliches Mikrofon + GPS = Rejection-Risk). V1 auf aktiven Modus fokussieren. Hintergrundmodus später, wenn iOS-Strategie klarer ist.

**Ton-ID: Selbst gehosteter BirdNET-Analyzer (kein On-Device TFLite für V1)**  
On-Device TFLite wäre ideal (offline, kein Akku durch Netzwerk, kein Datenschutz-Problem), erfordert aber native Audio-Bridge (Swift/Kotlin) + BirdNET TFLite-Modell-Integration — zu hoher Aufwand für MVP.  
Entschieden: Selbst gehosteter BirdNET-Analyzer auf VPS (z.B. Hetzner CX22, ~4€/Monat). App schickt 3s-Chunks per HTTP, Server antwortet mit JSON. On-Device als spätere Iteration (Phase 2).  
Offline-Einschränkung bewusst akzeptiert.

---

## Offene Fragen
- [ ] Vogel-DB: Eigene aus eBird-Taxonomie befüllen oder API? (xeno-canto für Audio)
- [ ] Monetarisierungsmodell? (aktuell keine Priorität)
- [ ] Geografischer Fokus: Hamburg oder ganz Deutschland für MVP?
