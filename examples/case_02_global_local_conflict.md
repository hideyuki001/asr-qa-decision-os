# Case 02 — Global vs Local Certainty Conflict

## Case ID

`global_local_conflict`

---

## Input Observation

The utterance sounds natural when heard as a whole:

```text
渋いっすよねー
```

However, when evaluated at the slot level, parts of the audio are unclear and cannot be confirmed with certainty.

---

## Judgment Problem

The sentence is globally coherent and plausible.

But individual tokens cannot be confidently verified from the audio.

The question is:

> Should the evaluator output the full sentence based on overall naturalness, or mask uncertain segments?

---

## Applied Rule

```yaml
rule_id: RF-03
name: Slot-Level Certainty Gate
priority: S+
```

---

## Decision Gate

```yaml
condition:
  global_context_natural: true
  local_certainty: false
```

---

## Decision

```yaml
decision: partial_unintelligible
output: （unintelligible）っすよねー
```

---

## Reasoning

Global naturalness does not justify output.

Even if the sentence is highly plausible, each token must be independently verified.

Unclear segments must not be reconstructed from context.

---

## Controller Result

```yaml
controller:
  if_triggered: DEFER
```

---

## Principle

```yaml
pl:
  jp: "通しで自然でもスロットで確定できなければ書かない"
  en: "Even if globally natural, do not output unless locally certain"
```

---

## Final Judgment

The sentence is partially masked:

```text
（unintelligible）っすよねー
```

Only the confirmed portion is retained.

---

## Related Rules

- RF-02 — No Inference (Global Principle)
- RF-03 — Slot-Level Certainty Gate

---

## Notes

This case demonstrates a core principle:

> Naturalness is not evidence.

The system prioritizes audio certainty over contextual plausibility.
