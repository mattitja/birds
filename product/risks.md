# Risiken & offene Fragen

Dinge die früh validiert oder entschieden werden müssen — bevor viel Code geschrieben wird.

---

## Kritische Risiken (Top 3 zuerst angehen)

### 1. Cold Start — leere Karte killt Onboarding

Die Community-Karte ist zentraler Value-Prop, aber funktioniert nur mit Daten. Journey 1 (Mia sieht Pin → Neugier → erster Catch) funktioniert nicht auf einer leeren Karte.

**Optionen:**
- [ ] eBird/GBIF-Daten als historische Seed-Daten einlizenzieren (machbar, lizenzrechtlich prüfen)
- [ ] Launch auf eine einzige Stadt fokussieren und dort dichte Community aufbauen
- [ ] Community-Karte erst nach kritischer Masse einführen — MVP ohne Karte?
- [ ] Karte zeigt primär eigene Catches bis Freunde vorhanden → sozialer Druck als Sekundär-Wachstum

**Entscheidung ausstehend.**

---

### 2. Illustrationen — kritischer Pfad, massiv unterschätzt

Hochwertige Aquarell/Gouache-Illustrationen für 550 Arten sind das Fundament der Ästhetik-Differenzierung. Ohne das wird die App zu einer weiteren generischen Natur-App.

**Optionen:**
- [ ] Professioneller Vogel-Illustrator: konsistent, teuer, langsam (Wochen bis Monate)
- [ ] KI-generiert (Midjourney o.ä.): schnell, günstig — Konsistenz über 550 Arten schwer zu halten
- [ ] Hybrider Ansatz: KI-Basis + manuelles Nachbearbeiten für die wichtigsten ~50 Arten zuerst
- [ ] Lizenzierte Bibliothek: prüfen ob Vogel-Illustrations-Bibliotheken mit App-Lizenz existieren

**Muss sehr früh entschieden werden** — nicht als Detailfrage, als kritischer Pfad. MVP braucht mindestens die 50 häufigsten Arten in finaler Qualität.

---

### 3. Hintergrundmodus iOS — technisches Risiko

Kontinuierliche Mikrofon-Analyse im Hintergrund ist auf iOS keine Selbstverständlichkeit:
- `background audio` Berechtigung ist für Musik-Apps gedacht — Apple reviewt streng
- Permanentes Mikrofon + GPS + CPU ≈ 20–30% Akku pro Stunde (2h Wanderung = halber Akku)
- Privacy-Flag im App-Review möglich
- Bekannter Hack (stille Audio-Session im Hintergrund) funktioniert, kann aber abgelehnt werden

**Sofortmaßnahme:** Als isolierten Prototyp testen bevor V1 darauf aufgebaut wird.  
**Fallback:** Hintergrundmodus nur als "kurzes aktives Fenster" (z.B. 60s alle paar Minuten) statt dauerhaft.

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
- [ ] eBird-Taxonomie (offen verfügbar) als Basis für Artenliste
- [ ] xeno-canto für Gesänge (Creative Commons — Lizenz prüfen)
- [ ] Wer befüllt Beschreibungen, Fun Facts, Lebensraum-Infos für 550 Arten? (Content-Aufwand)

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
