# 🕌 Aazan — Learn Anything by Teaching It

> *"The best way to learn is to teach."* — Richard Feynman
>
> Aazan makes that insight into a product. Teach an AI student named **Bodhi** — and learn more deeply in the process.

---

## 🧠 The Problem

Passive learning is broken.

- Reading a textbook? **~10% retention.**
- Watching a tutorial? **~20% retention.**
- Teaching someone else? **~90% retention.**

The "Protégé Effect" is well-documented in cognitive science — explaining a concept forces your brain to identify gaps, restructure knowledge, and solidify understanding.

But there's one problem: **you don't always have someone to teach.**

**Aazan solves that.** Bodhi, your AI student, is always ready to learn — and to ask you the questions that reveal what you *don't* actually know yet.

---

## ✨ What It Does

| Feature | Description |
|---|---|
| 📝 **Text Input** | Paste any content — notes, articles, concepts — and start a teaching session |
| 📄 **PDF Upload** | Upload study material directly; Aazan extracts and processes it for you |
| 🎙️ **Voice Chat** | Teach Bodhi out loud, the most natural form of explanation |
| 🤖 **AI Student (Bodhi)** | An AI that asks follow-up questions, challenges your explanations, and identifies gaps |
| 🗂️ **Session Management** | Full CRUD — create, retrieve, and manage your teaching sessions |

---

## 🏗️ Architecture & Technical Decisions

### Why Rust?

This is where most developers would reach for Node.js or Python. I chose Rust + Axum deliberately:

**The Trade-off I made:**
- ❌ Slower initial development velocity
- ✅ Memory safety without a garbage collector
- ✅ WebAssembly-native (Dioxus compiles to WASM for the frontend)
- ✅ Single binary deployment — no runtime dependencies
- ✅ Performance headroom for real-time voice processing

For an app that handles file uploads, PDF parsing, and real-time AI interactions simultaneously, Rust's ownership model means **no race conditions, no memory leaks, no surprises in production.**

### Why a Monolith?

The temptation in 2024–2026 is to immediately reach for microservices. I chose a **deliberate monolith**:

- Single Axum + Dioxus codebase
- Shared types between frontend and backend — no API contract drift
- One deployment, one mental model
- Easy to extract services later *if* scale demands it

> **The rule I follow:** Distribute when you have a proven reason. Not before.

### Tech Stack

```
Backend:   Axum (async Rust web framework)
Frontend:  Dioxus (Rust → WebAssembly)
Database:  SQLite via sqlx
PDF:       pdf-extract crate (in-memory processing)
AI:        Anthropic Claude API
Input:     Multipart form data, text, voice
```

---

## 📡 API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/session` | Create session from text or PDF |
| `GET` | `/api/sessions` | List all sessions |
| `GET` | `/api/session/{id}` | Retrieve specific session |
| `DELETE` | `/api/session/{id}` | Delete a session |

---

## 🚀 Getting Started

```bash
# Clone the repo
git clone https://github.com/bunnyBites/aazan
cd aazan

# Set your environment variables
cp .env.example .env
# Add your Anthropic API key to .env

# Run the app
cargo run
```

> **Prerequisites:** Rust 1.75+, SQLite

---

## 🗺️ Roadmap

- [x] Session Management API (create, read, delete)
- [x] PDF file upload + text extraction
- [x] Text-based teaching sessions
- [ ] Voice input integration
- [ ] Bodhi's adaptive questioning engine
- [ ] Session analytics (gap detection)
- [ ] Public deployment

---

## 💡 What I Learned Building This

**1. Rust's learning curve is a feature, not a bug.**
The compiler's strictness forced me to think about ownership and concurrency *before* they became runtime bugs. Every fight with the borrow checker was a bug I didn't ship.

**2. Monolithic Dioxus + Axum is underrated.**
Sharing types across the stack in a single Rust codebase eliminates an entire category of bugs — the "frontend expects X, backend sends Y" class of errors that plagues TypeScript projects.

**3. Building an AI-native app requires product thinking, not just API calls.**
Integrating Claude isn't hard. Designing *how* Bodhi asks questions — pedagogically, progressively, without overwhelming the user — that's the real engineering challenge.

---

## 👤 About the Author

**Mukesh Kumar** — Senior Software Engineer with 7+ years building scalable frontend systems.

- 🌐 [bitsbunny.com](https://bitsbunny.com)
- 💼 [LinkedIn](https://www.linkedin.com/in/mukeshkumar-s)
- 🐙 [GitHub](https://github.com/bunnyBites)
- 🦀 Open source contributor: [Dioxus](https://github.com/DioxusLabs/dioxus/pull/1610) · [Yew](https://github.com/trunk-rs/trunk/pull/614) · [Solana](https://github.com/Unboxed-Software/solana-course/pull/285)

---

*Aazan — from the Tamil word for "teacher" and the Hindi word for "easy."*
*Because learning should be both.*
