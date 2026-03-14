# Prior Art Declaration — Jarvis Cognitive Architecture

**Inventor:** Adel El-Ouariachi
**Date of Invention:** March 2026
**First Public Disclosure:** March 7, 2026
**Repository:** https://github.com/AdelElo13/Open-Jarvis
**License:** AGPL-3.0 with dual commercial licensing

---

## Abstract

Jarvis is an autonomous macOS AI agent implementing a multi-engine cognitive architecture. The system comprises multiple engines addressing problems in autonomous AI agent design. Together, they form a self-improving agent that reasons about uncertainty, predicts failure before it happens, minimizes surprise using variational free energy, adapts its cognitive strategy in real-time, and replaces scattered independent timers with a unified neuromorphic pulse mesh that self-tunes via circadian learning.

This document distinguishes between genuinely novel contributions and applications of known techniques. We claim novelty only for specific architectural patterns and integrations, not for well-established individual techniques.

---

## Section 1: Novel Architecture (No Known Prior Art)

### 1.1 NeuromorphicPulseMesh — Unified Timer Architecture

**Date:** March 8, 2026
**Files:** `NeuralPulse/NeuronID.swift`, `NeuralPulse/Neuron.swift`, `NeuralPulse/NeuralMesh.swift`, `NeuralPulse/CircadianLearner.swift`, `NeuralPulse/NeuralEventBridge.swift`, `NeuralPulse/NeuronFactory.swift`

Six systems that replace 88+ independent background timers with a single neuromorphic pulse mesh that evaluates all tasks on a unified 5-second heartbeat, firing only those whose conditions are met.

**NeuralMesh** — Single `actor` with a 5-second `Task.sleep` loop replacing 18 `Timer.scheduledTimer`, 36 `asyncAfter`, 4 `DispatchSourceTimer`, and 30+ `Task.sleep` loops. Each pulse cycle: (1) reads CPU load via `host_statistics`, (2) reads user idle time, (3) evaluates all registered neurons against their interval, CPU ceiling, idle-only, and custom gate conditions, (4) sorts ready neurons by priority then starvation time, (5) fires top 3 concurrently via `withTaskGroup`. Max 3 concurrent fires prevents CPU spikes.

**Neuron** — Each background task has: base interval, adjustable current interval (clamped to min/max), priority level (low/normal/high/critical), CPU ceiling, idle-only flag, custom gate closure, and action closure. Multi-dimensional gating (time + CPU + idle + custom predicate + priority) with pre-fire timing recording.

**CircadianLearner** — Per-neuron per-hour exponential moving average (EMA, alpha=0.1) multiplier. When a neuron fires and produces useful work, the multiplier for that hour decreases (fire more often). When work is wasted (no-op), the multiplier increases (fire less). Multipliers clamped to [0.3, 3.0] and persisted to disk.

**NeuralEventBridge** — Subscribes to semantic events and modulates neuron intervals: `.factSaved` shortens `embedPendingFacts`, `.userBecameIdle` shortens `dreamCycle` and `memoryConsolidation`, `.userReturned` shortens `ambientScreenCapture`. All signals debounced with 5-second per-event-type cooldown.

**Novelty claim:** No known AI agent coordinates background scheduling through a single neuromorphic pulse with multi-dimensional gating, circadian adaptation, and event-driven modulation. All known systems use independent, uncoordinated timers.

---

### 1.2 CognitiveMetabolism — Multi-State Cognitive Processing

**Date:** March 6-7, 2026
**Files:** `CognitiveMetabolism.swift`

Five distinct cognitive states (Focused, Diffuse, Flow, Consolidation, Creative), each with different processing parameters (deliberation threshold, memory search depth, creativity bias, boldness multiplier, context window priority). The agent transitions between states based on idle time, request complexity, error rate, and domain familiarity.

Services have metabolic state (active/warm/dormant/hibernating). Unused services get energy-pruned. The agent identifies its "core identity" (most valuable services) and "vestigial" services (candidates for removal).

