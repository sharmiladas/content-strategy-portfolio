# Tutorial: Building an AI Content Quality System

## 1. Start with quality as a system requirement

A common mistake is to treat “good output” as a prompt-writing problem. In production, quality is a system property. Source quality, retrieval, context construction, prompt behavior, model behavior, policies, and review workflows all influence the result.

This project therefore begins by defining measurable quality dimensions before selecting an evaluator.

## 2. Build a transparent baseline

V1 uses explicit rules for groundedness, factual consistency, completeness, relevance, brand/tone, and evidence support.

Why start here? Transparent checks expose assumptions. They also create a baseline against which model-based evaluators can later be calibrated.

## 3. Evaluate claims, not only documents

V2 splits generated text into claims and attempts to map each claim to approved evidence.

The important architectural shift is:

`document score → claims → evidence → claim decisions → aggregate score`

This supports provenance and makes reviewer decisions easier to explain.

## 4. Add an LLM judge carefully

An LLM judge is useful for semantic qualities that are difficult to express as rules. It should not become an unexplained single source of truth.

A stronger pattern combines deterministic signals, model-based judgments, and calibrated human review.

## 5. Turn examples into regression gates

V3 stores expected decisions in a golden set. Any change to prompts, models, retrieval, content, or evaluators can be rerun against the same cases.

This is the beginning of an AI quality CI/CD discipline.

## 6. Make quality observable

V4 adds a dashboard. Teams need to see trends across dimensions rather than only a single aggregate score.

In production, this would include evaluator version, model version, prompt version, corpus version, cost, latency, review overrides, and failure categories.

## 7. Connect evaluation to RAG

V5 adds retrieval. A generated answer cannot be more grounded than the context it receives.

Evaluate retrieval separately:
- Did we retrieve the right evidence?
- Was important evidence omitted?
- Did irrelevant evidence enter context?
- Did generation use the evidence correctly?

## 8. Add structured knowledge

V6 adds a marketing knowledge graph:

`Audience → Need → Product → Capability → Message → Evidence → Asset → Channel`

This helps an AI system reason over explicit relationships rather than depending entirely on semantic similarity.

## 9. Production pattern

A mature architecture combines retrieval, structured knowledge, generation, claim-level evidence, automated evaluation, human review, regression testing, and observability.

That is the core portfolio argument of this project: **AI content quality is an architecture problem, not merely a prompting problem.**
