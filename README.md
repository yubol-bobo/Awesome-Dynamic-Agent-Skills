<div align="center">

# Awesome Dynamic Agent Skills [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

#### *They Are Not Static* — a curated reading list & companion to the survey on **dynamic, self-evolving skill systems for LLM agents**.

[**Project page**](https://yubol-bobo.github.io/Awesome-Dynamic-Agent-Skills/) ·
[**Paper (PDF)**](#paper) ·
[**Cite**](#citation) ·
[**Contribute**](#contributing)

[![GitHub stars](https://img.shields.io/github/stars/yubol-bobo/Awesome-Dynamic-Agent-Skills?style=social)](https://github.com/yubol-bobo/Awesome-Dynamic-Agent-Skills)
![Last update](https://img.shields.io/badge/Last%20update-2026--05-blue)
![Papers](https://img.shields.io/badge/Papers-94-success)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

</div>

---

> **TL;DR.** LLM agents externalize procedural knowledge into reusable *skills* — code, natural-language procedures, SKILL.md packages, graphs, parametric adapters. **Dynamic skill systems** treat the library itself as a learning object that grows, shrinks, repairs itself, and is sometimes distilled into weights. This list audits **94 papers** (2023–2026) through a unified lens: a 7-tuple skill formalism, an 8-stage lifecycle, and a **ten-operator algebra** $\{\text{Add, Refine, Merge, Split, Prune, Distill, Abstract, Compose, Rewrite, Rerank}\}$.

---

## Contents
- [Why dynamic skills?](#why-dynamic-skills)
- [The 7-tuple at a glance](#the-7-tuple-at-a-glance)
- [The eight-stage lifecycle](#the-eight-stage-lifecycle)
- [The ten-operator algebra](#the-ten-operator-algebra)
- [📚 Surveyed papers](#-surveyed-papers)
  - [Foundational](#foundational)
  - [Skill-aware RL](#skill-aware-rl)
  - [Lesson / heuristic memory](#lesson--heuristic-memory)
  - [Executable skill libraries](#executable-skill-libraries)
  - [Parametric / training-time](#parametric--training-time)
  - [Infrastructure & governance](#infrastructure--governance)
  - [Benchmarks & evaluation](#benchmarks--evaluation)
  - [Safety & audit](#safety--audit)
  - [Position papers & related surveys](#position-papers--related-surveys)
- [Seven empirical regularities](#seven-empirical-regularities)
- [Citation](#citation)
- [Contributing](#contributing)

---

## Why dynamic skills?

Many skill libraries are still treated as **static**: authored once, versioned rarely, and weakly connected to the trajectories that reveal whether a skill remains useful, safe, or correct. The 2025–2026 wave of work rejects this assumption — methods now **propose, verify, admit, organize, retrieve, maintain, distill, and govern** skills as a continuous loop. The central thesis of the survey:

> **Dynamic skill systems are lifecycle-managed, verified, evolving artifact stores for LLM agents.**

A skill artifact is *created from evidence, proposed as an edit, verified, admitted, organized, retrieved or composed, maintained, sometimes distilled, and governed through provenance and rollback*. Papers differ mainly in which stages they implement, which learning signal drives edits, and where they place the verifier.

---

## The 7-tuple at a glance

The canonical options 4-tuple $\langle C, \pi, T, R \rangle$ is extended for dynamic libraries:

$$
\mathcal{S}_t \;=\; \langle\, C_t,\; \pi_t,\; T_t,\; R_t,\; \boldsymbol{\varphi_t},\; \boldsymbol{\nu_t},\; \boldsymbol{\prec_t} \,\rangle
$$

where $\varphi$ is an **edit operator**, $\nu$ is the **admission verifier**, and $\prec$ is a **lineage** partial order. Lifted to the library:

$$
\mathcal{L}_{t+1} \;=\; \mathrm{Apply}\bigl(\vec{u}_t(\tau_t, r_t),\; \mathcal{L}_t\bigr)
$$

with trigger $\tau$, learning signal $r$, and an operator-vector $\vec{u}$ drawn from the algebra below.

---

## The eight-stage lifecycle

| # | Stage | Design question |
|---|-------|-----------------|
| 1 | **Evidence acquisition** | What observation justifies a library change? (trajectory, reward, failure, user edit, cross-user signal) |
| 2 | **Proposal** | How is evidence converted into a candidate edit? |
| 3 | **Verification & admission** | Should the candidate enter the library? As mature, tentative, quarantined, or rejected? |
| 4 | **Organization & storage** | flat · tree · DAG · graph · ontology · subspace · dual store |
| 5 | **Retrieval & composition** | Which artifacts influence the next action? |
| 6 | **Maintenance & repair** | Pruning, merging, splitting, reranking, refining, rewriting |
| 7 | **Distillation & portability** | Move procedural knowledge between artifacts, weights, agents, users |
| 8 | **Governance & provenance** | Lineage, authorship, safety checks, release state, rollback |

The **admission gate (stage 3)** is the most important boundary — dynamic systems generate plausible skills cheaply, but the library only improves when admission filters them with an appropriate verifier.

---

## The ten-operator algebra

| Op | Name | What it does | Representative |
|:--:|------|------|------|
| **A** | Add | Insert a new skill | Voyager · SAGE |
| **R** | Refine | Edit content without changing the interface | Memento · PSN |
| **M** | Merge | Combine multiple skills | Trace2Skill · AutoRefine |
| **S** | Split | Factor one skill into reusable components | SkillX |
| **P** | Prune | Remove or quarantine | Wild-Skills · ClawSafety |
| **D** | Distill | Compress trajectories into a skill | CASCADE · MUSE |
| **B** | Abstract | Lift a concrete procedure to a template | CUA-Skill · CoEvoSkills |
| **C** | Compose | Chain skills into a verified composite | SkillCraft · SkillOrchestra |
| **W** | Rewrite | Change body and possibly interface | EvolveR |
| **K** | Rerank | Change retrieval priors without changing content | SkillRouter |

> Almost no system supports all ten operators. The supported subset is one of the clearest taxonomic fingerprints.

---

## 📚 Surveyed papers

> Format: **`Name`** · arXiv link · year · operators · *one-line headline*

### Foundational

- **Voyager** — [arXiv:2305.16291](https://arxiv.org/abs/2305.16291) · 2023 · `A` · *Open-ended embodied agent; 3.3× items, 15.3× tech-tree progress over baselines.*
- **LATM** — [arXiv:2305.17126](https://arxiv.org/abs/2305.17126) · 2023 · `A` · *Tool-maker + tool-user beats few-shot.*
- **SoK-Skills** — [arXiv:2602.20867](https://arxiv.org/abs/2602.20867) · 2026 · *Position: agentic skills beyond tool use; the 4-tuple foundation we extend.*
- **Sutton, Precup & Singh (1999)** — *Between MDPs and Semi-MDPs: Options framework.* [DOI](https://doi.org/10.1016/S0004-3702(99)00052-1)

### Skill-aware RL

- **SAGE** — [arXiv:2512.17102](https://arxiv.org/abs/2512.17102) · 2025 · `A,R` · *Skill-integrated RL on AppWorld.*
- **SkillRL** — [arXiv:2602.08234](https://arxiv.org/abs/2602.08234) · 2026 · `A,D` · *Hierarchical skill-conditioned RL.*
- **AgentEvolver** — [arXiv:2511.10395](https://arxiv.org/abs/2511.10395) · 2025 · `A,R,D` · *Self-question / navigate / attribute.*
- **CODE-SHARP** — [arXiv:2602.10085](https://arxiv.org/abs/2602.10085) · 2026 · `A,R,M,W` · *4 mutations + prereq DAG; 24.3% → 41.0% under a learned gate.*
- **Agentic-Proposing** — [arXiv:2602.03279](https://arxiv.org/abs/2602.03279) · 2026 · `A,R,P,D,B,C` · *91.6% on AIME-25 with a 30B model and 11K trajectories.*
- **COS-PLAY** — [arXiv:2604.20987](https://arxiv.org/abs/2604.20987) · 2026 · `A,R,P,D` · *Co-evolves decision policy + skill bank.*
- **MAGELLAN** — *ICML 2025* · `A,D` · *Metacognitive predictions of learning progress for autotelic agents.*

### Lesson / heuristic memory

- **ERL** — [arXiv:2603.24639](https://arxiv.org/abs/2603.24639) · 2026 · `A,R` · *Task-end retrospective lessons.*
- **RetroAgent** — [arXiv:2603.08561](https://arxiv.org/abs/2603.08561) · 2026 · `A,R` · *Dual intrinsic feedback (solve → evolve).*
- **MUSE** — [arXiv:2510.08002](https://arxiv.org/abs/2510.08002) · 2025 · `A,R,D` · *Long-horizon productivity memory.*
- **EvolveR** — [arXiv:2510.16079](https://arxiv.org/abs/2510.16079) · 2025 · `A,R,W` · *Strategic-principle evolution.*
- **Memento** — [arXiv:2603.18743](https://arxiv.org/abs/2603.18743) · 2026 · `A,R,K` · *Case memory + SKILL.md rerank — let agents design agents.*
- **XSkill** — [arXiv:2603.12056](https://arxiv.org/abs/2603.12056) · 2026 · `A,R,M,P,B,K` · *Visual dual skill / experience store for multimodal agents.*
- **SAGER** — [arXiv:2604.14972](https://arxiv.org/abs/2604.14972) · 2026 · `A,R,W` · *Per-user policy skills for recommendation.*
- **CASCADE** — [arXiv:2512.23880](https://arxiv.org/abs/2512.23880) · 2025 · `A,D,P` · *Cumulative scientific skill consolidation.*
- **SimpleMem** — [arXiv:2601.02553](https://arxiv.org/abs/2601.02553) · 2026 · `A,D` · *Efficient lifelong memory; write-time semantic compression.*

### Executable skill libraries

- **SkillWeaver** — [arXiv:2504.07079](https://arxiv.org/abs/2504.07079) · 2025 · `A,R,P` · *Web agents self-improve via Propose · Practice · Verify · Hone.*
- **AgentFactory** — [arXiv:2603.18000](https://arxiv.org/abs/2603.18000) · 2026 · `A,R,C` · *Subagents as evolvable, executable skills.*
- **EvoSkill** — [arXiv:2603.02766](https://arxiv.org/abs/2603.02766) · 2026 · `A,R,P` · *Failure-driven proposal + Pareto-front admission; +12.1 pts SealQA.*
- **CoEvoSkills** — [arXiv:2604.01687](https://arxiv.org/abs/2604.01687) · 2026 · `A,R,B` · *Co-evolving verifier loop; 71.1% → 41.1% without surrogate verifier.*
- **PSN** — [arXiv:2601.03509](https://arxiv.org/abs/2601.03509) · 2026 · `A,R,M,W,K,P` · *Programmatic Skill Networks — 5 refactors + symbolic credit.*
- **SkillCraft** — [arXiv:2603.00718](https://arxiv.org/abs/2603.00718) · 2026 · `A,C,R` · *Verified compositional MCP skills.*
- **Live-SWE-agent** — [arXiv:2511.13646](https://arxiv.org/abs/2511.13646) · 2025 · `A,R` · *Runtime scaffold synthesis.*
- **SkillX** — [arXiv:2604.04804](https://arxiv.org/abs/2604.04804) · 2026 · `A,S,B,K` · *Automatic hierarchical library construction.*
- **Trace2Skill** — [arXiv:2603.25158](https://arxiv.org/abs/2603.25158) · 2026 · `A,M,D` · *Prevalence-weighted consolidation of trajectory-local lessons.*
- **SkillClaw** — [arXiv:2604.08377](https://arxiv.org/abs/2604.08377) · 2026 · `A,R,M,K` · *Cross-user skill evolution with an agentic evolver.*
- **AutoSkill** — [arXiv:2603.01145](https://arxiv.org/abs/2603.01145) · 2026 · `A,R` · *Training-free personalized skill bank.*
- **AutoRefine** — [arXiv:2601.22758](https://arxiv.org/abs/2601.22758) · 2026 · `A,R,M` · *Dual-form skills + maintenance; without maintenance util. 0.71 → 0.08.*
- **MemSkill** — [arXiv:2602.02474](https://arxiv.org/abs/2602.02474) · 2026 · `A,R,K` · *Meta-memory skill banks.*
- **Wild-Skills** — [arXiv:2604.04323](https://arxiv.org/abs/2604.04323) · 2026 · `A,P,K` · *Skill utility under realistic 34K-pool retrieval.*
- **CUA-Skill** — [arXiv:2601.21123](https://arxiv.org/abs/2601.21123) · 2026 · `A,B` · *Parameterized GUI skills for computer-using agents.*
- **SkillFoundry** — [arXiv:2604.03964](https://arxiv.org/abs/2604.03964) · 2026 · `A,R,M,P,B` · *Scientific contracts + provenance.*
- **SkillForge** — [arXiv:2604.08618](https://arxiv.org/abs/2604.08618) · 2026 · `A,R,W` · *Failure diagnosis & evolution in cloud technical support.*
- **SkillMOO** — [arXiv:2604.09297](https://arxiv.org/abs/2604.09297) · 2026 · `R,P,K` · *Pareto pass/cost optimization for SE skills.*
- **Bilevel-MCTS** — [arXiv:2604.15709](https://arxiv.org/abs/2604.15709) · 2026 · `R,W` · *MCTS over skill package structure.*
- **Metasurface-Agent** — [arXiv:2604.01480](https://arxiv.org/abs/2604.01480) · 2026 · `A,R` · *Physics-verified self-evolving scientific skills.*
- **EvoAgent** — [arXiv:2604.20133](https://arxiv.org/abs/2604.20133) · 2026 · `A,R,K,C` · *Multi-file skills + delegation.*
- **MACRO** — [arXiv:2603.05860](https://arxiv.org/abs/2603.05860) · 2026 · `A,C,D` · *Discovers composite medical-imaging tools.*

### Parametric / training-time

- **SELAUR** — [arXiv:2602.21158](https://arxiv.org/abs/2602.21158) · 2026 · `D` · *Uncertainty-reshaped failure rewards.*
- **SKILL0** — [arXiv:2604.02268](https://arxiv.org/abs/2604.02268) · 2026 · `D,B` · *Helpfulness-decaying curricula → in-context skill internalization.*
- **LSE** — [arXiv:2603.18620](https://arxiv.org/abs/2603.18620) · 2026 · `D,R` · *Trained prompt-context evolution.*
- **SkillsCrafter** — [arXiv:2603.05160](https://arxiv.org/abs/2603.05160) · 2026 · `D,M,K` · *LoRA bank + semantic subspace for lifelong manipulation.*
- **K²-Agent** — [arXiv:2603.00676](https://arxiv.org/abs/2603.00676) · 2026 · `A,R,D` · *Co-evolving know-what / know-how for hierarchical mobile control.*
- **MetaClaw** — [arXiv:2603.17187](https://arxiv.org/abs/2603.17187) · 2026 · `A,R,D` · *Fast-skill / slow-weight adaptation in the wild.*
- **Co-Evolving Agents** — [arXiv:2511.22254](https://arxiv.org/abs/2511.22254) · 2025 · `A,D,P` · *Hard-negative failure training.*
- **Agent0** — [arXiv:2511.16043](https://arxiv.org/abs/2511.16043) · 2025 · `A,D` · *Zero-data curriculum-executor co-evolution.*
- **Tool-R0** — [arXiv:2602.21320](https://arxiv.org/abs/2602.21320) · 2026 · `A,D` · *Dual self-play for tool use from zero data.*
- **SCALAR** — [arXiv:2603.09036](https://arxiv.org/abs/2603.09036) · 2026 · `D,B` · *LLM-guided symbolic planning + RL grounding.*
- **ARISE** — [arXiv:2603.16060](https://arxiv.org/abs/2603.16060) · 2026 · `D,K` · *Agent reasoning with intrinsic skill evolution; swarm PPO + PSO.*
- **EXIF** — [arXiv:2506.04287](https://arxiv.org/abs/2506.04287) · 2025 · `D,B` · *Exploration-first skill discovery.*

### Infrastructure & governance

- **AgentSkillOS** — [arXiv:2603.02176](https://arxiv.org/abs/2603.02176) · 2026 · `A,C,S,P,K` · *Capability tree + DAG orchestration at ecosystem scale.*
- **SkillRouter** — [arXiv:2603.22455](https://arxiv.org/abs/2603.22455) · 2026 · `K` · *Full-text retrieve-and-rerank over 80K skills.*
- **SkVM** — [arXiv:2604.03088](https://arxiv.org/abs/2604.03088) · 2026 · `A,R,C` · *Language VM for skills across heterogeneous LLMs and harnesses.*
- **SkillNet** — [arXiv:2603.04448](https://arxiv.org/abs/2603.04448) · 2026 · `A,K,P` · *Ontology + relation graph; create / evaluate / connect skills.*
- **SkillOrchestra** — [arXiv:2602.19672](https://arxiv.org/abs/2602.19672) · 2026 · `K,C` · *Skill handbooks for agent routing.*
- **SkillFlow (system)** — [arXiv:2504.06188](https://arxiv.org/abs/2504.06188) · 2025 · `K` · *Multi-stage community-skill retrieval.*
- **AutoAgent** — [arXiv:2603.09716](https://arxiv.org/abs/2603.09716) · 2026 · `A,R,C` · *Evolves tools, peers, and self.*
- **AgentDevel** — [arXiv:2601.04620](https://arxiv.org/abs/2601.04620) · 2026 · `A,R,K,P` · *Reframing self-evolving agents as release engineering.*
- **GEA** — [arXiv:2602.04837](https://arxiv.org/abs/2602.04837) · 2026 · `A,R,M` · *Group-evolving agents via experience sharing.*
- **Single-Agent w/ Skills** — [arXiv:2601.04748](https://arxiv.org/abs/2601.04748) · 2026 · `A,M,D,P` · *When a single skill-using agent replaces multi-agent systems.*
- **EffiSkill** — [arXiv:2603.27850](https://arxiv.org/abs/2603.27850) · 2026 · `A,B,K` · *Mined operator skills for code efficiency.*
- **Graph of Skills** — [arXiv:2604.05333](https://arxiv.org/abs/2604.05333) · 2026 · `K,C` · *Dependency-aware structural retrieval at 200–2,000 skills.*
- **GraSP** — [arXiv:2604.17870](https://arxiv.org/abs/2604.17870) · 2026 · `C,R` · *Typed DAG composition + repair.*
- **Skilldex** — [arXiv:2604.16911](https://arxiv.org/abs/2604.16911) · 2026 · `A,K,P` · *Package manager and registry with hierarchical scope distribution.*
- **Corpus2Skill** — [arXiv:2604.14572](https://arxiv.org/abs/2604.14572) · 2026 · `A,S,K` · *Don't retrieve, navigate — enterprise QA via navigable skills.*
- **SkillRepoMining** — [arXiv:2603.11808](https://arxiv.org/abs/2603.11808) · 2026 · `A,B` · *Mining open-source agentic repositories for SKILL.md packages.*
- **SkillGraph** — [arXiv:2604.17503](https://arxiv.org/abs/2604.17503) · 2026 · `C,K` · *Multimodal collab. graph topology.*
- **Experience-Compression** — [arXiv:2604.15877](https://arxiv.org/abs/2604.15877) · 2026 · `D,B,K` · *Unifying memory · skills · rules across the compression spectrum.*

### Benchmarks & evaluation

- **SkillFlow-Bench** — [arXiv:2604.17308](https://arxiv.org/abs/2604.17308) · 2026 · *Lifelong skill discovery & evolution; 166 tasks, 20 task families.*
- **SkillsBench** — [arXiv:2602.12670](https://arxiv.org/abs/2602.12670) · 2026 · *How well agentic skills work across diverse tasks.*
- **SkillLearnBench** — [arXiv:2604.20087](https://arxiv.org/abs/2604.20087) · 2026 · *Continual learning for agent skill generation on real tasks.*
- **AgentSkills-Data** — [arXiv:2602.08004](https://arxiv.org/abs/2602.08004) · 2026 · *Data-driven analysis of 40K+ public Claude skills.*
- **ProEvolve** — [arXiv:2603.05910](https://arxiv.org/abs/2603.05910) · 2026 · *Programmable evolution for agent benchmarks.*
- **LifelongAgentBench** — [arXiv:2505.11942](https://arxiv.org/abs/2505.11942) · 2025 · *LLM agents as lifelong learners.*
- **ELL** — [arXiv:2508.19005](https://arxiv.org/abs/2508.19005) · 2025 · *Experience-driven lifelong-learning framework + benchmark.*

### Safety & audit

- **ASG-SI** — [arXiv:2512.23760](https://arxiv.org/abs/2512.23760) · 2025 · `A,R,P,D` · *Audited skill graph + verifiable rewards.*
- **ClawSafety** — [arXiv:2604.01438](https://arxiv.org/abs/2604.01438) · 2026 · `P` · *"Safe" LLMs, unsafe agents — highest-ASR vector in personal agents.*
- **Secure-Skills** — [arXiv:2604.02837](https://arxiv.org/abs/2604.02837) · 2026 · `P` · *Architecture, threat taxonomy, security analysis.*
- **Supply-Chain Poisoning** — [arXiv:2604.03081](https://arxiv.org/abs/2604.03081) · 2026 · `P` · *DDIPE poisoning attacks on coding-agent ecosystems.*
- **SkillSieve** — [arXiv:2604.06550](https://arxiv.org/abs/2604.06550) · 2026 · `P` · *Hierarchical malicious-skill triage.*
- **SkillAttack** — [arXiv:2604.04989](https://arxiv.org/abs/2604.04989) · 2026 · `P` · *Automated red teaming through attack-path refinement.*
- **BadSkill** — [arXiv:2604.09378](https://arxiv.org/abs/2604.09378) · 2026 · `P` · *Backdoors via model-in-skill poisoning.*
- **CredLeak** — [arXiv:2604.03070](https://arxiv.org/abs/2604.03070) · 2026 · `P` · *Cross-modal credential leakage at scale.*
- **HarmfulSkillBench** — [arXiv:2604.15415](https://arxiv.org/abs/2604.15415) · 2026 · `P` · *How harmful skills weaponize agents.*
- **SkillStealing** — [arXiv:2604.21829](https://arxiv.org/abs/2604.21829) · 2026 · `K` · *Black-box skill extraction from proprietary LLM agents.*
- **Malicious-or-Not** — [arXiv:2603.16572](https://arxiv.org/abs/2603.16572) · 2026 · `P` · *Adding repository context to skill classification.*
- **MedSkillAudit** — [arXiv:2604.20441](https://arxiv.org/abs/2604.20441) · 2026 · `P,R` · *Domain-specific audit framework for medical-research skills.*

### Position papers & related surveys

- **AgentSkills-LLMs** — [arXiv:2602.12430](https://arxiv.org/abs/2602.12430) · 2026 · *Architecture · acquisition · security · path forward.*
- **Self-Evolving AI Agents (survey)** — [arXiv:2508.07407](https://arxiv.org/abs/2508.07407) · 2025 · *Bridging foundation models and lifelong agentic systems.*
- **Lifelong Learning of LLM-based Agents (roadmap)** — [arXiv:2501.07278](https://arxiv.org/abs/2501.07278) · 2025

---

## Seven empirical regularities

| # | Regularity | One-line evidence |
|--:|------------|-------------------|
| **R1** | Curated skills outperform unverified self-generated skills. | EvoSkill +12.1 pts on SealQA; CoEvoSkills 71.1% → 41.1% without surrogate verifier. |
| **R2** | Verification quality is often decisive in skill-aware RL. | CODE-SHARP 24.3% → 41.0%; Agentic-Proposing 68.7% → 82.3% problem validity. |
| **R3** | Flat retrieval drops around 64–128 skills. | Single-Agent-Skills sweep: 96–98% (16–32) → 78% (128) → 64% (256). |
| **R4** | Larger relative gains for weaker backbones. | SkillWeaver, MetaClaw, EvoSkill, Agentic-Proposing all converge on this pattern. |
| **R5** | Focused libraries often beat comprehensive ones. | SkillX hierarchies > flat; Wild-Skills filtering > raw inclusion. |
| **R6** | Maintenance becomes load-bearing at scale. | AutoRefine: pass 35.6% → 31.1%, 4.5× repo, util 0.71 → 0.08 without prune+merge. |
| **R7** | Write-time abstraction usually beats read-time only. | SimpleMem: removing write-time compression drops LoCoMo F1 43.24 → 31.29. |

> **Cross-cutting observation.** Admission, RL verifier quality, maintenance, and write-time abstraction are all forms of **write-time discipline**. Skill *usage* is not skill *utility*.

---

## Citation

If you use this list or the survey, please cite:

```bibtex
@article{li2026dynamicskills,
  title   = {They Are Not Static: A Survey of Dynamic Agent Skills},
  author  = {Li, Yubo},
  journal = {arXiv preprint},
  year    = {2026},
  url     = {https://github.com/yubol-bobo/Awesome-Dynamic-Agent-Skills}
}
```

---

## Contributing

Spotted a missing paper? Wrong category? An out-of-date result? **PRs welcome.** Please:

1. Open an [issue](https://github.com/yubol-bobo/Awesome-Dynamic-Agent-Skills/issues) or PR with the arXiv link, year, and a one-line headline.
2. Pick a section (or propose a new one).
3. If the paper is method-y, also tell us which operators it implements — we use the ten-letter algebra on the project page.

The taxonomy fields (cluster · artifact · clock · trigger · operators · signal · storage) live inline in [`index.html`](index.html) — keep `README.md` and that data block in sync.

---

<div align="center">

Maintained by **[Yubo Li](https://github.com/yubol-bobo)** · Carnegie Mellon University · `yubol@andrew.cmu.edu`

If you find this useful, consider giving the repo a ⭐ — it helps others discover the survey.

</div>