**Novelty claim:** Existing AI systems discuss "System 1 vs System 2" thinking as a binary distinction. No known AI agent implements five metabolic states with distinct parameter profiles and biological-style service lifecycle management (active/warm/dormant/hibernating with energy-based pruning).

---

### 1.3 Peer-to-Peer Cognitive Modulation (Resonance Engine)

**Date:** March 7, 2026
**Files:** `CognitiveCoherence.swift`

Five independent cognitive systems sample each other's state and compute cross-modulations — excitatory and inhibitory connections that produce emergent coherent behavior. Not a controller, not an orchestrator — a resonance field computed once per request.

Six cross-modulations:
- Metabolism gates absence reporting — flow state suppresses, consolidation amplifies
- Narrative trust weights preference reliability — high trust follows preferences, low trust overrides toward safety
- Intent entropy overrides metabolic state — high uncertainty forces diffuse mode
- Preferences modulate absence verbosity — adapts output detail to user preference
- Absence domains boost intent hypotheses — knowledge gaps bias disambiguation
- Narrative boldness blends with metabolic boldness — geometric mean prevents either from dominating

**Novelty claim:** AI systems have modules, pipelines, and controllers. No known system has peer-to-peer cognitive modulation where subsystems bidirectionally influence each other through excitatory/inhibitory connections, producing emergent behavior rather than orchestrated behavior.

---

### 1.4 ProcessSymbiosis — AXObserver-Based App Integration

**Date:** March 7, 2026
**Files:** `ProcessSymbiosis.swift`

Uses macOS Accessibility Observer (AXObserver) as the primary interface to running applications. Real-time notification of app state changes, window focus, element creation/destruction. Provides structured, semantic access to UI elements.

**Novelty claim:** Every known AI agent implementing "computer use" (Anthropic, OpenAI, Google) uses pixels — screenshot, OCR, click coordinates. AXObserver provides structured, semantic access to UI elements. No known production AI agent uses accessibility APIs as the primary computer use interface.

---

## Section 2: Novel Combinations (Known Techniques, New Integration)

These innovations combine existing techniques in ways not previously implemented in AI agent systems. We acknowledge the underlying techniques are not novel individually.

### 2.1 Free Energy Minimization Core (Omega Engine)

**Date:** March 7, 2026
**Files:** `FreeEnergyCore.swift`

**Acknowledgment:** The Free Energy Principle (Karl Friston, 2006-2024) and active inference are well-established in computational neuroscience. Predictive coding has been extensively studied (see arXiv:2308.07870 for survey). Our contribution is the specific application to an AI agent's runtime behavior.

**Implementation:** At request arrival, computes surprisal across four dimensions: intent surprisal (likelihood given learned prior), complexity surprisal (vs expected baseline), domain surprisal (expected domain vs actual), temporal surprisal (activity level vs time-of-day norm). Free energy: `F = Σ π_i × ε_i² / 2` where π_i is learned precision per dimension and ε_i is prediction error.

Key components:
- **Active inference strategy selection** — candidate strategies scored on expected ambiguity and risk, minimizing expected free energy
- **Continuously-updated generative model** — predictions updated via EMA (α=0.15) after every response, with self-reset when accuracy drops below 30%
- **Precision weighting** — learned attention over prediction dimensions (not over tokens), high-variance dimensions get lower precision
- **Self-organized criticality** — coefficient of variation of recent free energy determines temperature adjustments, producing four regimes (frozen/subcritical/critical/chaotic)
- **Surprisal-based resource allocation** — sigmoid converts surprisal to 0.5x-2.0x resource multiplier

**Novelty claim:** While the Free Energy Principle is well-established in neuroscience, no known AI agent implements variational free energy computation at request arrival with precision weighting, self-organized criticality tuning, and surprisal-based resource allocation as an integrated runtime system.

