# Screens

Navigation: **Untere Tab-Leiste** mit 4 Tabs (außer während Ton/Foto-ID — Vollbild).

---

## Tab 1: Karte
- Vollbild-Karte (Mapbox), Catch-Pins / Cluster — **zeigt alle Catches der Stadt (alles ist öffentlich)**
- Filterleiste: Art, Zeitraum, Nur-Freunde-Toggle (optionales Refinement), Heatmap-Toggle
- Schwebender „Cachen"-Button (primärer CTA, immer sichtbar)
- Pin antippen → Mini-Karte (Art, Nutzer, Zeit, Entfernung) → Catch-Detail
- Nutzer-Profile einsehbar über Pins (ohne Freundschafts-Barriere)

## Tab 2: Cachen (Aktion)
1. **Methoden-Auswahl** — Gehört? Gesehen? Ton-ID oder Foto-ID?
2. **Ton-ID** — Live-Zuhören, Wellenform-Animation, Artenergebnis
3. **Foto-ID** — Kamera-Sucher, Aufnahme, Artenergebnis
4. **Manuelle Suche** — Suchleiste, Artenliste
5. **Bestätigungsscreen** — Art bestätigt, Methode, optionale Notiz/Foto, Standortvorschau
6. **Erfolgsscreen** — Animation + Belohnung + „Teilen"-Option

## Tab 3: Bird-Dex
- Raster aller regionalen Arten: gecacht (Illustration + Name) / nicht gecacht (Silhouette + ?)
- Fortschrittsbalken: „34 / 550 Arten gecacht"
- Filter: Familie, Lebensraum, Seltenheit, Jahreszeit, „Noch nicht gecacht"

**Arten-Detailscreen:**
- Großes Bild (Wikimedia-Foto, V1)
- Name (DE + wissenschaftlich), 1-Satz-Beschreibung, Seltenheit, Jahreszeit
- Gesang-Player
- Ausklappbar: Lebensraum, Nahrung, Zugverhalten, Verwechslungsarten, Fun Facts
- Meine Catches (wann/wo + Mini-Karte)
- Community: Catch-Anzahl, Hotspot-Karte
- „Jetzt cachen"-Button

## Tab 4: Profil & Soziales
- **Mein Profil** — Avatar, Username, Level/XP, Badges, Stats
- **Meine Badges** — verdient + gesperrt
- **Aktivitätsfeed** — Freundes-Catches chronologisch
- **Freundesliste** — mit jüngster Aktivität
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
