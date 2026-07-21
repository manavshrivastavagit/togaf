# TOGAF Part 2 — Last Minute Exam Cheat Sheet

**Part 2 = Scenario-Based.** You read a complex situation, then rank 4 responses (Best=5, 2nd=3, 3rd=1, Worst=0). 60% to pass. Open book (TOGAF Standard searchable).

---

## HOW PART 2 DIFFERS FROM PART 1

| Part 1 | Part 2 |
|--------|--------|
| Recall & comprehension | **Apply & analyze** |
| Simple Q → 1 answer | Scenario → **rank 4 answers** |
| Memorize definitions | **Pick the BEST action** in context |
| Closed book | **Open book** (but no time to look up much) |
| ~1.5 min/question | ~11 min/scenario |

---

## THE 5 SCENARIO PATTERNS (90% of questions)

### PATTERN 1: "Something went wrong — fix it"
**Keywords:** deviation, non-compliance, bypass, skip, informal

**Correct sequence:**
1. Document non-conformance formally
2. Assess risk/impact
3. Require EITHER remediation OR formal time-bound dispensation
4. **BEFORE go-live** (never after)

**Distractors (instant 0 pts):**
- "Allow go-live and fix later"
- "Informal approval"
- "Retrofit after deployment"

---

### PATTERN 2: "Multiple stakeholders disagree"
**Keywords:** conflict, competing priorities, concerns, CIO vs CISO vs regulator

**Correct approach:**
1. Create **Stakeholder Map** — identify ALL
2. Translate concerns → requirements → constraints
3. **Reconcile** conflicting metrics into agreed KPIs
4. Document in **Architecture Vision**
5. Create **Communications Plan** per group

**Distractors:**
- "Focus only on powerful stakeholders"
- "Record concerns in risk log; deal later"
- "Exclude external stakeholders to protect speed"

---

### PATTERN 3: "New regulation / market change mid-project"
**Keywords:** regulatory, mandate, compliance, new requirement

**Correct approach:**
1. **Requirements Impact Assessment** (not "log and defer")
2. Feed changes into relevant ADM phases
3. Classify change:
   - **Simplification** → streamline existing
   - **Incremental** → minor additions, update existing
   - **Re-architecting** → new capabilities/regulations → **NEW ADM cycle** starting at Architecture Vision
4. Update **Consolidated Requirements Repository**

**Distractors:**
- "Defer to next cycle"
- "Implement immediately without assessment"
- "Treat re-architecting as incremental"

---

### PATTERN 4: "Team wants to build bespoke / ignore standards"
**Keywords:** custom, bespoke, ignore, build from scratch, skip reuse

**Correct approach:**
1. Point to **Architecture Repository** — show reusable assets
2. Require adoption of **ABBs/SBBs**
3. Gaps → **governed dispensation process** (if justified)
4. Document in **Standards Information Base**

**Distractors:**
- "Let them build custom"
- "Skip checking for reusable assets"
- "Advisory standards only"

---

### PATTERN 5: "Technology sprawl / everyone choosing their own stack"
**Keywords:** inconsistent, fragmented, no standards, every team different

**Correct approach:**
1. Define **Technology Standards Catalogue**
2. Establish **governed dispensation process** for exceptions
3. **Proportionate risk-based governance** (not universal approval)
4. Board reserves attention for **high-impact decisions only**

**Distractors:**
- "Mandate single stack with no exceptions"
- "Let every team choose independently"
- "Add more Board members to approve everything"

---

## QUICK DECISION TREE

```
Read scenario → What's the problem?
│
├─ Deviation from architecture?
│  → Document → Remediate OR dispensation BEFORE go-live
│
├─ Stakeholder conflict?
│  → Map ALL → Reconcile → Vision + Comms Plan
│
├─ New external change (regulation/market)?
│  → Impact Assessment → Classify (simplification/incremental/re-architecting)
│  → Re-architecting = NEW ADM cycle at Architecture Vision
│
├─ Team ignoring standards/reuse?
│  → Show repository → Require adoption → Dispensation if gaps
│
├─ Technology inconsistency?
│  → Standards catalogue + governed dispensation + proportionate governance
│
├─ Legacy modernization?
│  → Transition Architectures + Capability-Based Planning + incremental delivery
│
├─ Architecture Board bottleneck?
│  → Proportionate risk-based governance + delegation criteria
│
└─ Security/compliance concern?
   → Integrated in ALL phases (not a single checkpoint)
```