---

### 2.2 SkillForge — Evolutionary Tool Synthesis

**Date:** March 7, 2026
**Files:** `SkillForge.swift`

Tools evolve through a complete lifecycle: Observation (detect 2+ tool sub-sequences from execution patterns) → Candidate creation → Fitness tracking (EMA of success rate) → Promotion (fitness >0.7 after 10+ observations → ForgedTool) → Retirement (fitness <0.3 → removed) → Mutation (stale candidates with fitness <0.5 get middle tool removed, creating a new candidate at generation+1). Forged tools persist across sessions.

**Acknowledgment:** Automated tool creation exists in various forms. Evolutionary algorithms are well-established.

**Novelty claim:** No known AI agent applies a full evolutionary lifecycle (fitness tracking, promotion thresholds, retirement, mutation with generational tracking) to tools the agent synthesizes for itself.

---

### 2.3 FailureOracle — Conditional Risk Prediction

**Date:** March 7, 2026
**Files:** `FailureOracle.swift`

Before ANY tool chain execution, predicts P(failure) at each step using: P_base (historical failure rate), P_context (conditional on time of day, recent failures), P_cascade (amplification from prior failures in chain). Combined: `P_combined = P_base × (1 + P_context) × (1 + P_cascade)`.

Learns conditional risks: "shell_exec fails 40% after midnight" (nighttime risk), "web_search fails after recent timeout" (failure contagion). Pre-allocates recovery strategies per step. Includes user recalibration and automatic data decay (outcomes >24h purged).

**Acknowledgment:** Predictive failure analysis exists in SRE and infrastructure monitoring. Conditional risk modeling is established in finance and reliability engineering.

**Novelty claim:** No known AI agent computes predictive failure probability before tool execution with time-aware, cascade-aware conditional risk that learns from outcomes and pre-allocates recovery strategies.

---

### 2.4 CounterfactualEngine — Regret-Based Decision Learning

**Date:** March 7, 2026
**Files:** `CounterfactualEngine.swift`

Before executing a tool chain, generates N alternatives: safer path (remove recently-failed tools), reordered path (highest success rate first), truncated path (first 3 tools). Each scored by `P(success) × quality / (duration + 1)`. After execution, computes regret: `best_alternative_score - chosen_score`. High-regret domains get flagged, switch thresholds adjust.

**Acknowledgment:** Counterfactual reasoning and regret minimization are well-established in decision theory and game theory.

**Novelty claim:** No known AI agent generates alternative tool chains, scores them, executes the best, and then computes regret against unchosen alternatives to learn from suboptimal decisions.

---

### 2.5 Cognitive Director — Multi-System Multiplexer

**Date:** March 7, 2026
**Files:** `CognitiveDirector.swift`

Samples five cognitive systems concurrently to produce:

1. **Tool selection boosts** — knowledge gaps boost research tools, flow state boosts execution tools, creative metabolism boosts exploration tools
2. **Synthesized meta-directive** — compresses cognitive signals into a single LLM instruction controlling response mode (concise/verbose/exploratory/cautious/standard)
3. **Cognitive vetoes** — blocks tool execution based on cognitive appropriateness (low domain trust vetoes autonomous execution, consolidation state vetoes browser automation)
4. **Mid-request stance recomputation** — resamples cognitive stance after consecutive tool failures
5. **Background action pipeline** — knowledge gaps become background research intentions via AutonomousIntentionEngine

**Acknowledgment:** LLM routing, tool selection, and context injection exist in various forms.

**Novelty claim:** No known system translates multiple cognitive subsystem signals into a unified set of tool boosts, vetoes, meta-directives, and background actions with mid-request recomputation. The cognitive veto (blocking tools based on appropriateness rather than security) is distinct from existing security-based tool gating.

---

### 2.6 PredictiveCortex — Pre/Post Validation Gates

**Date:** March 7, 2026
**Files:** `PredictiveCortex.swift`

