# Screens

Navigation structure: **Bottom Tab Bar** with 4 tabs.

---

## Tab 1: Map

**Primary entry point for exploration.**

- Full-screen map (Mapbox)
- Catch pins / clusters visible
- Filter bar: species, time range, friends-only toggle
- Heatmap toggle
- Floating "Catch" button (primary CTA, always visible)
- Tap pin → mini card (species, user, time, distance)
- Mini card → expands to Catch Detail

---

## Tab 2: Catch (Action)

**The main action — triggered from FAB or tab.**

Flow (screens within this tab):
1. **Catch Method Selection** — Heard it? Saw it? Want to use sound ID or photo ID?
2. **Sound ID Screen** — Live listening, waveform animation, species result
3. **Photo ID Screen** — Camera viewfinder, capture, species result
4. **Manual Search Screen** — Search bar, species list
5. **Catch Confirmation Screen** — Species confirmed, select method, optional note/photo, location preview
6. **Catch Success Screen** — Animation + reward + "Share" option

---

## Tab 3: Collection

**My birds — the Pokédex.**

- Grid of caught species (greyed out for not-yet-caught, shown in region)
- Sort: recently caught / alphabetical / rarity
- Filter: family, season, rarity
- Tap species → **Species Detail Screen**
  - Photo, name, description, song player
  - My catches of this species (where/when)
  - Community catches (how many people caught it, where)
  - "Catch again" button

---

## Tab 4: Profile & Social

**Me + my friends.**

Screens:
- **My Profile** — avatar, username, level/XP bar, badges, stats (species count, catch count, streak)
- **My Badges** — grid of earned and locked badges
- **Activity Feed** — friend catches chronologically
- **Friends List** — with their recent activity
- **Friend Profile** — their public collection + recent catches
- **Settings** — notification prefs, privacy, account

---

## Global / Overlay Screens

| Screen | Trigger |
|---|---|
| Onboarding (3 slides) | First launch |
| First Catch Tutorial | After first sound ID result |
| Catch Detail (modal) | Tap any catch pin on map |
| Rare Bird Alert (push) | Notification tap → map with highlighted pin |
| Species Quick Card (sheet) | Tap species anywhere in app |

---

## Design Notes

- Bottom tab bar always visible (except during sound/photo ID — full screen)
- Catch button (mic icon) could be persistent FAB over the map tab
- Dark mode support from day 1 (outdoors at dusk/dawn)
- Large tap targets — used with one hand outdoors
- Minimal text input — tap > type wherever possible
