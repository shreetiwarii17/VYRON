# VYRON — Accessibility, resolved by AI

**by Team कृत्रिम** · A high-fidelity fullstack prototype of an AI-driven web accessibility engine that doesn't just report problems — it writes the actual code fixes.

![Stack](https://img.shields.io/badge/Next.js-16-black) ![React](https://img.shields.io/badge/React-19-149eca) ![Tailwind](https://img.shields.io/badge/Tailwind-4-38bdf8) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Drizzle-336791)

---

## ✨ Features

- **Command Center** — massive URL input, four curated Demo Worlds, and a Paste Code editor
- **Scanning sequence** — live code-streaming animation through 5 analysis stages
- **Intelligence Dashboard** — animated accessibility score ring, scan summary panel, severity groups (Critical / Serious / Moderate), search + filters, **Split view** and **Issues grid**
- **Sandboxed DOM preview** — hover any issue to highlight the exact offending element
- **Magic Diff view** — red/green side-by-side before/after code with a "Generating Fix..." shimmer
- **AI Insights** — 2-sentence explanations in **English + हिन्दी** for every fix
- **Resolution export** — one-click copy patch (real unified diff), download `.patch`, patched HTML, and a full **PDF report (EN / हिन्दी)**
- **Rescan, undo, and persistent scan history** stored in PostgreSQL
- **Four atmospheres** — Sunset Velvet · Daylight Studio · Cosmic Aura · Cyber Matrix
- **Real audit engine** — 11 WCAG 2.2 rule families (alt text, accessible names, labels, measured contrast ratios, heading order, lang, tabindex, focus, zoom, title) with exact source-offset edits

## 🧱 Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 16 (App Router, Turbopack) |
| UI | React 19, Tailwind CSS 4, Lucide icons, Framer Motion |
| Fonts | Inter Variable + JetBrains Mono Variable (self-hosted via Fontsource) |
| Database | PostgreSQL + Drizzle ORM |
| Exports | `diff` (unified patches), `jspdf` (PDF, Devanagari rendered via canvas) |

## 🚀 Getting started

```bash
# 1. Install dependencies
npm install

# 2. Configure environment
cp .env.example .env
# edit DATABASE_URL to point at your PostgreSQL instance

# 3. Create the database schema
npx drizzle-kit push

# 4. Run
npm run dev        # development
npm run build && npm start   # production
```

Requires Node.js 20+ and a PostgreSQL database.

## 🗂 Project structure

```
src/
├── app/
│   ├── page.tsx / layout.tsx / globals.css   # SPA shell + design system (4 atmospheres)
│   └── api/
│       ├── health/route.ts                   # DB healthcheck
│       └── scans/route.ts, scans/[id]/route.ts  # create / list / load / resolve
├── components/
│   ├── vyron-app.tsx          # app controller (phases, toasts, persistence)
│   ├── top-bar.tsx            # branding, progress pipeline, atmosphere switcher
│   ├── command-center.tsx     # URL / Demo Worlds / Paste code input
│   ├── scanning-sequence.tsx  # code-streaming scan animation
│   ├── dashboard.tsx          # score, summary, queue, split/grid layouts
│   ├── score-ring.tsx         # animated accessibility score
│   ├── site-preview.tsx       # sandboxed DOM with issue highlighting
│   ├── issue-card.tsx         # violation card + Auto-Resolve button
│   ├── diff-modal.tsx         # shimmer → diff → apply → success export
│   ├── report-modal.tsx       # bilingual report + patch/HTML/PDF export
│   └── history-drawer.tsx     # persistent scan history
├── lib/
│   ├── accessibility/         # engine, types, patch builder, PDF + report copy
│   ├── demo-worlds.ts         # 4 curated HTML demo sites
│   └── atmospheres.ts         # theme definitions
├── server/scan-records.ts     # row → API serialization
└── db/                        # Drizzle client + scans schema
```

## 🔍 How the audit works

- **Demo Worlds / Paste code** → deterministic source-level analysis; every finding carries exact edit offsets, so resolving it produces a real applicable patch.
- **Live URL** → server-side fetch (public HTTP(S) only, private networks blocked, 7s timeout). If retrieval fails, VYRON clearly labels the result as a **simulated snapshot** — never presented as real page evidence.
- Scoring is severity-weighted (critical 12, serious 7, moderate 4) and recalculated server-side on every apply/undo.

## 📄 License

Prototype — add your preferred license before publishing.
