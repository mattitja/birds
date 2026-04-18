# Recherche: Vogelton-Erkennung

## BirdNET-Analyzer (Open Source, Cornell Lab / Stefan Kahl)
GitHub: https://github.com/kahst/BirdNET-Analyzer  
Doku: https://birdnet-team.github.io/BirdNET-Analyzer/

**Technische Parameter:**
- Snippet-Länge: fix **3 Sekunden** pro Analyse-Einheit
- Sample Rate: 48 kHz (internes Resampling, egal was rein kommt)
- Overlap: 0–2.9s einstellbar → Sliding Window möglich (z.B. alle 1s neues 3s-Fenster)
- Confidence: Float 0–1, Default-Threshold 0.25, frei einstellbar
- Multi-Vogel: **Ja** — pro 3s-Snippet mehrere Erkennungen mit je eigenem Score
- Frequenzbereich: 0–15.000 Hz, einstellbar
- Arten: **6512 global**, alle relevanten DE/EU-Arten enthalten

**Betriebsmodi:**
- File-basiert (Batch) — primärer Use Case
- Server-Modus — single-threaded, JSON-Response, für 1–10s Clips designed
- Streaming/Real-Time: **nicht nativ** — aber Buffer-basiertes Chunking möglich
- **Offline: Ja** — Modell läuft lokal, kein Internet nötig

**Lizenz:** Open Source (MIT-ähnlich), kostenlos für non-commercial

**birdnetlib** (Python-Wrapper): https://github.com/joeweiss/birdnetlib  
Vereinfachte API, `RecordingBuffer`-Klasse deutet auf Chunk-basierte Analyse hin — kein echter Streaming-Mode, aber sliding window über Buffer implementierbar.

---

## BirdNET-Tiny / BirdNET-Tiny Forge
GitHub: https://github.com/birdnet-team/BirdNET-Tiny-Forge  

- Speziell für **Microcontroller / Edge-Geräte** entwickelt
- Kollaboration Cornell + fold ecosystemics
- Ziel: kompaktes Modell für Deployment auf ressourcenarmer Hardware
- Modell-Format unklar (vermutlich TFLite), Details nicht öffentlich gut dokumentiert
- Könnte der Weg zu **On-Device-Inference auf dem Smartphone** sein — noch zu validieren

---

## BirdWeather
Website: https://app.birdweather.com  

Kein eigenständiger Sound-ID-Service. BirdWeather ist eine **Datenplattform**:
- Du analysierst selbst (mit BirdNET oder kompatiblem Tool)
- Pushst Ergebnisse via API an BirdWeather
- BirdWeather visualisiert und aggregiert Community-Daten
→ Für uns nicht als ID-Service relevant, aber interessant als Referenz für Community-Daten-Architektur.

---

## Keine öffentliche Cornell BirdNET REST-API gefunden
Es gibt kein öffentliches "BirdNET-as-a-Service" API von Cornell. Alles läuft über das Open-Source-Tool (selbst hosten oder on-device).

---

## Technische Weggabelung: On-Device vs. Self-Hosted Server

### Option A: On-Device (TFLite auf dem Smartphone)
- Modell läuft direkt auf dem Gerät → **offline-fähig**
- Merlin macht das vermutlich so (erklärt Offline-Support)
- BirdNET-Tiny wäre der Weg dafür
- Vorteil: kein Netz im Wald nötig, keine Latenz durch Netzwerk, keine Server-Kosten, kein Datenschutz-Problem
- Risiko: Modellgröße vs. Genauigkeit, Akku-Impact durch CPU/GPU-Last on-device
- Expo/React Native: TFLite via `react-native-fast-tflite` oder `@tensorflow/tfjs-react-native` möglich

### Option B: Selbst gehosteter Server (BirdNET-Analyzer auf VPS/Cloud)
- Vollständiges BirdNET-Modell, höchste Genauigkeit
- App streamt Audio-Chunks an eigenen Server → Analyse → Ergebnis zurück
- Vorteil: volle Kontrolle über Modell, Updates ohne App-Update, kein Akku-Impact
- Nachteil: Internet-Pflicht (kein Empfang im Wald), Latenz (~1–3s), Server-Kosten, Privacy (Audio geht ans Netz)
- Sliding Window: alle ~1s einen 3s-Chunk senden, Server antwortet mit JSON

### Option C: Fremde API
- Keine öffentliche BirdNET-API gefunden
- BirdWeather kein ID-Service
- Keine relevante Alternative entdeckt
→ **Option C fällt de facto weg.**

---

## Merlin-ähnliches Sliding Window — wie es technisch aussieht

