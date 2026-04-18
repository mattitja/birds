# Screens

Navigation: **Untere Tab-Leiste** mit 4 Tabs (außer während Catch-Aktion — Vollbild).

Tab-Reihenfolge (links → rechts): **Map | Catch | Bird-Dex | Profile**. Map ist **Default-Tab** beim Start.

---

## Tab 1: Map (Default)
**Ziel:** Community-Catches erkunden, Motivation zum Rausgehen schaffen, räumliche Neugier wecken.

- **Vollbild-Karte (Mapbox)**, centered auf Nutzer-Standort (Stadt/Umkreis)
- **Alle Community-Catches** als Pins/Cluster sichtbar — kein Follower-Gate, alles öffentlich
- **Filterleiste** (oben): Art, Zeitraum, Nur-Freunde-Toggle, Heatmap-Toggle
- **Keine "Catchen"-Button auf dieser Seite** — Catchen erfolgt über eigenen Tab (Tab 2)
- **Pin antippen** → Mini-Card (Art, Nutzer, Zeit) → Tap auf Card → Catch-Detail oder Nutzer-Profil
- **Design-Intent:** "Da ist ein Eisvogel 300m von hier" → motiviert, dort hinzulaufen und selbst zu suchen

## Tab 2: Catchen (Catch-Aktion)
**Ziel:** Intuitives, spielerisches Vogel-Identifizieren — wie Shazam, aber mit Pokéball-Wurfmechanik.

1. **Hauptscreen — Mikrofon-Geste**
   - **Großes Mikrofon-Icon** (visuell zentral, Shazam-Ästhetik, hochauflösend)
   - Tap → Live-Tonaufnahme + Wellenform-Visualisierung
   - BirdNET-Erkennung läuft im Hintergrund

2. **Erkannter Vogel — Vorschlag-Card**
   - Card schiebt sich von oben ins Bild (oder fade-in)
   - Zeigt: Vogel-Illustration, Name, Confidence-Prozentsatz (z.B. "Rotkehlchen 87%")

3. **Catch-Geste — Pokéball-Throw**
   - Nutzer **swipet / dragged die Card runter in seinen Bird-Dex** -> fangen, speichern
   - **Haptisches Feedback** beim Loslassen
   - → nahtlos in **Erfolgsscreen** übergehen
   
4. **Alternativ: Methoden-Menü** (klein, oben oder unten)
   - "Gehört" (Sound ID) / "Gesehen" (Foto-ID) / "Manuell suchen"
   - Für Nutzer, die anders identifizieren wollen

5. **Erfolgsscreen** — Fullscreen, wie in Tab 3 beschrieben
6. 
6. - Pin ploppt auf der Karte auf, Pin ist so markiert, das klar ist, dass es ein eigener Catch ist

6. **Fallback — Manuelle Suche** 
   - Suchleiste, gefilterte Artenliste nach Eingabe

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

### Arten-Detailscreen
- **Großes Bild** (Wikimedia-Foto, V1) — ungecatchte Arten zeigen trotzdem Fotos
- **Name:** DE + wissenschaftlich
- **1-Satz-Beschreibung**, Seltenheit, Jahreszeit
- **Gesang-Player** — Song abspielen
- **Ausklappbar:** Lebensraum, Nahrung, Zugverhalten, Verwechslungsarten, Fun Facts
- **Meine Catches** — wann/wo + Mini-Karte (wenn schon gecatcht)
- **Community:** Catch-Anzahl + Hotspot-Karte
- **Buttons oben/unten:**
  - **"Auf Karte zeigen"** → öffnet Tab 1 (Map), **gefiltert nach dieser Art** (MVP-Feature)
  - **"Jetzt catchen"** → öffnet Tab 2 (Catch), pre-filled mit dieser Art (optional)

## Tab 4: Profil & Soziales
- **Mein Profil** — Avatar, Username, Stats
- **Aktivitätsfeed** — Freundes-Catches chronologisch
- **Folge ich** — mit jüngster Aktivität
- **Freundesprofil** — öffentliche Sammlung + jüngste Catches
- **Einstellungen** — Benachrichtigungen, Datenschutz, Account

## Globale Screens
| Screen | Auslöser |
|---|---|
| Onboarding (3 Slides) | Erster Start |
| Tutorial erster Catch | Nach erstem Ton-ID-Ergebnis |
| Catch-Detail (Modal) | Catch-Pin antippen |
| Seltener-Vogel-Alarm | Push-Benachrichtigung → Karte mit hervorgehobenem Pin |
| Arten-Schnellkarte (Sheet) | Art irgendwo in der App antippen |

## Ästhetik
- **Bilder**: quelloffene Fotos (Wikimedia), warm — Aquarell/Gouache Phase 2
- **Farben**: Erdtöne, Waldgrün, Himmelblau + lebendige Akzentfarbe
- **Typografie**: Lesbar bei Sonnenlicht, ausreichend Kontrast
- **Animationen**: Jede Interaktion hat Feedback — Catch ist der Premium-Moment
- **Haptik**: Vibration beim Catch, neuer Art, Badge-Verdienen
- **Dark Mode**: von Anfang an (draußen in der Dämmerung/Morgengrauen)
- **Catch-Erfolg**: Vollbild — große Illustration, Konfetti/Partikel, Vogelgeräusch
