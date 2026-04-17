# Decision Log

Decisions we've made, with reasoning. Update this when something changes.

---

## Product Decisions

### Collaborative over competitive
**Decision:** No leaderboards, no competitive rankings.  
**Why:** High misuse risk (fake catches to rank up). More importantly: competition alienates casual users (Mia). The nature context is inherently non-competitive — we want people to help each other find birds, not beat each other.  
**Trade-off:** Less engagement from hyper-competitive users — accepted.

### Public catches by default
**Decision:** Catches are public by default (can be set to friends/private).  
**Why:** Community map only works if there's data. Public default maximises map density from day 1. Privacy options available for sensitive sightings (rare birds that could attract crowds and disturb nesting).

### Weekly streak, not daily
**Decision:** Streak is measured weekly ("catch at least once this week"), not daily.  
**Why:** Daily streaks create anxiety and churn. Birdwatching is a weekend/leisure activity. We want to encourage going outside more, not punish for missing a Tuesday.

### Sound ID before Photo ID in MVP
**Decision:** Prioritize sound identification for V1 over photo ID.  
**Why:** Sound is the "Merlin hook" — it works passively (you don't need to see the bird). Many birds are heard before seen. This is the highest-value, lowest-friction ID method for beginners.

---

## Technical Decisions

### Expo (React Native) for mobile
**Decision:** Expo over Flutter, native iOS/Android, or web-only PWA.  
**Why:** Cross-platform (iOS + Android from one codebase). Expo SDK has camera, microphone, location APIs built in. TypeScript support. Large ecosystem, good LLM training data = better agentic coding.  
**Trade-off:** Slightly less performance than native. Acceptable for this use case.

### Supabase as backend
**Decision:** Supabase over custom Node.js backend, Firebase, or PocketBase.  
**Why:** PostGIS built in = spatial queries for map/heatmap with no extra setup. Realtime subscriptions for social feed. Auth with social providers out of the box. Storage for catch photos. Row Level Security for privacy. Strong docs = good agentic coding target.  
**Trade-off:** Less control than custom backend. Vendor lock-in risk. Acceptable at this stage.

### Mapbox over Google Maps / Leaflet
**Decision:** Mapbox GL JS / react-native-mapbox-gl.  
**Why:** Heatmap layers, custom styling (can achieve Pokemon-like aesthetic), clustering built in. Performance better than Leaflet for large datasets.  
**Trade-off:** Paid above free tier. Worth it for map quality.

---

## Open Questions

- [ ] Bird species database: build our own seeded from eBird taxonomy, or use an API? (xeno-canto for audio, eBird for taxonomy)
- [ ] Sound ID: BirdNET API (free, Cornell) vs building on top of Merlin SDK (if available) vs own model?
- [ ] Monetization model? (currently: not a priority, but affects some design decisions)
- [ ] Geography focus: Hamburg / Germany only for MVP, or global from day 1?
