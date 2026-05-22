# FallConcierge

**Sovereign AI concierge with real-time psychological profiling.**

One HTML file. Claude API. Jungian archetypes. Freudian shadow reading. Adaptive sales intelligence. Zero server. Zero dependencies.

---

## What It Does

FallConcierge is an AI-powered conversational interface that psychologically profiles visitors in real-time and adapts its communication style to match who it's talking to. It doesn't just answer questions — it reads the person behind the question.

**The concierge detects:**
- Which of 10 Jungian archetypes the visitor maps to
- Their Freudian shadow profile (what they say vs what they mean)
- Industry, team size, pain points, tool stack
- Buying readiness on a 0-10 scale
- Name and email when naturally shared

**Then it adapts:**
- Tone calibration across 5 dimensions (formality, confidence, warmth, directness, humor)
- Sales framework selection (SPIN, Challenger, PAS, AIDA)
- Word choice and phrasing style
- Conversation strategy

---

## Architecture

```
Visitor Message
     |
     v
+------------------+
|  PSYCHOLOGY      |  Client-side JS — no API call needed
|  ENGINE          |
|                  |
|  Archetype:      |  10 Jungian archetypes scored via
|  - trigger words |  role matching (+50), trigger words (+10),
|  - role matching |  repulsion signals (-5)
|  - tone scoring  |
|                  |
|  Shadow:         |  8 Freudian role profiles
|  - what they say |  what_they_say vs what_they_mean
|  - what they mean|  fear, hidden_objection, need
|                  |
|  Readiness:      |  0-10 composite score
|  - engagement    |  messages, signals, industry,
|  - qualification |  team, tools, pain points
+------------------+
     |
     v  [PSYCHOLOGY CONTEXT] injected into system prompt
     |
+------------------+
|  CLAUDE API      |  Anthropic Claude Sonnet
|  (adaptive)      |
|                  |
|  System prompt   |  Base persona + archetype adaptation
|  adapts per      |  rules + shadow reading rules +
|  visitor profile |  sales framework selection
+------------------+
     |
     v
  Adapted Response
  (tone, framework, word choice all calibrated)
```

---

## The 10 Archetypes

| Archetype | Detects | Adapts To |
|-----------|---------|-----------|
| **RULER** | CEO, CFO, Director, "control", "governance" | Authoritative, data-driven, short sentences |
| **SAGE** | CTO, Analyst, Researcher, "evidence", "methodology" | Evidence-based, depth, let them conclude |
| **HERO** | Founder, Growth, VP, "challenge", "ship", "launch" | Bold, direct, frame as worthy battle |
| **CREATOR** | Designer, UX, Brand, "craft", "elegant", "bespoke" | Visionary, appreciate craft, show possibility |
| **EXPLORER** | PM, Indie Hacker, "discover", "frontier", "curious" | Energetic, unconventional, show discovery |
| **CAREGIVER** | HR, Support, Community, "team", "help", "protect" | Warm, empathetic, people over metrics |
| **MAGICIAN** | Strategy, Architecture, "transform", "system" | Systems thinking, connect dots, show shift |
| **REBEL** | Disruptor, Hacker, "break", "disrupt", "kill" | Provocative, challenge status quo, arm them |
| **EVERYPERSON** | SMB, Freelancer, "simple", "practical", "affordable" | Plain language, real examples, low barrier |
| **INNOCENT** | Risk-averse, Procurement, "safe", "proven", "guarantee" | Reassuring, remove anxiety, social proof |

---

## The Freudian Shadow Layer

For 8 common roles, the engine reads the gap between what visitors **say** and what they **mean**:

| Role | They Say | They Mean | They Fear | They Need |
|------|----------|-----------|-----------|-----------|
| CEO | "Data-driven decisions" | Validation of instinct | Looking foolish to board | Peer adoption proof |
| CTO | "Enterprise reliability" | Something exciting | Bad engineering behind marketing | Open source transparency |
| Founder | "Enterprise features" | Ship by Friday | Running out of runway | Free tier that scales |
| Developer | "Comprehensive docs" | Copy-paste and it works | Breaks at 3am | Uptime stats |
| Marketer | "Measurable ROI" | Creative recognition | Brand sounding generic | Voice customisation |
| Sales | "Build relationships" | Shortcut to quota | Looking like using AI | Indistinguishable output |
| Finance | "Innovation" | Avoid blame if fails | Signing off on disaster | No-risk pilot |
| SMB Owner | "Grow the business" | Stop drowning in admin | Money on dust | Immediate visible result |

---

## Sales Framework Selection

The concierge selects the optimal sales methodology based on detected archetype:

| Visitor Type | Framework | Approach |
|---|---|---|
| Sage / CTO | **SPIN** (Rackham) | Situation → Problem → Implication → Need-payoff |
| Rebel / Hero | **Challenger** (Dixon & Adamson) | Teach → Tailor → Take Control |
| Quick exchanges | **PAS** (Direct response) | Problem → Agitate → Solve |
| General visitors | **AIDA** (Lewis) | Attention → Interest → Desire → Action |