```
Mikrofon → Audio-Puffer
→ alle ~1s: neues 3s-Chunk (mit 2s Overlap zum vorherigen)
→ BirdNET-Analyse (on-device oder server)
→ Ergebnisse: [(Art, Confidence), ...] pro Chunk
→ UI: aktuell singender Vogel = Art mit höchstem Score im letzten Chunk
```

Ergebnis kommt ~1–3s zeitversetzt (je nach Inferenz-Ort). Für "letzter singende Vogel" reicht das.

---

## On-Device TFLite in React Native — Details

### react-native-fast-tflite (Marc Rousavy)
- Gold Standard für TFLite in React Native
- GPU-Beschleunigung: Metal (iOS), NNAPI/Vulkan (Android)
- Inferenz-Zeit: **< 50ms** auf modernem Smartphone
- Direkte Tensor-Übergabe ohne JS-Serialisierungs-Overhead

### Das Tensor-Problem
BirdNET erwartet einen rohen Float32Array mit **144.000 Werten** (3s × 48.000 Hz).  
Problem: `expo-av` liefert komprimierte `.m4a`-Dateien — kein direkter Zugriff auf PCM-Samples.

**Lösung:** `react-native-live-audio-stream`
- Liefert rohe PCM-Daten als Base64-Chunks direkt vom Mikrofon
- Kein Dateisystem-Umweg, kein Codec-Overhead

### Vollständige On-Device-Pipeline
```
Mikrofon
  → react-native-live-audio-stream (PCM Base64-Chunks)
  → JS: Base64 → Float32Array
  → Sliding Window: alle ~1s ein neues 3s-Fenster zusammenstellen
  → react-native-fast-tflite: Float32Array → BirdNET TFLite-Modell
  → Ergebnis: [(Art, Confidence), ...] pro Chunk
  → UI-Update
```

### Native Bridging — der Knackpunkt
Für eine produktionsreife Pipeline (Audio-Buffer → Tensor) ist nativer Code nötig:
- **iOS:** Swift oder C++ (AVAudioEngine → Float32 direkt)
- **Android:** Kotlin oder C++ (AudioRecord → FloatBuffer)
- **JSI-Bridge:** C++ Modul für Zero-Copy-Tensor-Übergabe an fast-tflite

Das ist die Stelle, wo Vibe-Coding an Grenzen stößt — kein LLM-Output ersetzt das Verständnis der nativen Audio-APIs und Memory-Layouts.

### Phasen-Strategie
**Phase 1 — Server (ein Nachmittag):**
- App streamt 3s-Chunks via HTTP an selbst gehosteten BirdNET-Analyzer
- Kein nativer Code, kein TFLite, kein Bridging
- Validiert: UI-Flow, Sliding Window, Confidence-Anzeige, Alert-Logik
- Offline-Problem bewusst akzeptiert

**Phase 2 — On-Device TFLite (~2–3 Wochen):**
- BirdNET TFLite-Modell ins App-Bundle
- Native Audio-Bridge (Swift/Kotlin) für PCM-Stream
- react-native-fast-tflite für Inferenz
- Server-Endpunkt bleibt als Fallback (schlechte Hardware / ältere Geräte)
- Offline-fähig, keine Latenz durch Netzwerk, kein Datenschutz-Problem

---

## Noch offen / zu validieren
- [ ] BirdNET-Tiny: Gibt es ein fertiges TFLite-Modell? Genauigkeit vs. Full-Model?
- [ ] On-Device Inferenz in React Native/Expo: Prototyp nötig um Akku-Impact + Latenz zu messen
- [ ] iOS Background Audio + kontinuierliche Inferenz: App-Store-Konformität testen (→ auch in risks.md)
- [ ] BirdCLEF-Gewinner-Architekturen (Kaggle) falls später eigenes Modell: meist EfficientNet/CNN auf Mel-Spektrogramm
- [ ] Trainingsdaten falls eigenes Modell: xeno-canto (CC-lizenziert), BirdCLEF-Datasets (Kaggle)

---

## Empfehlung für jetzt

**Self-Hosted BirdNET-Analyzer auf einem kleinen VPS** (z.B. Hetzner CX22, ~4€/Monat):
- Schnellste Time-to-Working-Prototype
- Volle Kontrolle über Snippet-Länge, Overlap, Threshold, Frequenzbereich
- Sliding Window implementierbar (App schickt alle 1s einen 3s-Chunk)
- Kann später durch On-Device-Modell ersetzt werden ohne App-Logik zu ändern
- Offline-Problem bewusst akzeptieren für MVP, On-Device als spätere Iteration

Langfristig (wenn du dich reinnerdest): eigenes Modell auf Basis von xeno-canto + BirdCLEF-Daten, on-device deployed via TFLite.
