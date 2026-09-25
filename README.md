# 📕 Contradex

> *Gotta catch 'em all... contradictions, that is.*

**Contradex** is a privacy-first pipeline that ingests a user's medical, insurance, lease, and loan PDFs and flags contradictions across sources and time — like a Pokédex, but instead of cataloging creatures, it catalogs the claims buried in your paperwork and tells you when two of them don't evolve into the same truth.

**Status:** 🔴 In Progress (still in the tall grass, actively training)

---

## 🎒 Trainer's Toolkit

| Badge | Tech |
|---|---|
| ⚡ | Python |
| 🔥 | PyTorch |
| 💧 | Hugging Face |

---

## 🧬 What It Does

Real-world documents lie to each other constantly — an EOB says a hospital stay was *outpatient*, the discharge summary says *inpatient*. Contradex hunts down exactly these kinds of mismatches.

### 🥚 Stage 1: Extraction (The Egg)
LLM-based structured extraction hatches free text into clean **claim tuples**:

```
(entity, attribute, value, date, source)
```

Every document becomes a set of catchable, comparable claims instead of an unstructured wall of text.

### 🐛 Stage 2: Retrieval (First Evolution)
Embedding clustering acts like a **radar for wild claim pairs** — it surfaces candidate claims that share an entity and are worth comparing, so we're not brute-forcing every claim against every other claim.

### 🐉 Stage 3: Verification (Final Evolution)
A **DeBERTa-v3 NLI cross-encoder** goes head-to-head with each candidate pair, with an **LLM-as-judge fallback** called in as backup when the fight is close. Together they decide:

- ⚔️ **Contradiction** — the claims can't both be true
- 🕊️ **Legitimate change over time** — the claims evolved, no battle needed

---

## 🗺️ Route Map (Architecture)

```
Documents (medical / insurance / lease / loan PDFs)
        │
        ▼
  ┌─────────────┐
  │  Extraction │  → (entity, attribute, value, date, source) tuples
  └─────────────┘
        │
        ▼
  ┌─────────────┐
  │  Retrieval  │  → embedding clustering → candidate claim pairs
  └─────────────┘
        │
        ▼
  ┌─────────────┐
  │ Verification│  → DeBERTa-v3 NLI + LLM-as-judge fallback
  └─────────────┘
        │
        ▼
   🚩 Contradictions flagged
```

---

## 🔒 Privacy First

No badge is worth handing over your medical records carelessly. Contradex is designed to process sensitive personal documents (medical, insurance, lease, loan) with privacy as a first-class constraint, not an afterthought.

---

## 🏆 Roadmap

- [x] Design claim tuple schema
- [x] Architect two-stage retrieval + verification
- [ ] Finish LLM-based extraction pipeline
- [ ] Train/evaluate DeBERTa-v3 NLI cross-encoder
- [ ] Wire up LLM-as-judge fallback
- [ ] End-to-end evaluation on real document sets

---

*May your claims never contradict, and your discharge summaries always match your EOBs.*
