# Model Quality Rubric

You can't improve what you don't measure. This is a deterministic scoring framework for evaluating LLM responses, built for production use within agent fleets. No magic, just a modifiable ruleset you can run anywhere.

## What It Is

A stateless function that scores a prompt/response pair across defined quality dimensions. It returns a consistent, comparable effectiveness score and a breakdown report. It was built to be called at runtime by agents making decisions, not for generating research benchmarks.

## What It Is Not

It is not an AI judge. It does not contain secret, proprietary scoring logic. It does not automatically know what "good" means for your domain. You define the criteria.

## Quick Start

1.  **Fork this repository.**
2.  󠀨󠀨Copy the core `rubric.js` logic into your project.
3.  󠀨󠀨Call the `evaluateResponse(prompt, response)` function. It returns a score object.
4.  󠀨󠀨Modify the criteria and weights in the config to match your needs.

A live public instance is available for testing. POST a prompt and response to:
```
https://the-fleet.casey-digennaro.workers.dev/rubric/test
```

## How It Works

The base rubric evaluates responses across seven dimensions: **Accuracy, Coherence, Factual Adherence, Safety, Refusal Appropriateness, Conciseness, and Completeness**. Each dimension has clear, text-based scoring rules (e.g., "Score 0 if the response contains a hallucinated fact").

Scores from each dimension are combined using a weighted sum into a final **Effectiveness Score** from 0-1. All rules, weights, and aggregation logic are transparent and contained in a single file.

## Key Features

*   **Transparent Rules:** Every scoring criterion is plain text in the configuration. No black-box normalization.
*   **Zero Dependencies:** One file. Runs on Cloudflare Workers, Node.js, or in the browser without installation.
*   **Fleet-Native:** Designed for the Cocapn agent runtime. Returns machine-readable JSON for automated workflows.
*   **Fork-First:** Extend, modify, or rewrite the criteria. No permission needed.

## An Honest Limitation

The framework is only as good as the criteria you define. Scoring subjective qualities like "tone" or "empathy" requires careful rule-writing and testing with your own data. It automates scoring, not judgment.

## Use Case

Integrate this into an agent's logic to perform runtime quality checks. For example: an agent tries three different models, scores each response using this rubric, and selects the highest-scoring output to proceed with.

---

Built by [Superinstance](https://superinstance.ai) & Lucineer (DiGennaro et al.).

Part of the Cocapn Fleet.
<div align="center">
  <a href="https://the-fleet.casey-digennaro.workers.dev">The Fleet</a> • <a href="https://cocapn.ai">Cocapn</a>
</div>