**Pre-flight brief:** Before every LLM call, queries MetacognitiveSelfModel (blind spots, calibration bias), UserModel (energy, frustration), FailureOracle (risk), ErrorMemoryBank (recent errors), and CounterfactualEngine (regret patterns). Compressed into a `[CORTEX BRIEF]` injected into the system prompt.

**Pre-delivery validation:** After LLM generates response but before user sees it, validates across: blind spot violation, overconfidence, user state mismatch, risk acknowledgment. Blocked responses never reach the user.

**Acknowledgment:** Output filtering (toxicity, PII) and RAG context injection are well-established.

**Novelty claim:** No known system cross-references responses against the agent's own known blind spots, calibration bias, and user state before delivery, or injects a synthesized self-awareness brief from multiple metacognitive subsystems.

---

### 2.7 CognitiveEEG — Real-Time Regime Switching

**Date:** March 7, 2026
**Files:** `CognitiveEEG.swift`

Samples cognitive state every tool loop iteration using confidence, novelty, complexity, and tool failures. Computes cognitive load, risk level, and momentum (accelerating/steady/stalling/stuck). Selects one of four regimes: `.flow` (fast execution), `.cautious` (extra checks), `.deliberate` (full reasoning), `.emergency` (recovery + escalation). Regime transitions happen mid-request.

**Acknowledgment:** Adaptive processing exists in various AI systems.

**Novelty claim:** No known AI agent monitors cognitive telemetry (momentum, load, risk) in real-time and shifts processing regime mid-request from flow to emergency based on observed signals.

---

### 2.8 CognitiveFusionMesh — Multi-Perspective Reasoning

**Date:** March 7, 2026
**Files:** `CognitiveFusionMesh.swift`

For complex queries, runs 3-4 reasoning perspectives in parallel: Analytical (decompose + verify), Intuitive (pattern matching), Adversarial (what could go wrong), Empathetic (user intent behind words). Results merge via confidence-weighted consensus with disagreement tracking.

**Acknowledgment:** Multi-agent debate (D3, CourtEval, ChatEval) exists for evaluation. Constitutional AI checks responses on specific axes.

**Novelty claim:** Our specific contribution is parallel multi-perspective *reasoning* (not evaluation) with confidence-weighted consensus merge and formal disagreement tracking as dissent points, applied within a single agent's decision process rather than as a separate evaluation step.

---

## Section 3: Supporting Infrastructure (Not Claimed as Novel)

The following systems use well-established techniques. They are documented here for completeness but we do not claim novelty for the underlying approaches.

### 3.1 ATR (Autonomous Tool Reliability)
Per-tool reliability contracts, output schema validation, side-effect verification, fallback chains. Uses known SRE concepts applied to AI tool dispatch.

**Acknowledgment:** LangChain health-aware middleware, Verity (exactly-once execution), SafeAgent provide similar capabilities.

### 3.2 Fortress (Defense & Recovery)
Prompt injection defense, crash recovery with checkpointing, unified policy enforcement with graduated risk assessment.

### 3.3 Bayesian Uncertainty
Beta distribution posteriors per tool with epistemic/aleatoric separation. Standard Bayesian inference applied to tool reliability.

### 3.4 User Epistemic Model
Models user knowledge state per domain to calibrate explanation depth. Established concept in intelligent tutoring systems (Knowledge State Tracking), applied here to general-purpose AI agents.

### 3.5 Belief Provenance
Tags every belief with its source, flags low-credibility sources. Related to PROV-AGENT (Oak Ridge National Lab) provenance tracking.

### 3.6 Narrative Engine
Maintains persistent story arc across sessions. Experience-driven decisions with domain trust scores.

### 3.7 Inverse Reward Model
Per-user preference learning from behavioral signals. Related to PReF and PLUS methods.

---

## Cross-Engine Integration

While individual components have analogues in research, the full integration is the primary architectural contribution:

