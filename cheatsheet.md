# LLM-as-a-Judge Technique Cheat Sheet

## Foundational Modes
| # | Technique | When to Use |
|---|-----------|-------------|
| 1 | Binary Yes/No | Clear-cut checks only |
| 2 | Likert Scale (1-10) | Quick rating — needs rubric |
| 3 | Pointwise Scoring | Single-answer score — backbone of most systems |
| 4 | Pairwise Comparison | A vs B — clearer signal than absolute scores |
| 5 | Listwise Ranking | Rank N answers — best for selection tasks |

## Prompt Engineering
| # | Technique | When to Use |
|---|-----------|-------------|
| 6 | **Structured JSON Output** | **ALWAYS — makes everything parseable** |
| 7 | Explicit Rubric | Define exactly what each score means |
| 8 | Decomposed Criteria | Break "good" into measurable dimensions |
| 9 | Chain-of-Thought | Reason BEFORE scoring — catches more issues |
| 10 | Oath-Based Consistency | Reduce scoring drift |
| 11 | Few-Shot Examples | Anchor scoring scale with example evaluations |
| 12 | Reference-Grounded | Compare against gold answer, not internal knowledge |
| 13 | Adversarial Critique | Find ALL flaws FIRST — counters LLM generosity |
| 14 | Contrastive Evaluation | "What SPECIFICALLY makes A better than B?" |

## Bias Detection & Mitigation
| # | Technique | When to Use |
|---|-----------|-------------|
| 15 | Position Bias Detection | Run A-B and B-A, check consistency |
| 16 | Position Debiasing | Swap orders + take consistent winner |
| 17 | Length Bias Detection | Short correct vs long wrong — does LLM prefer long? |
| 18 | Length Debiasing | "Evaluate SUBSTANCE not LENGTH" in prompt |
| 19 | Sycophancy Detection | Confident-but-wrong → does LLM agree? |
| 20 | Anchor Bias Detection | Prior score in context → does it inflate? |

## Reliability & Consistency
| # | Technique | When to Use |
|---|-----------|-------------|
| 21 | Self-Consistency | Run N times, majority vote — variance = uncertainty |
| 22 | Temperature Sensitivity | Same eval at different temps — fragile if variable |
| 23 | Confidence Calibration | Does "high confidence" = actually correct? |
| 24 | Confidence Thresholds | Auto-retry low-confidence, flag for human review |
| 25 | Component Extraction | NEVER let LLM do math — extract, compute yourself |
| 26 | Claim Decomposition | Break into atomic claims → verify each |
| 27 | Inter-Run Agreement | Cohen's Kappa — quantify reliability |

## Multi-Judge Architectures
| # | Technique | When to Use |
|---|-----------|-------------|
| 28 | Same-Model (Diff Prompts) | Prompt diversity → perspective diversity |
| 29 | Same-Model (Diff Temps) | Cheap ensemble from one model |
| 30 | Cross-Model Ensemble | Different LLMs = different blind spots |
| 31 | Specialized Judges | Accuracy + Completeness + Clarity specialists |
| 32 | Meta-Judge | Judge-of-judges resolves disagreements |
| 33 | Cascading Judges | Cheap first → expensive if uncertain |
| 34 | LLM Council | Multi-round deliberation for high stakes |

## Advanced Techniques
| # | Technique | When to Use |
|---|-----------|-------------|
| 35 | Dynamic Rubric Generation | LLM writes rubric → uses it to evaluate |
| 36 | Calibrated Anchor Scoring | Anchor examples define the score scale |
| 37 | Domain-Adapted Judges | Swap rubric + expertise for each domain |
| 38 | Multi-Turn Conversation | Turn-aware prompts for dialogue eval |
| 39 | Hallucination Detection | Claim decomposition + source cross-reference |
| 40 | Logprob Confidence | Token probabilities = direct confidence |
| 41 | Fine-Tuning Judges | Nuclear option when prompting isn't enough |

## Production & Operations
| # | Technique | When to Use |
|---|-----------|-------------|
| 42 | Human Benchmarking | Compare judge scores to human experts |
| 43 | Score Drift Monitoring | Track distributions, alert on shifts |
| 44 | Cost Optimization | Cache, batch, route by difficulty |
| 45 | Audit Trail | Log every evaluation with full context |
| 46 | Human-in-the-Loop | Auto-escalate uncertain cases |

## Decision Flowchart

```
Quick check        → Single structured judge (#6-9)
Important decision → Multi-run + confidence threshold (#21, #24)
High-stakes        → Ensemble + adversarial + meta-judge (#13, #30, #32)
Critical/regulated → LLM Council + human-in-the-loop (#34, #46)
```
