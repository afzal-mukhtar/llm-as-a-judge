# From Prompt to Verdict: Building LLM Judges That Actually Work

> Every AI team eventually faces the same wall: your model generates answers, but how do you know they're any good? Manual review doesn't scale. BLEU and ROUGE miss the point. And asking an LLM "is this correct?" gives you confident nonsense.
>
> In this 2-hour build-along bootcamp, you'll construct a complete LLM-as-a-Judge pipeline from zero — structured prompts, chain-of-thought reasoning, adversarial critique, bias detection, multi-judge ensembles, confidence calibration, and the LLM Council pattern. Every technique is coded live, tested against the same examples, and benchmarked against human expert scores.
>
> Walk in with a laptop. Walk out with a production-ready evaluation system you built yourself.

## 46 Techniques. 9 Blocks. 120 Minutes. You Code Everything.

| Block | Time | What You Build |
|-------|------|---------------|
| 1. Why Evaluation Is Broken | 0–15 min | See naive judges fail with your own eyes |
| 2. Structured Evaluation | 15–35 min | JSON output + rubric + CoT + oath → `evaluate()` |
| 3. Grounding & Critique | 35–55 min | Reference-aware + few-shot + adversarial → `critique()` |
| 4. Comparison Modes & Bias | 55–70 min | Pairwise + listwise + bias detection & debiasing |
| 5. Reliability & Consistency | 70–85 min | Self-consistency + confidence thresholds + claim decomposition |
| 6. Multi-Judge Architectures | 85–100 min | Ensemble + specialized + meta-judge + cascading + LLM Council |
| 7. Advanced Techniques | 100–112 min | Dynamic rubrics + hallucination detection + domain adaptation |
| 8. Production & Benchmarking | 112–118 min | Human baselines + monitoring + audit trails |
| 9. Wrap-Up | 118–120 min | Complete `LLMJudge` class + cheat sheet + resources |

## Quick Start

### Prerequisites

- Python 3.9+
- An LLM provider (any one of the following):
  - **Ollama** (local, free) — recommended for workshop
  - **OpenAI** API key
  - **Anthropic** API key
  - **Groq** API key (free tier available)

### Setup

```bash
# 1. Clone the repository
git clone https://github.com/afzal-mukhtar/llm-as-a-judge.git
cd llm-as-a-judge

# 2. Install dependencies
pip install -r requirements.txt

# 3. (If using Ollama) Pull a model
ollama pull llama3.1:8b

# 4. Open the workshop notebook
jupyter notebook notebooks/workshop.ipynb
```

Change the `MODEL` variable in the first cell to match your provider:
```python
MODEL = "ollama/llama3.1:8b"          # Local Ollama
MODEL = "gpt-4o-mini"                 # OpenAI
MODEL = "anthropic/claude-3-haiku"    # Anthropic
MODEL = "groq/llama-3.1-8b-instant"  # Groq
```

## Project Structure

```
llm-as-a-judge/
├── notebooks/
│   └── workshop.ipynb                 # THE build-along notebook (45 cells)
├── datasets/
│   ├── eval_test_cases.json           # 12 curated cases (easy → adversarial)
│   ├── pairwise_cases.json            # 6 A-vs-B comparison pairs
│   ├── listwise_cases.json            # 3 sets of 4 answers to rank
│   ├── hallucination_cases.json       # 5 cases with subtle factual errors
│   ├── multi_turn_cases.json          # 3 conversation evaluation cases
│   └── human_baseline.json            # Human expert scores for benchmarking
├── src/
│   └── prompts.py                     # Prompt library (reference)
├── cheatsheet.md                      # One-page technique quick reference
├── requirements.txt
└── archive/                           # Previous workshop versions
```

## Technique Categories

- **Foundational Modes** (#1-5): Binary, Likert, pointwise, pairwise, listwise
- **Prompt Engineering** (#6-14): Structured output, rubric, CoT, oath, few-shot, reference-grounded, adversarial, contrastive
- **Bias Detection & Mitigation** (#15-20): Position, length, sycophancy, anchor bias
- **Reliability & Consistency** (#21-27): Self-consistency, temperature sensitivity, confidence calibration, component extraction, claim decomposition
- **Multi-Judge Architectures** (#28-34): Same-model ensemble, cross-model, specialized judges, meta-judge, cascading, LLM Council
- **Advanced Techniques** (#35-41): Dynamic rubrics, calibrated anchors, domain adaptation, multi-turn eval, hallucination detection
- **Production & Operations** (#42-46): Human benchmarking, drift monitoring, cost optimization, audit trails, human-in-the-loop

See [cheatsheet.md](cheatsheet.md) for the complete quick reference.

## Bonus: Multi-LLM Deliberation

The workshop includes a bonus section covering:

- **Karpathy's LLM Council** -- How anonymized peer review across multiple models eliminates inter-model bias (3-stage: first opinions, anonymized ranking, chairman synthesis)

## License

MIT