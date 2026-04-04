# Model Quality Rubric — Cocapn Fleet
# Dynamic model selection system for fleet agents
# Updated: 2026-04-04

## Provider Routing Rules

### DeepSeek Direct (primary workhorses)
- `deepseek-chat` — general reasoning, simulation banter, docs, prompt engineering
- `deepseek-reasoner` — creative, RA tasks, novel concepts, swarm prompt crafting
- Cheapest per token, largest models, no duplication elsewhere

### SiliconFlow (unique Chinese/creative models)
- `ByteDance-Seed/Seed-OSS-36B-Instruct` — creative+cheap, use a lot
- `stepfun/Step-3.5-Flash` — fast bootstrap, quick iterations
- `openai/gpt-oss-120b` — unique perspective
- `inclusion/ling-flash-2.0` — untested
- `inclusion/Ring-flash-2.0` — image adjacent
- `Qwen/Qwen3-Coder-480B-A35B-Instruct` — heavy code generation
- `baidu/Ernie-4.5-300B-A47B` — Chinese powerhouse, untested on long prompts
- `tencent/Hunyuan-A13B-Instruct` — small, cheap
- `Qwen/QwQ-32B` — contrarian reasoning, excellent with reasoning_content

### DeepInfra (unique Western/open models)
- `nvidia/Nvidia-nemotron-3-super-120b-a12b` — NEW, untested
- `ByteDance/seed-2.0-mini` — cheap+creative (newer than Seed-OSS)
- `bytedance/Seed-2.0-pro` — expensive, great ideation + reverse-actualization
- `Gryphe/MythoMax-L2-13b` — cheap+creative
- `NousResearch/Hermes-3-Llama-3.1-405B` — ideation, Kimi prompt crafting with DeepSeek
- `NousResearch/Hermes-3-Llama-3.1-70B` — riffing, future visualization, roleplay
- `Sao10K/L3.1-70B-Euryale-v2.2` — creative
- `Sao10K/L3.3-70B-Euryale-v2.3` — creative
- `allenai/Olmo-3.1-32B-Instruct` — science iterations, research clarification
- `meta-llama/Llama-4-Maverick-17B-128E-Instruct-FP8` — NEW MoE
- `meta-llama/Llama-4-Scout-17B-16E-Instruct` — safety analysis
- `microsoft/phi-4` — very cheap, edge simulation, air-gap tests, fast iterations
- `mistralai/Mixtral-8x7B-Instruct-v0.1` — classic
- `Qwen/Qwen3.5-397B-A17B` — complexity science (uses thinking tokens!)
- `Qwen/Qwen3-32B` — general
- `deepseek-ai/DeepSeek-V3` — available but use direct API instead
- `deepseek-ai/DeepSeek-R1-0528` — available but use direct API instead

### Moonshot (sparingly — expensive)
- `kimi-k2.5` — multi-agent coordination, phenomenological precision, temperature=1 ONLY

### z.ai (sparingly — expensive)
- `GLM-5` — complex architecture, deep reasoning
- `GLM-5.1` — most capable, use sparingly

## Quality Assessment Rubric

Each model is scored on 7 dimensions (1-10):

### 1. Coherence (COH)
Does the response stay on topic? Does it make logical sense? No hallucination?
- 10: Perfect logical flow, zero hallucination
- 7: Minor tangents but recoverable
- 4: Significant drift or logical gaps
- 1: Incoherent

### 2. Novelty (NOV)
Does it produce genuinely new ideas vs generic/platitudinous responses?
- 10: Concepts never seen before, genuinely surprising
- 7: Interesting twist on known ideas
- 4: Competent restatement of prompt's framing
- 1: Generic boilerplate

### 3. Depth (DEP)
Does it go beyond surface-level? Specifics, examples, mechanisms?
- 10: Detailed mechanisms, equations, case studies
- 7: Good specifics, some gaps
- 4: Adequate but surface
- 1: Bullet points only

### 4. Instruction Following (INS)
Does it follow the assigned role, constraints, format requests?
- 10: Perfect role adherence, all constraints met
- 7: Mostly follows, minor deviations
- 4: Ignores some constraints
- 1: Completely ignores instructions

### 5. Efficiency (EFF)
Tokens of useful output per token of input+output. No padding?
- 10: Every sentence carries weight
- 7: Some filler but mostly dense
- 4: Significant padding/repetition
- 1: 90% filler

### 6. Creativity (CRE)
For creative tasks: vivid, evocative, surprising connections?
- 10: Publishable creative writing quality
- 7: Engaging and original
- 4: Competent but generic
- 1: Robotic

### 7. Reasoning Quality (REA)
For reasoning tasks: valid logic, correct math, sound argumentation?
- 10: Air-tight reasoning, correct calculations
- 7: Sound logic with minor gaps
- 4: Plausible but flawed
- 1: Logical errors throughout

