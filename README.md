# ASR QA Decision OS v0.1

ASR QA is not annotation — it's a decision system.

ASR QA often suffers from inconsistent human judgment and hidden inference.  
This system eliminates both.

A deterministic system where the same input produces the same judgment outcome.  
This repository transforms subjective human QA into a structured, traceable, and auditable process.

---

## 🧠 What This System Does

Instead of relying on human intuition, this system enforces:

- **No unsupported inference**  
  → Judgments must be grounded in audio evidence only

- **Slot-level certainty**  
  → Each segment is evaluated independently with explicit certainty

- **Evidence-based recovery**  
  → Recovery is allowed only with clear audio confirmation

- **Traceable decision logic**  
  → All decisions follow explicit, reproducible rules

---

## ⚙️ Core Decision System

The full decision logic is defined here:

👉 [`asr_qa_decision_os.yaml`](./asr_qa_decision_os.yaml)

This is not configuration.  
This is not a guideline.  

This is an **enforceable decision system**.

It includes:

- Rule system (RF-01 ~ RF-09)
- Priority engine (JSI: Judgment Selection Interface)
- Decision controller (STOP / DEFER / ALLOW)
- Real-world validated edge cases

---

## 🔍 Example Rule (Excerpt)

```yaml
- rule_id: RF-02
  name: No Inference (Global Principle)
  condition:
    certainty: false
    inferred_from_context: true
  action:
    output: unintelligible
```

👉 If something is not clearly heard,  
it must not be reconstructed from context.

---

## 🧩 Decision Architecture

```
Input
  ↓
Rule Layer (RF-01 ~ RF-09)
  ↓
Priority Engine (JSI)
  ↓
Decision Controller
  ↓
Output (STOP / DEFER / ALLOW)
```

### Components

**1. Rule Layer**  
- Defines evaluation constraints  
- Prevents hallucination and over-interpretation  

**2. Priority Engine (JSI)**  
- Resolves conflicts between rules  

Examples:
- inference vs audio → audio wins  
- global context vs local certainty → local wins  

**3. Decision Controller**

| State | Behavior |
|------|--------|
| STOP | Blocks invalid output (hallucination, mutation) |
| DEFER | Outputs partial / unintelligible |
| ALLOW | Accepts output |
| ALLOW_WITH_UI_ADJUSTMENT | Structural correction (e.g. overlap split) |

---

## 🔬 Real Decision Cases

This system is validated using real ASR edge cases:

**Contextual Recovery**  
「エトチル」→「出トチる」  
→ recovered using later audio evidence  

**Global vs Local Conflict**  
Sentence is natural, but slot is uncertain  
→ partial unintelligible  

**Particle Mutation Risk**  
助詞変更による意味変化  
→ forced rollback  

**Phonetic Loop Preservation**  
「ララレラレレレ」  
→ preserved as meaningful utterance  

**Safe Word Retention**  
「ママチャリ」  
→ preserved due to clarity + consistency  

---

## 📁 Repository Structure

```
/README.md
/rules/asr_qa_decision_os.yaml   # Core decision system
```

---

## 🎯 Who This Is For

- AI evaluators (ASR / LLM / multimodal)
- QA engineers
- Dataset curators
- Human-in-the-loop pipeline designers

---

## 🧠 Philosophy

This system transforms QA from a task into a deterministic system.

Human judgment is not removed —  
it is constrained, structured, and made reproducible.

---

## 🚧 Status

v0.1 — Initial rule system & decision engine

---

## 🔮 Future Directions

- Decision trace visualization  
- Integration with LLM evaluation pipelines  
- Expansion to multimodal QA (ASR + VLM)  
- Automated error pattern detection  

---

## 🔗 Related Work

This project is the execution layer of:

ASR QA Judgment Framework  
https://github.com/hideyuki001/asr-qa-judgment-framework

---

## 📌 Author

Hideyuki Okabe  
Senior AI Evaluator | ASR / LLM QA Specialist  
Designer of reproducible judgment systems
