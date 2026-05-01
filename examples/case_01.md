# Case 01 — Contextual Reinforcement Recovery

## Case ID

`contextual_recovery`

---

## Input Observation

An unclear token appeared earlier in the audio:

```text
エトチル
```

Later in the same context, the speaker clearly produced:

```text
出トチるわ
```

---

## Judgment Problem

The earlier token was unclear in isolation.

However, the same token appeared later with clearer audio evidence.

The question is:

> Can the earlier unclear token be recovered, or should it remain unintelligible?

---

## Applied Rule

```yaml
rule_id: RF-07
name: Contextual Reinforcement Recovery
priority: S
```

---

## Decision Gate

```yaml
condition:
  unclear_token: true
  same_token_later_clear: true
  context_match: true
  same_speaker_or_same_topic: true
  recovery_based_on_audio_evidence: true
```

---

## Decision

```yaml
decision: recover
output: 出トチる
```

---

## Reasoning

This is not unsupported inference.

The recovery is allowed because the later occurrence provides clear audio evidence that confirms the earlier unclear token.

The decision is based on evidence, not contextual guessing.

---

## Controller Result

```yaml
controller:
  if_triggered: ALLOW
```

---

## Principle

```yaml
pl:
  jp: "後続の明確な音声証拠により前方を復元できる"
  en: "Earlier tokens may be recovered using later confirmed audio evidence"
```

---

## Final Judgment

The earlier unclear token may be recovered as:

```text
出トチる
```

because the later audio confirms the same expression.

---

## Related Rules

- RF-02 — No Inference
- RF-07 — Contextual Reinforcement Recovery

---

## Notes

This case demonstrates the boundary between:

- prohibited contextual inference
- permitted evidence-based recovery

The key distinction is whether later audio evidence confirms the token.
