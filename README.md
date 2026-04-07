# Model Quality Rubric ✅

You can't improve what you don't measure. This is a deterministic scoring framework that evaluates an LLM's response across seven dimensions and returns a consistent score from 0 to 1. No magic, no black boxes. Just a ruleset you can run, tweak, and trust.

A live public test endpoint is running. POST a prompt and response pair as JSON to:
```
https://the-fleet.casey-digennaro.workers.dev/rubric/test
```

## Why This Exists
Every team ends up building a quality checker. You spend weeks defining "good output," then write fragile code that later breaks. This is the boring, reliable baseline. It works well enough that you won't need to start from scratch.

## Quick Start
1.  **Fork this repository.** Change whatever you want.
2.  Copy the `rubric.js` file into your project. No installs required.
3.  Call `evaluateResponse(prompt, response)`. Get a full score breakdown in under 3ms.
4.  Tune the weights or rewrite criteria for your use case.

## Key Features
*   **Transparent Rules:** Every scoring check is defined in a plain config object. You can read every line that produces a score.
*   **Zero Dependencies:** Runs unmodified on Cloudflare Workers, Node.js, browsers, and edge runtimes.
*   **Deterministic:** Same prompt and response always returns the exact same score. No randomness.
*   **Fleet Native:** Outputs machine-readable JSON for automated routing, fine-tuning, and guardrails in Cocapn agent fleets.
*   **Pure Function:** No external API calls, telemetry, or side effects.
*   **Configurable:** Adjust dimension weights, add your own checks, or remove ones you don't need.

## What Makes This Different
1.  This is not an LLM judge. It does not call another model to score your model, so there are no extra costs, latency, or hidden hallucinations in the scoring layer.
2.  This is built for production. You can score every response your fleet generates at request volume.
3.  This is not a product. You fork it, you own it. There is no API key, paywall, or forced update.

## Limitations
The scoring is based on explicit, rule-based checks. It cannot understand nuanced context, irony, or sarcasm. For example, a factually incorrect statement meant as a joke will be penalized as a hallucination. Its accuracy is bounded by the clarity of its predefined rules.

## License
MIT

Attribution: Superinstance and Lucineer (DiGennaro et al.)

<div style="text-align:center;padding:16px;color:#64748b;font-size:.8rem"><a href="https://the-fleet.casey-digennaro.workers.dev" style="color:#64748b">The Fleet</a> &middot; <a href="https://cocapn.ai" style="color:#64748b">Cocapn</a></div>