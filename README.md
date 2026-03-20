#  GigShield — AI-Powered Parametric Income Insurance for Food Delivery Partners

> **Guidewire DEVTrails 2026** | University Hackathon  
> **Persona:** Food Delivery Partners (Zomato / Swiggy)  
> **Platform:** Web Application  
> **Stack:** React + Node.js

---

##  Problem Statement

India's food delivery partners (Zomato, Swiggy) earn ₹15,000–₹25,000/month but lose **20–30% of income** during external disruptions — heavy rain, extreme heat, floods, local curfews, or platform outages. They have **no financial safety net**.

**GigShield** is a parametric income insurance platform that automatically detects disruptions, triggers claims without paperwork, and pays out lost wages instantly — all within a weekly pricing model that matches a gig worker's earnings cycle.

---

##  Persona: The Zomato/Swiggy Delivery Partner

### User Profile
| Attribute | Detail |
|-----------|--------|
| Age | 20–35 years |
| Monthly Income | ₹15,000 – ₹25,000 |
| Working Hours | 8–12 hrs/day, 6–7 days/week |
| Primary Zones | Urban/semi-urban (Hyderabad, Mumbai, Bengaluru, Delhi) |
| Tech Comfort | Moderate — uses smartphones daily |
| Pain Point | No income during rain, floods, curfews, or app blackouts |

### Real Persona Scenario

**Meet Ravi, 27, Swiggy delivery partner in Hyderabad:**
- Earns ~₹800/day on a good day
- During the 2024 Hyderabad floods, he couldn't work for 4 days → lost ₹3,200 with zero compensation
- Has no savings cushion; skipped meals and delayed rent
- Doesn't trust complex insurance products — needs something simple, transparent, and automatic

---

##  Application Workflow

```
┌─────────────────────────────────────────────────────────────┐
│                    GIGSHIELD WORKFLOW                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. ONBOARDING       2. RISK PROFILING   3. POLICY          │
│  ─────────────       ───────────────     ──────────         │
│  • Phone + OTP       • Work zone input   • Weekly plan      │
│  • Platform link     • AI risk score     • ₹29–₹79/week     │
│  • Income proof      • Zone history      • Coverage: 60%    │
│    (mock)            • Weather data        of avg daily      │
│                                            earnings          │
│                                                             │
│  4. MONITORING       5. AUTO TRIGGER     6. PAYOUT          │
│  ─────────────       ─────────────────   ───────            │
│  • Weather API       • Threshold met     • UPI instant      │
│  • AQI API           • Claim created     • ₹480–₹800/day    │
│  • Curfew feeds      • Zero paperwork    • SMS + App alert  │
│  • Platform API      • Fraud check       • Weekly summary   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

##  Weekly Premium Model

### Why Weekly?
Food delivery partners receive earnings weekly from Zomato/Swiggy. Aligning insurance premiums with the payout cycle reduces friction and increases adoption.

### Pricing Tiers

| Plan | Weekly Premium | Coverage/Day | Max Days/Week | Best For |
|------|---------------|-------------|--------------|---------|
| **Basic Shield** | ₹29/week | ₹480 | 3 days | New/part-time partners |
| **Pro Shield** | ₹49/week | ₹640 | 5 days | Full-time partners |
| **Max Shield** | ₹79/week | ₹800 | 6 days | High-earning partners |

### Dynamic Pricing Logic (AI/ML)
The base weekly premium is adjusted dynamically using:

```
Weekly Premium = Base Rate × Zone Risk Multiplier × Season Factor × Claim History Factor

