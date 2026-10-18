# AI Content Quality Lab

**A portfolio-scale AI evaluation system for measuring, diagnosing, and improving generated enterprise content.**

This project grows a simple quality scorer into a layered AI quality architecture:

- **V1 — Transparent quality scoring**
- **V2 — Claim-level evidence evaluation + LLM-as-a-Judge interface**
- **V3 — Regression and evaluation test suite**
- **V4 — Interactive quality dashboard**
- **V5 — Retrieval-Augmented Generation (RAG) integration**
- **V6 — Marketing Knowledge Graph integration**

The goal is not to demonstrate another chatbot. It is to demonstrate how an AI content system can be made **measurable, inspectable, governable, and production-aware**.

## Architecture

```text
                         ┌──────────────────────────┐
                         │ Approved Content Corpus  │
                         └────────────┬─────────────┘
                                      │
                   ┌──────────────────┴──────────────────┐
                   │                                     │
                   v                                     v
          ┌─────────────────┐                  ┌──────────────────┐
          │ Vector / Lexical│                  │ Knowledge Graph  │
          │ Retrieval Layer │                  │ Context Layer    │
          └────────┬────────┘                  └────────┬─────────┘
                   └──────────────────┬──────────────────┘
                                      v
                            ┌───────────────────┐
                            │ Generation Layer  │
                            └─────────┬─────────┘
                                      v
                            ┌───────────────────┐
                            │ Claim Extraction  │
                            └─────────┬─────────┘
                                      v
                 ┌────────────────────┼────────────────────┐
                 v                    v                    v
          Groundedness          Factuality          Completeness
                 │                    │                    │
                 ├──────────────┬─────┴─────┬──────────────┤
                 v              v           v              v
             Relevance      Brand/Tone   Evidence      LLM Judge
                 └──────────────┬───────────┬──────────────┘
                                v
                       ┌─────────────────┐
                       │ Quality Score   │
                       └───────┬─────────┘
                               v
                  PASS / HUMAN REVIEW / FAIL
                               │
                               v
                     Regression + Dashboard
```

## What makes this a portfolio project

This repository demonstrates four levels of thinking at once:

1. **Content strategy:** translating editorial expectations into explicit quality dimensions.
2. **AI systems:** retrieval, grounding, claim evaluation, and model-based judging.
3. **Product/program thinking:** thresholds, human-review routing, failure modes, and regression gates.
4. **Knowledge architecture:** structured entities and relationships improve context beyond flat retrieval.

## Quick start

```bash
pip install -r requirements.txt
python src/run_pipeline.py
python tests/regression_suite.py
```

For the dashboard:

```bash
streamlit run dashboard/app.py
```

## Evaluation dimensions

| Dimension | Weight | What it tests |
|---|---:|---|
| Groundedness | 25% | Claims supported by approved evidence |
| Factual consistency | 20% | Contradictions / unsupported factual assertions |
| Completeness | 20% | Required information included |
| Relevance | 15% | Focus on the requested task |
| Brand/tone | 10% | Compliance with language rules |
| Citation/evidence | 10% | Traceability to evidence |

Decision policy:

- **85–100:** PASS
- **70–84:** HUMAN REVIEW
- **<70:** FAIL

## Version map

### V1 — Transparent scoring
Deterministic evaluators provide an inspectable baseline.

### V2 — Claim-level evidence + LLM Judge
Generated text is decomposed into claims. Each claim is matched to evidence. An optional judge interface is provided for model-based evaluation.

### V3 — Regression testing
A golden evaluation set defines expected decisions. Changes to prompts, models, retrieval, or evaluators can be tested before release.

### V4 — Dashboard
A Streamlit dashboard visualizes overall quality, dimension scores, decisions, and claim-level evidence.

### V5 — RAG
A lightweight local retriever demonstrates how retrieval quality affects generated-content quality. It intentionally avoids requiring a hosted vector database so the project is easy to run.

### V6 — Marketing Knowledge Graph
A small graph connects audiences, needs, products, capabilities, messages, evidence, assets, and channels. Graph context can supplement retrieval and reduce ambiguity.

## Enterprise-scale design

A production implementation would add:

- model-provider adapters
- embedding/vector infrastructure
- identity and permission-aware retrieval
- prompt/evaluator versioning
- human-review calibration
- observability and drift monitoring
- audit logs
- risk-tiered approval policies
- adversarial evaluation sets
- claim-level provenance
- cost and latency monitoring

See `docs/ENTERPRISE_SCALE.md` and `docs/TUTORIAL.md`.
