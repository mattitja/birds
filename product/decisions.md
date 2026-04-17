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

---

## Offene Fragen
- [ ] Vogel-DB: Eigene aus eBird-Taxonomie befüllen oder API? (xeno-canto für Audio)
- [ ] Ton-ID: BirdNET API (Cornell, kostenlos) vs. Merlin SDK vs. eigenes Modell?
- [ ] Monetarisierungsmodell? (aktuell keine Priorität)
- [ ] Geografischer Fokus: Hamburg/Deutschland für MVP oder global?
