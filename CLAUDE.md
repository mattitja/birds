# Birds App — Agent Context

This is a bird discovery app — "Pokémon for birds". The goal is to get people into nature by lowering the barrier to birdwatching through gamification, social features, and collaborative mapping.

## How to use this repo as an agent

Before writing any code, read the relevant product docs in `product/`:

| Task | Read first |
|---|---|
| New feature | `product/features.md` + `product/user_journeys.md` |
| New screen / UI | `product/screens.md` + `product/personas.md` |
| DB schema / migration | `product/data_model.md` |
| API endpoint | `product/data_model.md` + `product/user_journeys.md` |
| Any architectural decision | `product/decisions.md` |

## Core principle

The app must work for someone who has never thought about birds before. Every feature must be evaluated against "Casual Mia" (see `product/personas.md`) — if she would be confused or bored, the feature needs to be simpler or more rewarding.

## Stack (decided)

> See `product/decisions.md` for rationale.

- **Mobile**: Expo (React Native) + TypeScript
- **Backend**: Supabase (PostGIS, Realtime, Auth, Storage)
- **Maps**: Mapbox GL
- **Styling**: NativeWind (Tailwind for RN)

## North Star Metric

Number of people who catch their first bird within 10 minutes of installing the app.
