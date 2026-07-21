# OGEA-102 TOGAF EA Practitioner — Exam Cheatsheet

**Format:** 8 scenario case studies, 4 ranked answers each, 90 min, 60% pass, **open book**  
**Scoring:** Best=5, 2nd=3, 3rd=1, Worst=0  
**Source:** csahli/TOGAF_EA_10_Prep, xde013/togaf, Gana-Dube/togaf-exam-hub, ITExams OG0-092, ExamTopics

---

## 1. EXAM STRATEGY

| Rule | Detail |
|------|--------|
| **Open book** | TOGAF Standard 10th Edition available as in-exam reference. Know Part numbers to find content fast |
| **Time** | ~11 min per scenario. Spend 3 min reading, 5 min analyzing options, 3 min ranking |
| **Scoring** | You can get 3/5 (second-best) on every question even if you miss the best — that's 60% = pass |
| **Process** | Read scenario → Identify ADM phase + topic → Eliminate 0-pt distractors → Rank remaining 3 |
| **Don't** | Over-rely on open book; 11 min per Q is tight. Know the standard's structure before the exam |

### Distractor Recognition — Instant 0-Point Answers
| If you see this | It's 0 pts (distractor) |
|----------------|-------------------------|
| "Skip governance" / "informal approval" | Always wrong |
| "Disband the Architecture Board" | Always wrong |
| "Ignore/exclude a key stakeholder" | Always wrong |
| "Defer to risk log, retrofit later" | Always wrong |
| "Implement straight into production, document after" | Always wrong |
| "Skip Preliminary Phase, start building" | Always wrong |
| "Big-bang implementation" | Usually wrong |
| "Conventional planning (not Capability-Based)" | Usually wrong |
| "Build bespoke without checking reuse" | Always wrong |
| "Security only in Phase D" | Always wrong |
| "Single mandated tech stack, no exceptions" | Always wrong |

---

## 2. PHASE-BY-PHASE MASTER TABLE

### Preliminary Phase — "Set up the capability"
| Correct Action | Wrong Action |
|---------------|--------------|
| Tailor ADM to org context (regulatory, agile, size) | Skip Preliminary / start at Phase A |
| Establish Architecture Capability with governance | Implement full TOGAF without tailoring |
| Define architecture principles (Business, Data, App, Tech) | Use generic principles without customization |
| Integrate existing reference models into Enterprise Continuum | Ignore existing assets |
| Set up proportionate governance | Create heavyweight bureaucracy |
| Assess security policy requirements; allocate security team | Defer security to later phases |
| Assess EA maturity | No maturity assessment |

### Phase A — "Get everyone aligned before building"
| Correct Action | Wrong Action |
|---------------|--------------|
| Create Stakeholder Map — identify ALL stakeholders | Focus only on powerful stakeholders |
| Translate concerns → requirements → constraints | Record concerns in risk log; deal later |
| Reconcile conflicting metrics into agreed KPIs | Document conflicts as constraints; delegate resolution |
| Use Business Scenarios to elicit requirements | Jump to solutions / vendor research |
| Develop Architecture Vision as high-level aspirational view | Create detailed technical design |
| Obtain approved Statement of Architecture Work | Start detailed work without approval |
| Develop Communications Plan for each stakeholder group | No communication planning |
| Include key external stakeholders (regulators, partners) | Exclude external stakeholders to protect speed |

### Phase B — "Map business capabilities, not project lists"
| Correct Action | Wrong Action |
|---------------|--------------|
| Develop Business Capability Map (baseline + target) | Take executives' project list and prioritize by cost/speed |
| Assess maturity per capability (heat map) | No maturity assessment |
| Trace capabilities → value streams → strategic goals | Build capability map but don't use it for decisions |
| Perform Gap Analysis (baseline vs target) | Skip gap analysis |
| Create Business Service/Function catalog, Process Flow diagrams | Only create high-level diagrams |
| Prioritize capability increments objectively | Let politics decide which projects are funded first |