---

## How It Was Built

This concierge is the product of several interlocking systems built over 18 months:

### Source Frameworks

1. **Trilogy Forge** (`trilogy-forge/src/archetypes.js`) — The 12 Jungian archetype system with scored detection logic. Each archetype has roles, trigger words, repulsion signals, and pre-calibrated 16-dimension tone profiles.

2. **Trilogy Forge Shadow Engine** (`trilogy-forge/src/shadow.js`) — 8 Freudian role profiles mapping Id (what they secretly want), Ego (what they say they want), Superego (what they think they should want), and the shadow gap between them.

3. **Trilogy Forge ToneEngine** (`trilogy-forge/src/tone.js`) — 16-dimension voice fingerprinting: formality, confidence, warmth, complexity, pace, authority, emotion, directness, humor, urgency, exclusivity, technicality, aspiration, vulnerability, provocation, storytelling. Each dimension calibrated 0.0-1.0 with archetype-specific presets.

4. **Trilogy Forge Sales Engine** (`trilogy-forge/src/sales.js`) — 4 structural frameworks (SPIN, Challenger, PAS, AIDA) with 7 Cialdini-based psychological triggers (scarcity, social proof, authority, reciprocity, loss aversion, anchoring, commitment).

5. **ToneSmith** (`tonesmith/tonesmith.html`) — 12-tone text analyser with marker word lists for tone detection (formal, casual, technical, persuasive, empathetic, authoritative, witty, narrative, urgent, academic, minimalist, lyrical).

6. **FallScout Psyche Engine** (`fallscout/server.js`) — Full-stack prospect profiling combining all 4 frameworks for LinkedIn intelligence. Generates 3 DM strategies per prospect (Archetype Play, Gap Reveal, Ego Mirror) with sniper rules: mirror voice, activate archetype, enter through emotion, bridge with logic, avoid defences, under 100 words, low-friction ask.

### What I Did

- Extracted the core psychological models from Trilogy Forge (archetypes, shadow, tone, sales)
- Compressed the 16-dimension ToneEngine into 5 key dimensions that drive conversational adaptation
- Built client-side archetype detection using trigger word scoring, role matching, and repulsion signals
- Implemented Freudian shadow profiling for 8 common visitor roles
- Created a readiness scoring system (0-10) combining engagement, qualification, and buying signals
- Wired the psychology layer to inject real-time context into Claude's system prompt
- Built the concierge as a sovereign single-file HTML app with IndexedDB persistence
- Integrated into the AI Native Solutions hub site as the primary visitor interface
- Added Claude API key management via localStorage (sovereign — never leaves browser)

### The Key Insight

Most chatbots treat every visitor the same. The concierge treats every visitor as a specific psychological type and adapts everything — tone, framework, word choice, strategy — in real-time. A CEO gets authority and certainty. A developer gets technical depth and transparency. A founder gets speed and challenge. Same AI, same product knowledge, completely different conversation.

---

## Setup

1. Open `index.html` in a browser
2. Click the API Key button
3. Paste your Claude API key (`sk-ant-...`)
4. Start talking

The key is stored in `localStorage` — never leaves your browser.

---

## Customisation

### Replace the System Prompt

Edit the `SYSTEM_PROMPT` constant in the `<script>` section. This controls the concierge's persona, knowledge base, and response style. The psychology layer feeds data into it via `[PSYCHOLOGY CONTEXT]` blocks — keep that integration point.

### Add Industry Knowledge

Add entries to `industryPatterns` in the `Psych` module to detect more industries.

### Add Shadow Profiles

Add entries to `shadowProfiles` for more role-specific what-they-say vs what-they-mean mappings.

### Embed in Another Site

The concierge can be embedded via iframe or the psychology engine can be extracted and wired into any existing chat interface.

---

## Sovereign Principles

- **One HTML file** — no build step, no dependencies, no framework
- **Data in IndexedDB** — conversations stored on device, never transmitted
- **API key in localStorage** — your key, your browser, your data
- **No tracking** — zero analytics, zero telemetry
- **Claude API only** — direct to Anthropic, no proxy, no middleware

---

## Stack

- Vanilla JavaScript (no framework)
- Claude API (Anthropic)
- IndexedDB (conversation persistence)
- localStorage (API key storage)

---

## Part of the AI Native Solutions Ecosystem

FallConcierge is node `prime=139` in the [FallMesh](https://sjgant80-hub.github.io/fallmesh/) sovereign mesh protocol.

Connected to:
- [Trilogy Forge](https://sjgant80-hub.github.io/trilogy-forge/) — psychological build engine (source of archetypes, shadow, tone, sales frameworks)
- [FallScout](https://sjgant80-hub.github.io/fallscout/) — LinkedIn intelligence with Psyche Engine
- [ToneSmith](https://github.com/sjgant80-hub/tonesmith) — open-source tone analysis
- [AI Native Solutions](https://sjgant80-hub.github.io/ai-nativesolutions/) — hub site where the concierge runs live

---

## License

MIT
