# Jarvis Cognitive Architecture — Prior Art Declaration

**Inventor:** Adel El-Ouariachi
**Date of Invention:** March 2026
**First Public Disclosure:** March 7, 2026
**Repository:** [github.com/AdelElo13/Open-Jarvis](https://github.com/AdelElo13/Open-Jarvis)

---

This repository is a **public prior art declaration** for the Jarvis Cognitive Architecture — an autonomous macOS AI agent (238K lines Swift, 762 tools) implementing a multi-engine cognitive architecture with several novel architectural patterns and integrations.

## Purpose

This declaration establishes a timestamped public disclosure. Under 35 U.S.C. 102, publicly disclosed inventions cannot be patented by others after the disclosure date. This protects the open-source community's right to use these innovations.

## What Is Genuinely Novel

After prior art review, we distinguish between:

- **Novel architecture** — no known implementation exists in any AI agent framework
- **Novel combination** — individual techniques exist in research, but the specific integration into a production AI agent is new
- **Novel application** — known techniques applied to a new domain (autonomous AI agent systems)

We do **not** claim novelty for well-established concepts. See "What We Do Not Claim" below.

## Key Innovations

| # | Innovation | Category | What's New |
|---|-----------|----------|------------|
| 1 | **NeuromorphicPulseMesh** | Novel architecture | Single coordinated neural pulse replacing 88+ independent timers with priority, CPU, and idle gating |
| 2 | **CircadianLearner** | Novel architecture | Per-task per-hour adaptive scheduling that learns when background work is useful |
| 3 | **CognitiveMetabolism** | Novel architecture | 5 metabolic cognitive states (Focused/Diffuse/Flow/Consolidation/Creative) with distinct processing parameters |
| 4 | **Peer-to-Peer Cognitive Modulation** | Novel architecture | 5 cognitive systems cross-modulate each other via excitatory/inhibitory connections — resonance, not pipeline |
| 5 | **Cognitive Veto on Tools** | Novel combination | Tool gating based on cognitive appropriateness (domain trust, metabolic state), orthogonal to security policy |
| 6 | **ProcessSymbiosis (AXObserver)** | Novel approach | Semantic UI access via macOS Accessibility API vs screenshot+OCR+click used by all known "computer use" systems |
| 7 | **Free Energy Minimization Core** | Novel application | Production implementation of Friston's FEP in an AI agent with surprisal-based resource allocation |
| 8 | **SkillForge** | Novel combination | Full evolutionary lifecycle for AI-synthesized tools: fitness tracking, promotion, retirement, mutation |
| 9 | **FailureOracle** | Novel combination | Predictive P(failure) per tool step with time-aware, cascade-aware conditional risk modeling |
| 10 | **CounterfactualEngine** | Novel application | Post-execution regret computation against unchosen alternatives for systematic decision learning |

## What We Explicitly Do NOT Claim As Novel

These techniques are used in Jarvis but are well-established in existing research:

- **Bayesian uncertainty quantification** — standard in ML (see Springer survey, 2021)
- **Predictive coding / surprise-based learning** — active neuroscience research (arXiv:2308.07870)
- **Multi-agent adversarial evaluation** — D3, CourtEval, ChatEval frameworks exist
- **Probabilistic intent recognition** — mature robotics research (Jain et al., IROS 2018)
- **Absence/gap detection in LLMs** — multiple published papers (arXiv:2512.10273)
- **Per-user preference learning** — PReF, PLUS methods published
- **Tool reliability monitoring** — LangChain health-aware middleware in development
- **Side-effect verification** — Verity, SafeAgent address this space

Our contribution is the specific integration of these techniques into a unified cognitive architecture, not the individual techniques themselves.

## Full Declaration

See **[PATENTS.md](PATENTS.md)** for the complete technical description with implementation details and honest prior art comparison.

## License

All inventions disclosed under [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html). Commercial licensing available from the inventor.

**This document constitutes prior art under 35 U.S.C. 102.** Any subsequent patent application covering substantially similar concepts is anticipated by this disclosure.

---

*Adel El-Ouariachi — March 7, 2026*
