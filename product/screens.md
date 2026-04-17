# Screens

Navigationsstruktur: **Untere Tab-Leiste** mit 4 Tabs.

---

## Tab 1: Karte

**Haupteinstiegspunkt für die Erkundung.**

- Vollbild-Karte (Mapbox)
- Catch-Pins / Cluster sichtbar
- Filterleiste: Art, Zeitraum, Nur-Freunde-Toggle
- Heatmap-Toggle
- Schwebender "Cachen"-Button (primärer CTA, immer sichtbar)
- Pin antippen → Mini-Karte (Art, Nutzer, Zeit, Entfernung)
- Mini-Karte → klappt zu Catch-Detail aus

---

## Tab 2: Cachen (Aktion)

**Die Hauptaktion — ausgelöst vom FAB oder Tab.**

Flow (Screens innerhalb dieses Tabs):
1. **Catch-Methoden-Auswahl** — Gehört? Gesehen? Ton-ID oder Foto-ID nutzen?
2. **Ton-ID-Screen** — Live-Zuhören, Wellenform-Animation, Artenergebnis
3. **Foto-ID-Screen** — Kamera-Sucher, Aufnahme, Artenergebnis
4. **Manuelle Suche** — Suchleiste, Artenliste
5. **Catch-Bestätigungsscreen** — Art bestätigt, Methode wählen, optionale Notiz/Foto, Standortvorschau
6. **Catch-Erfolgsscreen** — Animation + Belohnung + "Teilen"-Option

---

## Tab 3: Sammlung

**Meine Vögel — der Pokédex.**

- Raster der gecachten Arten (ausgegraut für noch nicht gecachte, nach Region angezeigt)
- Sortierung: zuletzt gecacht / alphabetisch / Seltenheit
- Filter: Familie, Jahreszeit, Seltenheit
- Art antippen → **Arten-Detailscreen**
  - Foto, Name, Beschreibung, Gesang-Player
  - Meine Catches dieser Art (wo/wann)
  - Community-Catches (wie viele Leute haben sie gecacht, wo)
  - "Nochmal cachen"-Button

---

## Tab 4: Profil & Soziales

**Ich + meine Freunde.**

Screens:
- **Mein Profil** — Avatar, Benutzername, Level/XP-Leiste, Badges, Statistiken (Artenanzahl, Catch-Anzahl, Streak)
- **Meine Badges** — Raster der verdienten und gesperrten Badges
- **Aktivitätsfeed** — Freundes-Catches chronologisch
- **Freundesliste** — mit deren jüngster Aktivität
- **Freundesprofil** — deren öffentliche Sammlung + jüngste Catches
- **Einstellungen** — Benachrichtigungspräferenzen, Datenschutz, Account

---

## Globale / Overlay-Screens

| Screen | Auslöser |
|---|---|
| Onboarding (3 Folien) | Erster Start |
| Tutorial erster Catch | Nach erstem Ton-ID-Ergebnis |
| Catch-Detail (Modal) | Catch-Pin auf Karte antippen |
| Seltener-Vogel-Alarm (Push) | Benachrichtigung antippen → Karte mit hervorgehobenem Pin |
| Arten-Schnellkarte (Sheet) | Art irgendwo in der App antippen |

---

## Design-Hinweise

- Untere Tab-Leiste immer sichtbar (außer während Ton/Foto-ID — Vollbild)
- Cachen-Button (Mikrofon-Icon) könnte persistenter FAB über dem Karten-Tab sein
- Dark-Mode-Unterstützung von Anfang an (draußen in der Dämmerung/Morgengrauen)
- Große Tipper-Ziele — mit einer Hand im Freien bedient
- Minimale Texteingabe — tippen > tippen wo immer möglich