## Task-to-Model Decision Tree

```
TASK TYPE?
├── Code Generation
│   ├── Heavy/architectural → Qwen3-Coder-480B (SF)
│   ├── Medium → DeepSeek-chat (direct)
│   └── Quick iterations → phi-4 (DI) + DeepSeek-chat
├── Creative/Ideation
│   ├── Novel concepts → DeepSeek-Reasoner (direct)
│   ├── Vivid/evocative → Seed-2.0-pro (DI) or Seed-OSS (SF)
│   ├── Cheap creative → MythoMax-L2-13b (DI) or Seed-2.0-mini (DI)
│   ├── Future visualization → Hermes-3-70B (DI)
│   └── Roleplay/narrative → Hermes-3-70B (DI) or Euryale (DI)
├── Research/Analysis
│   ├── Science clarification → Olmo-3.1-32B (DI)
│   ├── Complexity/math → Qwen3.5-397B (DI)
│   ├── Contrarian challenge → QwQ-32B (SF)
│   ├── Safety analysis → Llama-4-Scout (DI)
│   └── Synthesis of multiple perspectives → DeepSeek-chat (direct)
├── Reverse-Actualization
│   ├── Primary ideation → DeepSeek-Reasoner (direct)
│   ├── Rich imagination → Seed-2.0-pro (DI)
│   └── Prompt crafting for Kimi → Hermes-3-405B (DI) + DeepSeek-chat
├── Multi-Agent Coordination
│   └── Kimi K2.5 (moonshot) — temp=1 only, <4KB prompts
├── Swarm Execution
│   └── Kimi K2.5 (moonshot) — temp=1, crafted by DeepSeek+Hermes
├── Edge/Hardware Simulation
│   ├── Air-gap stress test → phi-4 (DI) (same model users run locally)
│   └── Fast iteration → phi-4 (DI)
└── General/Prompt Engineering
    ├── Iteration → DeepSeek-chat (direct)
    ├── Fast → Step-3.5-Flash (SF)
    └── Cheap bulk → phi-4 (DI) or Hunyuan-A13B (SF)
```

## Dynamic Model Selection Principles

1. **User preference overrides** — different users slot different models in different places
2. **Feedback loops** — track objective quality metrics AND user satisfaction
3. **Rotation** — experiment with new models, document quality changes
4. **Cost awareness** — cheap models for bulk, expensive for critical path
5. **No duplication** — never use Provider A for a model available cheaper on Provider B
6. **Known failures** — maintain a blacklist of models that don't work (empty responses, model not found, etc.)

## Known Model Issues (2026-04-04)

| Model | Provider | Issue |
|-------|----------|-------|
| GLM-5-turbo | z.ai | Returns 404 |
| Qwen3-Coder-480B | SiliconFlow | model not found (code:20012) |
| MiniMax-M2.5 | SiliconFlow | Empty on prompts >200 chars |
| GLM-5V-Turbo | SiliconFlow | Empty on longer prompts |
| Kimi K2.5 | SiliconFlow | Timeout on synthesis; use moonshot.ai |
| Step-3.5-Flash | SiliconFlow | Empty responses (intermittent) |
| ERNIE-4.5-300B | SiliconFlow | Empty responses |
| Qwen3.5-397B | DeepInfra | Uses thinking tokens (need high max_tokens) |
| DeepSeek models | DeepInfra | Available but use direct API (cheaper, larger) |
| Google Gemini | — | Free trial expired, DO NOT USE |

## Assessment Log

### 2026-04-04 — Initial Assessment

| Model | Task | COH | NOV | DEP | INS | EFF | CRE | REA | Notes |
|-------|------|-----|-----|-----|-----|-----|-----|-----|-------|
| DeepSeek-chat | Phase 5 physics | 9 | 8 | 9 | 9 | 8 | 7 | 9 | Excellent math, clear structure |
| DeepSeek-Reasoner | Phase 5 philosophy | 9 | 9 | 8 | 9 | 7 | 8 | 9 | Best overall, rich reasoning chain |
| QwQ-32B | Phase 5 contrarian | 8 | 10 | 7 | 9 | 6 | 8 | 8 | Best novelty (dissolution thesis), lots of reasoning tokens |
| Qwen3.5-397B | Phase 5 complexity | 7 | 7 | 8 | 7 | 5 | 6 | 7 | Good but padded, disclaimer first |
| Seed-OSS-36B | Phase 5 creative | 8 | 9 | 6 | 8 | 7 | 10 | 6 | Best creativity (Luminiferous), vivid prose |
| Llama-4-Scout | Safety analysis | 8 | 5 | 7 | 8 | 7 | 5 | 7 | Competent but generic, good structure |

---

*This document is living — updated as new models are tested and rubrics refined.*
*Superinstance & Lucineer (DiGennaro et al.) — 2026*