### Phase C — Data Architecture
| Correct Action | Wrong Action |
|---------------|--------------|
| Define authoritative (master) sources for key data entities | Leave each app with its own definitions |
| Assign clear data ownership and stewardship | No ownership |
| Establish common definitions and data standards | Build reconciliation layer for reporting only |
| Perform gap analysis against baseline | Load everything into data lake as-is |
| Create Data Entity catalog, Data Security diagram | Focus only on technology |

### Phase C — Application Architecture
| Correct Action | Wrong Action |
|---------------|--------------|
| Map proposed products to logical application components | Approve all proposed products to avoid politics |
| Identify overlaps and gaps explicitly | Pick cheapest per function regardless of integration |
| Recommend rationalized application portfolio | Commit to single product without quantifying gaps |
| Create Application Communication diagrams | Skip rationalization |

### Phase D — Technology Architecture
| Correct Action | Wrong Action |
|---------------|--------------|
| Define Target Technology Architecture with standards catalogue | Mandate single stack with no exceptions |
| Perform gap analysis against baseline | Make standards advisory only (no enforcement) |
| Establish **governed dispensation process** for non-standard tech | Let every team choose independently |
| Create Technology Portfolio catalog, Technology Standards catalog | No catalog |
| Use TRM as reference | Ignore reference models |

### Phase E — "Plan the journey"
| Correct Action | Wrong Action |
|---------------|--------------|
| Create Architecture Roadmap with Transition Architectures | Big-bang implementation |
| Sequence work packages by dependency and business value | Sequence by easiest |
| Perform Interoperability Analysis (multi-vendor/partner) | Skip interoperability |
| Make Build vs Buy vs Reuse decisions | Default to build |
| Review Business Transformation Readiness Assessment; mitigate risks | Ignore readiness |
| Consolidate gap analysis results from Phases B, C, D | Skip gap consolidation |
| Apply Capability-Based Planning for prioritization | Conventional planning |

### Phase F — "Finalize the plan"
| Correct Action | Wrong Action |
|---------------|--------------|
| Finalize Implementation and Migration Plan (v1.0) | Keep initial v0.1 without refinement |
| Coordinate with enterprise's overall change portfolio | Plan in isolation |
| Prioritize via Capability-Based Planning | Prioritize by cost or ease |
| Estimate resources, timings, delivery vehicles | No resource planning |
| Assign business value to each work package | Only track cost |

### Phase G — "Govern the build"
| Correct Action | Wrong Action |
|---------------|--------------|
| Create Architecture Contracts with implementers | No contracts |
| Conduct compliance reviews at key milestones | Only review at end |
| **Document non-conformance formally** | Informal approval |
| **Require remediation OR formal time-bound dispensation BEFORE go-live** | Allow go-live, fix later |
| Dispensation = conditions + remediation plan + ARB approval | No conditions or expiry |
| Post-implementation review + document lessons learned | Close without review |

### Phase H — "Manage ongoing change"
| Correct Action | Wrong Action |
|---------------|--------------|
| **Classify change**: Simplification, Incremental, or Re-architecting | Treat all changes the same |
| **Re-architecting** = new capabilities/regulations/partners → **new ADM cycle** starting at Architecture Vision | Treat as incremental, update in place |
| **Incremental** = minor additions → update existing architecture | Trigger full new cycle for minor change |
| Establish value realization process + monitoring | No monitoring |
| Manage risks continuously | Risk management stops at go-live |

### Requirements Management (Continuous)
| Correct Action | Wrong Action |
|---------------|--------------|
| **Requirements Impact Assessment** for every new/changed requirement | Ignore or implement immediately |
| Feed changes into relevant ADM phases | Log and defer to next cycle |
| Maintain Consolidated Requirements Repository | No central tracking |

---

## 3. GOVERNANCE — THE UNBREAKABLE SEQUENCE

```
Architecture Contract  →  Compliance Review  →  Deviation Found
                                  ↓
                 Document Non-Conformance formally
                                  ↓
                      Assess risk/impact of deviation
                                  ↓
                 Require EITHER:
                   (a) Remediation to conformance, OR
                   (b) Formal time-bound dispensation
                       WITH conditions + remediation plan
                       + Architecture Board approval
                                  ↓
                      ALL BEFORE go-live
                      (NEVER after)
```