Where:
- Zone Risk Multiplier: 0.85 (flood-safe zone) → 1.25 (flood-prone zone)
- Season Factor: 1.0 (dry) → 1.4 (monsoon peak)
- Claim History Factor: 0.9 (no claims) → 1.2 (frequent claims)
```

**Example:** Ravi in Kukatpally (moderate flood risk), monsoon season, no prior claims:
`₹49 × 1.10 × 1.30 × 0.90 = ₹62.92/week → rounded to ₹63/week`

---

##  Parametric Triggers

Claims are triggered **automatically** when measurable thresholds are crossed — no manual filing required.

| Trigger | Data Source | Threshold | Payout |
|---------|------------|-----------|--------|
| Heavy Rain | OpenWeatherMap API | Rainfall > 50mm/hr OR Red Alert issued | Full day coverage |
| Extreme Heat | OpenWeatherMap API | Temperature > 43°C for 3+ hrs | 50% day coverage |
| Severe AQI | CPCB / AQI API | AQI > 400 (Hazardous) | Full day coverage |
| Flood/Waterlogging | IMD + Zone mapping | Flood zone active alert | Full day coverage |
| Curfew / Strike | News API + manual admin | Official order detected | Full day coverage |
| Platform Outage | Zomato/Swiggy mock API | >2hr platform downtime | 50% day coverage |

---

##  AI/ML Integration Plan

### 1. Dynamic Premium Calculation
- **Model:** Gradient Boosted Trees (XGBoost)
- **Inputs:** Worker's zone, historical weather data, claim frequency, season, delivery density
- **Output:** Personalized weekly premium
- **Training Data:** Mock historical weather + claim datasets

### 2. Fraud Detection
- **Anomaly Detection:** Isolation Forest algorithm
- **Checks:**
  - GPS location vs. claimed disruption zone
  - Claim timing vs. actual weather event window
  - Duplicate claims across same zone/same worker
  - Unusual claim patterns (e.g., claims every single trigger day)
- **Flag Mechanism:** Claims above fraud score 0.75 → manual review queue

### 3. Risk Zone Mapping
- **Model:** Clustering (K-Means) on historical flood/waterlogging data per pin code
- **Output:** Zone risk tier (Low / Medium / High / Very High)
- **Update Frequency:** Weekly re-scoring

### 4. Predictive Disruption Alerts
- **Model:** Time-series forecasting (Prophet/ARIMA) on 5-year weather data
- **Use:** Notify workers 24hrs before predicted disruption — they can activate coverage proactively

---

## Tech Stack

### Frontend
| Layer | Technology |
|-------|-----------|
| Framework | React 18 + Vite |
| UI Library | Tailwind CSS + shadcn/ui |
| State Management | Zustand |
| Charts/Analytics | Recharts |
| Maps | Leaflet.js |

### Backend
| Layer | Technology |
|-------|-----------|
| Runtime | Node.js + Express.js |
| Database | PostgreSQL (primary) + Redis (caching) |
| Auth | JWT + OTP via Twilio (mock) |
| ML Service | Python FastAPI microservice (sklearn/XGBoost) |
| Queue | Bull (Redis-based job queue for payouts) |

### External APIs & Integrations
| Service | Purpose | Mode |
|---------|---------|------|
| OpenWeatherMap | Weather triggers | Free tier |
| CPCB AQI API | Pollution triggers | Free tier |
| News API | Curfew/strike detection | Mock |
| Razorpay | Payout processing | Sandbox/test mode |
| Twilio | SMS notifications | Trial |
| Zomato/Swiggy | Income verification | Simulated mock |

### Infrastructure
- **Hosting:** AWS EC2 / Render (for demo)
- **CI/CD:** GitHub Actions
- **Containerization:** Docker Compose

---

## Repository Structure

```
gigshield/
├── client/                  # React frontend
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Onboarding/  # Worker registration
│   │   │   ├── Dashboard/   # Worker dashboard
│   │   │   ├── Policy/      # Policy management
│   │   │   ├── Claims/      # Claims tracking
│   │   │   └── Admin/       # Insurer analytics
│   │   ├── components/
│   │   └── hooks/
├── server/                  # Node.js + Express API
│   ├── routes/
│   │   ├── auth.js
│   │   ├── policy.js
│   │   ├── claims.js
│   │   ├── triggers.js
│   │   └── payouts.js
│   ├── services/
│   │   ├── weatherService.js
│   │   ├── fraudService.js
│   │   └── payoutService.js
│   └── jobs/                # Scheduled trigger monitoring
├── ml-service/              # Python FastAPI ML microservice
│   ├── premium_model.py
│   ├── fraud_model.py
│   └── risk_zones.py
├── mock-data/               # Simulated APIs and datasets
└── docker-compose.yml
```

---

## 🗓️ Development Plan

### Phase 1 (March 4–20) —  Ideation & Foundation
- [x] Persona research & scenario definition
- [x] Weekly pricing model design
- [x] Parametric trigger definitions
- [x] Tech stack finalization
- [x] Repository setup & README

### Phase 2 (March 21 – April 4) — Automation & Protection
- [ ] Worker registration + OTP onboarding flow
- [ ] Policy creation UI with dynamic premium display
- [ ] 3–5 automated parametric triggers (Weather, AQI, Curfew)
- [ ] Claims management module (zero-touch flow)
- [ ] ML premium calculation service (mock model)

### Phase 3 (April 5–17) — Scale & Optimise
- [ ] Fraud detection engine (Isolation Forest)
- [ ] Razorpay sandbox payout integration
- [ ] Worker dashboard (earnings protected, weekly coverage)
- [ ] Admin/insurer dashboard (loss ratios, predictive analytics)
- [ ] Final pitch deck + 5-minute demo video

---

##  Key Differentiators

1. **Zero-Touch Claims** — No forms, no calls. Disruption detected → claim auto-filed → payout in <2 hrs
2. **Hyper-Local Risk Scoring** — Premium varies by pin code, not just city
3. **Monsoon-Aware Pricing** — ML model adjusts premiums weekly based on IMD forecasts
4. **Vernacular UX** — Hindi/Telugu language support for low-literacy workers
5. **WhatsApp Integration (Phase 3)** — Workers can check coverage and receive alerts via WhatsApp



##  Links

-  **Phase 1 Video:** [https://youtu.be/cFEerA3mJrI?si=t5UlyaBos2Wj9dW6]
-  **Prototype:** [prototype/gigshield.html]

---

*Built with  for India's gig economy | Guidewire DEVTrails 2026*