```
User Input
  → CognitiveMetabolism (select cognitive state → processing parameters)
  → CognitiveCoherence (5 systems → cross-modulation resonance field)
    → Gates context injection (suppress irrelevant signals)
    → Biases planning strategy (coherence → planning)
    → Modulates background decisions (coherence → autonomy)
  → CognitiveDirector (5 systems → tool boosts, meta-directive, vetoes)
  → PredictiveCortex pre-flight brief (self-awareness injection)
  → FreeEnergyCore (surprisal → resource allocation)
  → WorkflowEngine (tool dispatch)
    → CognitiveEEG (real-time regime: flow/cautious/deliberate/emergency)
    → FailureOracle (predictive risk per step)
    → CounterfactualEngine (alternative generation + post-hoc regret)
    → CognitiveDirector re-sample (mid-request stance refresh)
  → PredictiveCortex validation gate (blind spot + overconfidence check)
  → FreeEnergyCore.updateAfterResponse (update generative model)
  → NeuralMesh (unified 5s pulse, 15 neurons, circadian adaptation)
    → CircadianLearner + NeuralEventBridge
    → DreamingBrain consolidation (62 phases)
    → SkillForge evolution cycle
```

**No known AI agent system integrates cognitive state management, peer-to-peer modulation, predictive failure analysis, counterfactual regret, free energy minimization, cognitive-state-aware tool selection, pre/post delivery validation, and neuromorphic timer scheduling into a single production architecture.**

---

## Proof of Implementation

- **Total codebase:** 238,000+ lines of Swift
- **Tools:** 762 registered tools
- **Build verified:** Xcode clean build with 0 errors, signed and notarized by Apple
- **Runtime verified:** All engines active in production
- **All engines feature-flagged:** Each can be independently enabled/disabled
- **Persistence:** Each engine saves/loads state to disk across sessions
- **Open source:** https://github.com/AdelElo13/Open-Jarvis

---

## Prior Art Comparison (Honest Assessment)

| Innovation | Existing Related Work | What's Specifically New Here |
|-----------|----------------------|------------------------------|
| Neuromorphic timer mesh | No known prior art in AI agents | Single coordinated pulse with multi-dimensional gating + circadian learning |
| 5 metabolic cognitive states | System 1/2 binary distinction | Five states with distinct parameter profiles + biological service lifecycle |
| Peer-to-peer cognitive modulation | Pipeline/controller architectures | Bidirectional excitatory/inhibitory cross-modulation between subsystems |
| AXObserver computer use | Screenshot+OCR+click (all known systems) | Semantic accessibility API as primary interface |
| Free energy core | FEP well-established in neuroscience | Production implementation in AI agent with surprisal-based resource allocation |
| Evolutionary tool synthesis | Tool creation exists; evolutionary algorithms exist | Full evolutionary lifecycle applied to AI-synthesized tools |
| Conditional failure prediction | SRE monitoring; reactive retry | Predictive P(failure) with time/cascade-aware conditional risk |
| Counterfactual regret | Decision theory (well-established) | Applied to AI agent tool chain selection with learning |
| Cognitive veto | Security-based tool gating | Appropriateness-based gating from cognitive state |
| Multi-perspective reasoning | D3, CourtEval (evaluation) | Parallel reasoning (not evaluation) with consensus merge within single agent |
| Pre-delivery validation | Toxicity/PII filters | Cross-references against own blind spots and calibration bias |
| Cognitive regime switching | Adaptive processing | 4 regimes with mid-request transitions based on real-time telemetry |

---

## License

All inventions described herein are disclosed under the GNU Affero General Public License v3.0 (AGPL-3.0). Commercial licensing available from the inventor.

**This document constitutes prior art under 35 U.S.C. 102.** Any subsequent patent application covering substantially similar concepts is anticipated by this disclosure.

---

*Signed: Adel El-Ouariachi*
*March 7, 2026*