### Fixing a Bottleneck Architecture Board
| ❌ Wrong | ✅ Correct |
|----------|-----------|
| Add more members to the Board | Introduce **proportionate risk-based governance** |
| Increase meeting frequency | Define delegation criteria: low-impact → streamlined route |
| "We need universal approval for consistency" | Board reserves attention for **high-impact decisions** only |

---

## 4. COMPLIANCE LEVELS

| Level | Definition | When to Use |
|-------|-----------|-------------|
| **Conformant** | All spec features implemented (extra features OK) | Everything per spec, possibly with extras |
| **Consistent** | Features in common; deviation in areas NOT covered by spec | Different approach but no spec violation |
| **Non-conformant** | **Key feature NOT implemented per specification** | Deviation from spec (even if everything else works) |

### Trap: "It works fine and meets requirements" ≠ Conformant
If the architecture spec mandates user-mode threads and the implementation uses kernel-mode RPC, it is **Non-conformant** — regardless of whether it "works."

---

## 5. THE 10 MOST TESTED SCENARIO PATTERNS

| Pattern | Correct Answer Formula |
|---------|----------------------|
| **Stakeholder conflict** | Stakeholder Map → concerns → reconcile → agreed KPIs in Vision → Comms Plan |
| **Regulatory change mid-project** | Requirements Impact Assessment → feed into relevant phases → change classification |
| **Deviation from architecture** | Document non-conformance → remediate OR formal dispensation BEFORE go-live |
| **Multi-vendor/partner integration** | Interoperability Analysis (Phase E) + III-RM reference model |
| **Technology sprawl vs innovation** | Standards catalogue + governed dispensation process |
| **Legacy modernization** | Transition Architectures → incremental delivery → Capability-Based Planning |
| **Reusable assets exist, team wants bespoke** | Direct to governed ABB/SBB → require adoption → gaps through dispensation |
| **Architecture Board bottleneck** | Proportionate risk-based governance → delegate low-impact decisions |
| **Global vs local requirements** | Architecture Partitioning + SIB for standards + dispensation for local needs |
| **Security/compliance concerns** | Integrated in ALL ADM phases (not a single checkpoint) |

---

## 6. ADM TECHNIQUES — When to Use

| Technique | Used In | Purpose |
|-----------|---------|---------|
| Gap Analysis | B, C, D | Baseline vs Target comparison |
| Business Scenarios | Phase A | Elicit business requirements |
| Stakeholder Management | Phase A, all phases | Map concerns, plan engagement |
| Capability-Based Planning | Phase B, E, F | Prioritize investments by business value |
| Business Transformation Readiness | Phase A, E | Assess organizational readiness for change |
| Interoperability Analysis | Phase E | Assess system integration issues |
| Risk Management | ALL phases | Continuous risk identification/mitigation |
| Migration Planning | Phase E, F | Sequence Transition Architectures |
| Compliance Review | Phase G, H | Verify implementation conformance |

---

## 7. OPEN BOOK — QUICK REFERENCE

| Topic | Where in TOGAF Standard (10th Ed) |
|-------|-----------------------------------|
| ADM Process (all phases) | Part II (chapters 2–11) |
| ADM Techniques | Part III |
| Architecture Content Framework | Part IV |
| Enterprise Continuum | Part V |
| Reference Models (TRM, III-RM) | Part VI |
| Architecture Capability / Governance | Part VII |
| Stakeholder Management | Part III / Part II ch. 3 |
| Architecture Principles | Part III |
| Business Scenarios | Part III |
| Capability-Based Planning | Part III |
| Risk Management | Part III |
| Gap Analysis | Part III |
| Building Blocks (ABB vs SBB) | Part IV |

**Practice tip:** During the exam, use the REFERENCE button to search by Phase (e.g., "Phase G") or technique name. The material is searchable.

