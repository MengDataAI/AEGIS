# Regex (baseline)

Rule-based keyword matching over the clinical note. **Baseline for smoke testing only.**

## What it does

Case-insensitive keyword matching (`graphs/regex/regex_terms.txt`) categorized into the six irAE event types (colitis, dermatitis, hepatitis, myocarditis, pneumonitis, thyroiditis). A match sets a binary `1` (otherwise `0`), and that value is copied into the grade/attribution/certainty fields.

## Limitations

This is intentionally simple and is **not** a real extraction method. It does **not** handle:

- **Negation** — "no evidence of colitis" still matches `colitis`.
- **Severity / grade** — output is binary 0/1, not a CTCAE grade.
- **Attribution** — no reasoning about drug causality; attribution just mirrors the match.
- **Temporality** — no past-vs-current distinction.

For real extraction, use an LLM workflow: `openai_zeroshot`, `openai_agent`, or `agent_split_temporality`.

## Run

```bash
python main.py regex \
  --model_config default \
  --prompt_variant default \
  --data_dir data/synthetic_notes \
  --output_base_dir outputs \
  --debug
```

Needs no API key, so it is the fastest way to verify the pipeline end-to-end.
