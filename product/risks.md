# Risiken & offene Fragen

Dinge die früh validiert oder entschieden werden müssen — bevor viel Code geschrieben wird.

---

## Kritische Risiken (Top 3 zuerst angehen)

### 1. Cold Start — akzeptiert & gelöst durch Community-Default

**Entscheidung (V1):** Leere Karte ist kein Risiko. Lösung: Alle Catches sind öffentlich (kein privat-Feature), so zeigt die Karte sofort Vögel von echten Menschen. Neuer Nutzer sieht: "hier sind Vögel — und ich bin Teil davon". Sein erster Catch wird für die ganze Stadt sichtbar. Das ist der Social-Hook: Nachbarn können deinen Catch sehen, können dir folgen.  
→ Keine eBird-Seed-Daten nötig. Beta-Mentality: „Wir bauen das gemeinsam auf — und jeder sieht es."

---

### 2. Illustrationen — rausgefallen, nachgereicht später

**Entscheidung (V1):** MVP ohne Custom-Illustrationen. Stattdessen quelloffene Bilder (Wikimedia Commons, ggf. Pixabay/Unsplash für Top-50). Rechtssicher, zeitnah, realistisch.  
→ Ästhetik-Differenzierung durch Haptik, Animationen, Layout — nicht durch Illustrationen. Aquarell-Art als Phase 2 wenn Nutzer-Traction das rechtfertigt.

---

### 3. Hintergrundmodus iOS — rausgefallen aus V1

**Entscheidung (V1):** Kontinuierlicher Hintergrundmodus zu komplex für iOS App Store (Compliance + Akku). 
→ V1 nur aktiver Modus (Handy in Hand). Hintergrundmodus als Phase 2, wenn iOS-Strategie besser verstanden.

---

## Produktschwächen (anzugehen vor V1)

### 3-Starter-Gate zu streng
"Dex öffnet sich erst nach Catch aller 3 Starter" kann Mia im Onboarding verlieren wenn sie gerade nicht draußen ist oder die Starter-Arten in ihrem Gebiet nicht vorkommen.  
→ **Überlegung:** 1 Catch reicht um Dex zu öffnen, 3 Starter sind Empfehlung nicht Gate.

### Datenmüll auf der Community-Karte
Kein Qualitätssicherungs-System. False Positives der Ton-ID + Spaß-Catches → Community-Karte wird wertlos. Kritisch besonders für "Seltener Vogel"-Benachrichtigungen.  
→ **Minimum für V1:** Seltenheits-abhängige Bestätigungsanforderung (seltene Arten → Foto required).

### Review-Phase als Feature noch nicht ausgearbeitet
"Drei Phasen"-Philosophie ist stark, aber der Review-Screen fehlt im Screens-Doc. Der Spaziergang als narrative Einheit (Route, Zeitleiste, Arten in Reihenfolge) ist ein Feature das Merlin/eBird nicht haben.  
→ **Als dedizierten Screen ausarbeiten:** "Heutiger Spaziergang" — Mini-Route, gehörte Arten, neue Catches.

### Sozialer Layer ohne Freunde wertlos
Feed leer bis Freundesnetz da ist.  
→ **Bereits adressiert durch Karte:** Community-Feed (alle öffentlichen Catches in der Nähe) als Default bis Freunde vorhanden. Explizit als Anti-Cold-Start-Strategie dokumentieren.

---

## Technische Offene Fragen

### Ton-ID: API-Wahl + Qualitätsstrategie
- [ ] BirdNET API (Cornell, kostenlos, non-commercial) vs. eigenes Modell vs. anderes
- [ ] Konfidenz-Threshold: Was zeige ich, was verwerfe ich? (zu niedrig = Fehler, zu hoch = frustration)
- [ ] False Positives: wie kommuniziere ich Unsicherheit an Mia ohne sie zu verwirren?
- [ ] Latenz: BirdNET braucht 3–15s Audio → kein echter Live-Stream, sondern Chunk-Polling

### Offline
Das Produkt ist vollständig online-abhängig (BirdNET API, Supabase, Mapbox Tiles). Merlin hat Offline — das ist ein echter Vorteil in Parks/Wäldern ohne Empfang.  
- [ ] Entscheiden: bewusst offline-los bleiben (und kommunizieren) oder Offline-First als späteres Feature einplanen?

### Push-Benachrichtigungen für Nähe-Alerts
"Eisvogel 800m von dir" erfordert server-seitig bekannten Nutzer-Standort.  
- [ ] Ansatz: letzter bekannter Standort in Supabase (ungenau) vs. client-side Geofencing (weitere Permission)
- [ ] Datenschutz-Kommunikation: Nutzer müssen verstehen was gespeichert wird

### Vogel-Datenbank Aufbau
- [x] eBird-Taxonomie als Basis — entschieden (→ decisions.md)
- [x] species_code als PK, scientific_name als BirdNET-Anker — entschieden
- [ ] xeno-canto für Gesänge: Creative Commons, aber Lizenz-Varianten prüfen (CC-BY vs. CC-BY-NC)
- [ ] Content-Aufwand: Beschreibungen, Fun Facts, Lebensraum für ~300 DACH-Arten — wer/wie/womit? Wikipedia-API als Ausgangspunkt oder manuell kuratiert?
- [ ] Vogel-Bilder: manuell kuratiert oder automatisiert via Wikipedia/Flickr-API im Seed-Script?

### Geografischer Fokus
- [ ] Deutschland gesamt vs. nur Hamburg/Berlin für MVP?
- [ ] Regionale Arten-Taxonomie (was ist "in Deutschland" vs. "regional selten") — wann nötig?

---

## Bereits entschiedene Fragen (zur Erinnerung)
- Monetarisierung: keine Priorität — Education, Spaß, Verbreitung im Vordergrund
- Kollaborativ statt kompetitiv: entschieden
- Wöchentlicher Streak: entschieden
- Expo + Supabase + Mapbox: entschieden
- Auto-Catch im Hintergrundmodus: NEIN — nur Alert, User bestätigt manuell (wichtig für Datenqualität + Erlebnismoment)