---

## 8. COMMON TRAPS — EXACT WORDING

| Question Phrase | What It Means / Trap |
|----------------|---------------------|
| "The Board must approve everything" | **Distractor** — leads to bottleneck; correct = proportionate governance |
| "Records concerns in the risk log" | **Partial** (1-3 pts) — logging ≠ addressing; concerns must be reconciled |
| "Build a bespoke solution" | **Distractor** if a reusable asset exists; correct = reuse with dispensation |
| "Advisory standards" | **Partial** — standards without governance have no teeth |
| "Implement and document after" | **0 pts** — sequence is critical: governance must constrain, not follow |
| "Conventional implementation planning" | **Distractor** when scope is enterprise-wide; use Capability-Based Planning |
| "Skip Preliminary Phase, start building" | **0 pts** — always establish capability first |
| "Data lake as-is, defer definitions" | **Partial** — loads data but doesn't fix inconsistency at root |
| "Incremental change" for new regulated product line | **Wrong classification** — that's re-architecting |
| "Highest-impact entities only" for data fix | **Partial** — fixes part of problem but ignores root cause |

---

## 9. RAPID DECISION FLOW

```
What phase is the scenario in?
├─ Preliminary  → Establish capability + tailor + principles + governance
├─ Phase A      → Stakeholders + Vision + SoW approval + Business Scenarios
├─ Phase B      → Capability map + value streams + gap analysis
├─ Phase C      → Data: authoritative sources + ownership + standards
│                 App: rationalize proposed products against capabilities
├─ Phase D      → Standards catalogue + dispensation process + gap analysis
├─ Phase E      → Roadmap + Transition Architectures + interoperability + make/buy
├─ Phase F      → Finalize Migration Plan + prioritize + coordinate frameworks
├─ Phase G      → Compliance review + Architecture Contract + dispensation BEFORE go-live
├─ Phase H      → Classify change (re-architecting → new ADM cycle)
└─ Requirements → Impact Assessment → feed into phases

Is there a governance issue?
├─ Deviation → Document → Remediate OR formal dispensation BEFORE go-live
├─ Bottleneck → Proportionate risk-based governance with delegation
├─ No governance → Set up Architecture Board + Contracts + reviews
└─ Compliance → Conformant/Consistent/Non-conformant per spec

Is there a stakeholder concern?
├─ Identify → Map → Reconcile → Address in Vision/views → Comms Plan
└─ Never exclude, never defer, never ignore

Is there a technology choice?
├─ Standards catalogue + governed dispensation process
└─ Never single mandated stack, never purely advisory
```

---

## 10. LAST-MINUTE MEMORY AIDS

| Acronym | Meaning |
|---------|---------|
| **BDAT** | Business, Data, Application, Technology (architecture domains) |
| **ABB/SBB** | Architecture Building Block (what) / Solution Building Block (how) |
| **TRM/III-RM** | Tech Ref Model (platform) / Integrated Info Infrastructure (boundaryless flow) |
| **SIB** | Standards Information Base (specs architectures must conform to) |
| **ACMM** | Architecture Capability Maturity Model |
| **SoW** | Statement of Architecture Work (scope contract between sponsor and architecture team) |
| **ARB** | Architecture Review Board (governance body) |
| **BTRA** | Business Transformation Readiness Assessment |
| **CBP** | Capability-Based Planning |
| **RfW** | Request for Architecture Work (triggers ADM cycle) |
| **RIS** | Requirements Impact Statement |
| **WBS** | Work Breakdown Structure |

**Correct answer keywords:** governed, proportionate, dispensation, stakeholder map, concerns, capability map, value stream, gap analysis, authoritative source, compliance review, Transition Architecture, integrated, tailored, reuse, continuous.

**Distractor keywords:** informal, skip, defer, bypass, universal, bespoke, big-bang, as-is, conventional, record-only, advisory-only.

---

*From analysis of 128 csahli questions + 18 Gana-Dube + 18 xde013 + 10 OG0-092 classic scenarios + official Open Group exam syllabus.*
