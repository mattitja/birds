# Features

Prioritätsstufen:
- **MVP** — für erste testbare Version erforderlich
- **V1** — für öffentlichen Launch erforderlich
- **Später** — wichtig, aber nicht blockierend
- **Vielleicht** — erst mit Nutzern validieren

---

## Vogelbestimmung

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Manuelle Suche nach Name | MVP | Fallback, immer nötig |
| Tonbestimmung (live) | V1 | Kern-Hook — wie Merlin. Drittanbieter-API (z.B. BirdNET) |
| Fotobestimmung | V1 | Drittanbieter-API (z.B. iNaturalist / BirdNET) |
| Artenliste durchsuchen | MVP | Gefiltert nach Region, Jahreszeit |

## Cachen

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Catch loggen (Art + Standort + Methode) | MVP | Methoden: mit bloßem Auge, Fernglas, nur gehört |
| Catch-Bestätigungsanimation / Belohnung | MVP | Das ist der magische Moment — muss sich toll anfühlen |
| Optionale Notiz / Foto zum Catch hinzufügen | V1 | |
| Eigenen Catch bearbeiten / löschen | V1 | |
| Private Catches | Später | Standard ist öffentlich/Freunde |

## Bird-Dex

Der Bird-Dex ist das Herzstück der App — nicht nur eine Artenliste, sondern das Sammlungsobjekt, für das man immer wieder rausgeht.

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Vollständiger regionaler Bird-Dex | MVP | Alle ~550 deutschen Brutvogelarten + häufige Durchzügler als Silhouetten sichtbar |
| 3 Starter-Vögel beim Onboarding | MVP | App wählt 3 häufige Arten in der Nähe vor — erst nach deren Catch öffnet sich der volle Dex |
| Artenkarte: Oberfläche | MVP | Illustration, Name, 1-Satz-Beschreibung, Seltenheitsindikator |
| Artenkarte: Tiefe | V1 | Gesang (Player), Lebensraum, Nahrung, Zugverhalten, Verwechslungsarten, Fun Facts |
| Silhouette → aufgedeckt beim ersten Catch | MVP | Das Aufdecken ist ein Belohnungsmoment |
| Arten nach Familie / Lebensraum / Seltenheit filtern | V1 | Für Ben: gezielt suchen; für Mia: stöbern |
| Fortschrittsanzeige im Dex | V1 | "Du hast 34 von 550 Arten gecacht" |
| Saisonale Verfügbarkeit pro Art | V1 | "Normalerweise März–September in Hamburg" |
| Catch-Verlauf pro Art | V1 | Wann/wo ich sie gecacht habe |
| "Neue Art"-Hervorhebung beim Catch | MVP | Erste Catch einer Art = besonderes Ereignis |
| Illustrationen: hochwertiger Aquarell/Gouache-Stil | MVP | Kernästhetik — kein Stockfoto, kein Cartoon |

## Karte

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Community-Karte mit allen öffentlichen Catches | MVP | Pins oder Cluster nach Art |
| Nach Art filtern | MVP | "Zeig mir alle Eisvogel-Sichtungen" |
| Nach Zeit filtern (letzte 7 Tage, Monat, Jahr) | V1 | |
| Heatmap-Ansicht | V1 | Dichte der Catches pro Gebiet |
| Eigene Catches auf Karte | MVP | |
| Catches von Freunden auf Karte | V1 | |

## Soziales

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Nutzerprofile | MVP | Benutzername, Avatar, Catch-Anzahl, Arten-Anzahl |
| Folgen / Freundschaftssystem | V1 | |
| Aktivitätsfeed (Freundes-Catches) | V1 | |
| Community-Meilensteine | Später | "Hamburg hat 100 Arten geloggt!" |
| "Erster Catch im Gebiet"-Badges | Später | Motiviert das Erkunden neuer Gebiete |

## Benachrichtigungen

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Seltener Vogel in der Nähe | V1 | "Eisvogel wurde 500m von dir gesehen" |
| Freundes-Catch-Benachrichtigung | V1 | |
| Wöchentliche Zusammenfassung | V1 | |
| Saisonale Zugvogelwarnungen | Später | |

## Gamification

| Feature | Priorität | Anmerkungen |
|---|---|---|
| XP / Level-System | V1 | Einfach, nicht kompetitiv |
| Badges / Erfolge | V1 | "Erster Catch", "10 Arten", "Im Regen gecacht" etc. |
| Catch-Streak | V1 | Wöchentlich, nicht täglich (nicht zu fordernd) |
| Kollaborative Stadtziele | Später | Keine persönlichen Rankings |

## Onboarding

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Reibungsloser Einstieg | MVP | Social Login (Apple, Google) |
| 3 Starter-Vögel Auswahl / Präsentation | MVP | Lokal, häufig, cachenswert — macht den Dex sofort greifbar |
| Tutorial für ersten Catch | MVP | Mia durch ihren ersten Catch führen |
| Standorterlaubnis mit klarem Mehrwert | MVP | "Wir zeigen dir Vögel in der Nähe" |
| Benachrichtigungserlaubnis nach erstem Catch | MVP | Nicht vorab abfragen |

## Ästhetik & Haptik

| Feature | Priorität | Anmerkungen |
|---|---|---|
| Vogel-Illustrationen (Aquarell/Gouache-Stil) | MVP | Kernidentität — für alle Artkarten, kein Stockfoto |
| Haptisches Feedback beim Catch | MVP | Vibration + Sound = das Moment fühlt sich physisch an |
| Catch-Animation ("Aufdecken" der Artenkarte) | MVP | Wie eine Sammelkarte die sich umdreht |
| Seitenübergangs-Animationen | V1 | Weich, natürlich — kein hartes Schneiden |
| Sound-Design (UI-Töne) | V1 | Subtile Vogelgeräusche als UI-Feedback |
| Splash/Ladebildschirm mit Illustration | MVP | Erster Eindruck zählt |
