# Entscheidungs-Log

Getroffene Entscheidungen mit Begründung. Aktualisieren wenn sich etwas ändert.

---

## Produktentscheidungen

### Kollaborativ statt kompetitiv
**Entscheidung:** Keine Ranglisten, keine kompetitiven Rankings.  
**Warum:** Hohes Missbrauchsrisiko (gefälschte Catches zum Aufsteigen). Wichtiger noch: Wettbewerb schreckt Casual-User (Mia) ab. Der Naturkontext ist von sich aus nicht kompetitiv — wir wollen, dass Menschen sich gegenseitig beim Entdecken von Vögeln helfen, nicht gegeneinander antreten.  
**Kompromiss:** Weniger Engagement von hyper-kompetitiven Nutzern — akzeptiert.

### Catches standardmäßig öffentlich
**Entscheidung:** Catches sind standardmäßig öffentlich (können auf Freunde/privat gesetzt werden).  
**Warum:** Community-Karte funktioniert nur wenn es Daten gibt. Öffentlicher Standard maximiert die Kartendichte von Anfang an. Datenschutzoptionen für sensible Sichtungen verfügbar (seltene Vögel, die Menschenmassen anziehen und Nistplätze stören könnten).

### Wöchentlicher Streak, kein täglicher
**Entscheidung:** Streak wird wöchentlich gemessen ("mindestens einmal diese Woche cachen"), nicht täglich.  
**Warum:** Tägliche Streaks erzeugen Angst und Churn. Vogelbeobachtung ist eine Wochenend-/Freizeitaktivität. Wir wollen ermutigen öfter rauszugehen, nicht dafür bestrafen einen Dienstag zu verpassen.

### Ton-ID vor Foto-ID im MVP
**Entscheidung:** Ton-Bestimmung für V1 priorisieren vor Foto-ID.  
**Warum:** Ton ist der "Merlin-Hook" — funktioniert passiv (man muss den Vogel nicht sehen). Viele Vögel werden gehört bevor sie gesehen werden. Das ist die wertvollste und reibungsärmste Bestimmungsmethode für Einsteiger.

---

## Technische Entscheidungen

### Expo (React Native) für Mobile
**Entscheidung:** Expo statt Flutter, nativem iOS/Android oder Web-only PWA.  
**Warum:** Cross-platform (iOS + Android aus einer Codebasis). Expo SDK hat Kamera-, Mikrofon- und Standort-APIs eingebaut. TypeScript-Unterstützung. Großes Ökosystem, gute LLM-Trainingsdaten = besseres agentic Coding.  
**Kompromiss:** Etwas weniger Performance als nativ. Für diesen Anwendungsfall akzeptabel.

### Supabase als Backend
**Entscheidung:** Supabase statt eigenem Node.js-Backend, Firebase oder PocketBase.  
**Warum:** PostGIS eingebaut = räumliche Abfragen für Karte/Heatmap ohne Extra-Setup. Realtime-Subscriptions für sozialen Feed. Auth mit Social-Providern out-of-the-box. Storage für Catch-Fotos. Row-Level-Security für Datenschutz. Starke Dokumentation = gutes agentic Coding-Ziel.  
**Kompromiss:** Weniger Kontrolle als eigenes Backend. Vendor-Lock-in-Risiko. Zum jetzigen Zeitpunkt akzeptabel.

### Mapbox statt Google Maps / Leaflet
**Entscheidung:** Mapbox GL JS / react-native-mapbox-gl.  
**Warum:** Heatmap-Layer, individuelles Styling (kann Pokémon-ähnliche Ästhetik erreichen), Clustering eingebaut. Bessere Performance als Leaflet bei großen Datensätzen.  
**Kompromiss:** Kostenpflichtig über Free Tier. Für Kartenqualität es wert.

---

## Offene Fragen

- [ ] Vogel-Artendatenbank: Eigene aus eBird-Taxonomie befüllen, oder API nutzen? (xeno-canto für Audio, eBird für Taxonomie)
- [ ] Ton-ID: BirdNET API (kostenlos, Cornell) vs. auf Merlin SDK aufbauen (falls verfügbar) vs. eigenes Modell?
- [ ] Monetarisierungsmodell? (aktuell keine Priorität, beeinflusst aber einige Designentscheidungen)
- [ ] Geografischer Fokus: Nur Hamburg / Deutschland für MVP, oder von Anfang an global?