---

## COMPLIANCE LEVELS (Memorize These)

| Level | Meaning | Example |
|-------|---------|---------|
| **Conformant** | All spec features + extras OK | Everything per spec, with bonuses |
| **Consistent** | Features in common, deviation in areas NOT covered by spec | Different approach, no spec violation |
| **Non-conformant** | **Key feature NOT implemented per specification** | Even if "it works fine" |

**Trap:** "It works and meets requirements" ≠ Conformant. If spec says X and you did Y = Non-conformant.

---

## WHEN TO USE WHICH ADM PHASE

| Situation | Phase |
|-----------|-------|
| Setting up architecture capability | **Preliminary** |
| Getting alignment, creating Vision | **Phase A** |
| Business processes, capabilities, value streams | **Phase B** |
| Data entities, authoritative sources, ownership | **Phase C (Data)** |
| Application portfolio, product rationalization | **Phase C (App)** |
| Technology standards, platform, dispensation | **Phase D** |
| Roadmap, Transition Architectures, interoperability | **Phase E** |
| Finalize Migration Plan, prioritize | **Phase F** |
| Compliance reviews, Architecture Contracts | **Phase G** |
| Classify ongoing changes, value realization | **Phase H** |
| Continuous requirements tracking | **Requirements Mgmt** |

---

## INSTANT 0-POINT ANSWERS (Never Pick These)

| Phrase in Answer | Why It's Wrong |
|------------------|----------------|
| "Skip Preliminary Phase" | Always establish capability first |
| "Informal approval" | Governance must be formal |
| "Disband the Board" | Never remove governance |
| "Go-live first, fix later" | Governance before implementation |
| "Big-bang implementation" | Use Transition Architectures |
| "Conventional planning" for enterprise scope | Use Capability-Based Planning |
| "Build bespoke" when reusable assets exist | Always check reuse first |
| "Security in Phase D only" | Security = ALL phases |
| "Single mandated stack, no exceptions" | Need dispensation process |
| "Advisory standards" | Standards need governance teeth |
| "Defer concerns to risk log" | Logging ≠ addressing |
| "Exclude stakeholders for speed" | Never exclude key stakeholders |

---

## OPEN BOOK — QUICK LOOKUP

| If question is about... | Look in... |
|-------------------------|------------|
| ADM phases & steps | Part II (chapters 2-11) |
| Gap Analysis, Business Scenarios, CBP | Part III |
| Architecture Content, Building Blocks | Part IV |
| Enterprise Continuum, Repository | Part V |
| TRM, III-RM reference models | Part VI |
| Governance, Architecture Capability | Part VII |

---

## MEMORY WORDS

**Correct answers contain:** governed, proportionate, dispensation, stakeholder map, reconcile, capability map, value stream, gap analysis, authoritative source, compliance review, Transition Architecture, tailored, reuse, continuous, impact assessment

**Distractors contain:** informal, skip, defer, bypass, universal, bespoke, big-bang, as-is, conventional, record-only, advisory-only, after go-live, mandate

---

## 30-SECOND PRE-EXAM REVIEW

1. **Part 2 = scenarios, rank 4 answers, 60% pass**
2. **Governance BEFORE implementation, always**
3. **Re-architecting = new ADM cycle** (don't treat as incremental)
4. **Dispensation = conditions + remediation + Board approval + BEFORE go-live**
5. **Non-conformant = spec says X, you did Y** (even if it works)
6. **Never skip, defer, or bypass** — always assess, classify, act
7. **Capability-Based Planning** for enterprise prioritization
8. **Stakeholder Map** for all conflicts
9. **Proportionate governance** to fix bottlenecks (not more meetings)
10. **Open book is searchable** — use REFERENCE button wisely

---

*Good luck! Remember: pick the MOST comprehensive, governed, stakeholder-inclusive answer.*
