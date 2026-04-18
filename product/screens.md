# Screens

Navigation: **Untere Tab-Leiste** mit 3 Tabs (außer während Catch-Aktion — Vollbild).

Tab-Reihenfolge (links → rechts): **Map | Catch | Bird-Dex**. Map ist **Default-Tab** beim Start. Profile / Einstellungen: erreichbar via Avatar-Icon im Bird-Dex-Header (minimal, kein eigener Tab).

---

## Tab 1: Map (Default)
**Ziel:** Community-Catches erkunden, Motivation zum Rausgehen schaffen, räumliche Neugier wecken.

- **Vollbild-Karte (Mapbox)**, centered auf Nutzer-Standort (Stadt/Umkreis)
- **Alle Community-Catches** als Pins/Cluster sichtbar — kein Follower-Gate, alles öffentlich
- **Filterleiste** (oben): Art (alphabetisch)
- **Keine "Catchen"-Button auf dieser Seite** — Catchen erfolgt über eigenen Tab (Tab 2)
- **Pin antippen** → Mini-Card: Art + Username — **kein Profil-Link im MVP**
- **Design-Intent:** "Da ist ein Eisvogel 300m von hier" → motiviert, dort hinzulaufen und selbst zu suchen

## Tab 2: Catchen (Catch-Aktion)
**Ziel:** Intuitives, spielerisches Vogel-Identifizieren — wie Shazam, aber mit Pokéball-Wurfmechanik.

1. **Hauptscreen — Mikrofon-Geste**
   - **Großes Mikrofon-Icon** (visuell zentral, Shazam-Ästhetik, hochauflösend)
   - Tap → Live-Tonaufnahme + Wellenform-Visualisierung
   - BirdNET-Erkennung läuft dann im Hintergrund

2. **Erkannter Vogel — Vorschlag-Card**
   - Card schiebt sich von oben ins Bild (oder fade-in)
   - Zeigt: Vogel-Illustration, Name, Confidence-Prozentsatz (z.B. "Rotkehlchen 87%")

3. **Catch-Geste — Pokéball-Throw**
   - Nutzer **swipet die Card nach oben** → fangen, speichern
   - **Haptisches Feedback** beim Loslassen
   - → nahtlos in **Erfolgsscreen** übergehen

4. **Erfolgsscreen** — Fullscreen: 
   - falls erster Catch: große Illustration, Konfetti/Partikel, „Erstes [Art] gecatcht!"
   - falls schon im Bird-Dex vorhanden: "[Vierter] Catch eines [Art]!"

5. Pin ploppt auf der Karte auf — als eigener Catch markiert

6. **Fallback — Manuelle Suche**
   - Suchleiste, gefilterte Artenliste nach Eingabe → Catch ohne Ton-ID möglich

## Tab 3: Bird-Dex (Sammlung)
**Ziel:** Pokédex-Effekt — Progression sichtbar, gefangene + ungefangene Arten in einem Blick.

### Hauptscreen — Art-Raster
- **Grid aller regionalen Arten** (DACH)
- **Gecatchte Arten:** Vogelillustrationen + Name (farbig, hochauflösend)
- **Ungecatchte Arten:** Silhouette + "?" (grau, andeutungsvoll — keine volle Enthüllung, aber Vogelname steht da)
- **Fortschrittsbalken oben:** "34 / **312 Arten in DACH gecatcht**" 
  - Gesamtzahl = alle Species mit `is_local = true` aus DB (konstant, motivierend)
- **Filter-Bar:** Familie, Lebensraum, Seltenheit, Jahreszeit, "Noch nicht gecatcht"
- **Tap auf Art** → Art-Detailscreen
- Für jede Art ist aufgezählt, wie oft sie schon gecatcht wurde

### Arten-Detailscreen
- **Großes Bild** (Wikimedia-Foto) — ungecatchte Arten zeigen trotzdem Fotos
- **Name:** DE + wissenschaftlich
- **1-Satz-Beschreibung** (Wikipedia-API automatisiert)
- **Meine Catches** — wann/wo (wenn schon gecatcht)
- **Buttons:**
  - **"Auf Karte zeigen"** → öffnet Tab 1 (Map), **gefiltert nach dieser Art**
  - **"Jetzt catchen"** → öffnet Tab 2 (Catch)
- **V1:** Gesang-Player, Lebensraum, Nahrung, Zugverhalten, Verwechslungsarten, Fun Facts, Community-Hotspot-Karte

## Globale Screens
| Screen                                  | Auslöser |
|-----------------------------------------|---|
| Onboarding (Wähle dein Starter-Vogel)   | Erster Start |
| Catch-Detail (Modal)                    | Catch-Pin antippen |
| Arten-Schnellkarte (Sheet)              | Art irgendwo in der App antippen |

## Ästhetik
- **Bilder**: quelloffene Fotos (Wikimedia), warm — Aquarell/Gouache Phase 2
- **Farben**: Erdtöne, Waldgrün, Himmelblau + lebendige Akzentfarbe
- **Typografie**: Lesbar bei Sonnenlicht, ausreichend Kontrast
- **Animationen**: Jede Interaktion hat Feedback — Catch ist der Premium-Moment
- **Haptik**: Vibration beim Catch, neuer Art, Badge-Verdienen
- **Dark Mode**: von Anfang an (draußen in der Dämmerung/Morgengrauen)
- **Catch-Erfolg**: Vollbild — große Illustration, Konfetti/Partikel, Vogelgeräusch
