# Prior Art Declaration — Jarvis Cognitive Architecture

**Inventor:** Adel El-Ouariachi
**Date of Invention:** March 2026
**First Public Disclosure:** This document
**Repository:** https://github.com/AdelElo13/JarvisMacApp
**License:** AGPL-3.0 with dual commercial licensing (see NOTICE)

---

## Abstract

Jarvis is an autonomous macOS AI agent implementing a novel multi-engine cognitive architecture. The system comprises thirteen distinct engines, each addressing an unsolved problem in autonomous AI agent design. Together, they form a self-improving, self-healing, self-aware agent that learns from its own behavior, reasons about uncertainty, tracks causal chains, detects what's missing, predicts failure before it happens, minimizes surprise using variational free energy, validates its own responses against its known blind spots, adapts its cognitive strategy to the situation in real-time, and replaces scattered independent timers with a unified neuromorphic pulse mesh that self-tunes via circadian learning.

No known AI agent framework (LangChain, CrewAI, AutoGen, OpenAI Assistants, Anthropic Claude, Cursor, Devin, OpenClaw) implements any of these thirteen engines as described below.

---

## Engine 1: ATR (Autonomous Tool Reliability)

**Date:** March 6-7, 2026
**Files:** `ToolContract.swift`, `OutputSchemaValidator.swift`, `EffectVerifier.swift`, `SandboxTestPipeline.swift`

### 1.1 ToolContract — Declarative Per-Tool Reliability Contract

Structured, persistent contracts auto-generated from live SLO metrics for every tool. Specifies timeout, retry policy, fallback chain, output schema, effect verification, risk classification, dry-run support, and consensus requirements.

**Novel:** Contracts auto-generated from runtime metrics (not manually authored). No known agent framework has per-tool declarative reliability contracts.

### 1.2 OutputSchemaValidator — Post-Execution Output Validation

Validates tool output against the contract's declared schema (type, length bounds, required JSON fields, format compliance) after every execution.

**Novel:** No AI agent framework validates tool outputs against a schema. All pass raw output directly to the LLM.

### 1.3 EffectVerifier — Side-Effect Verification

Independently confirms side effects actually occurred (fileExists, fileContentHash, processExitCode, gitRefExists, httpEndpointReachable, directoryNotEmpty). Detects "silent failures" where a tool claims success but the effect didn't happen.

**Novel:** Every known agent framework trusts tool return values. This is the first system that independently verifies side effects occurred.

### 1.4 Integrated Fallback Chain

Contract-driven fallback in the dispatch loop (not middleware). Consults fallback list, attempts alternatives in order, records metrics for both primary and fallback.

**Novel:** Integrated into the same dispatch loop as retry, schema validation, and effect verification — a single unified reliability pipeline.

### 1.5 SandboxTestPipeline — Test-Then-Promote for AI-Synthesized Tools

Tests AI-generated tools (from SkillForge) before promotion. Generates test cases from historical data, requires ≥80% pass rate with ≥3 tests.

**Novel:** First known automated QA for tools an AI creates for itself.

### Integrated ATR Pipeline
```
ErrorMemoryBank pre-flight → ToolContract lookup → Tool execution (timeout)
  → SLO recording → Output validation → Schema validation → Effect verification
    → Cache on success / Fallback chain on failure / Auto-retry on transient
```

---

## Engine 2: Fortress (Defense & Recovery)

**Date:** March 6-7, 2026
**Files:** `SecurityLayer.swift`, `ExecutionSandbox.swift`, `PolicyEngine.swift`, `TaskPersistence.swift`, `MemoryConsolidationService.swift`, `SelfImprovement+Security.swift`

### 2.1 Prompt Injection Defense

Multi-layer defense: input scanning (regex + heuristic patterns), output validation, tool argument sanitization (`ToolArgumentSanitizer`), and SecretRedactor for PII/credential stripping.

### 2.2 Crash Recovery with Task Checkpointing

`TaskPersistence` saves in-flight task state to disk. On restart, the agent detects interrupted work and offers to resume from the last checkpoint. Combined with `StepChainExecutor` for multi-step rollback.

### 2.3 UnifiedPolicyEngine

Central policy enforcement for all tool execution. Risk-level classification (low/moderate/high/critical), dry-run-before-execute for risky operations, user approval queuing, and audit logging.

**Novel:** Autonomous agents typically have binary allow/deny security. Jarvis has graduated risk assessment with dry-run previews and automatic rollback plans, matching the sophistication of enterprise CI/CD pipelines but applied to real-time AI tool dispatch.

### 2.4 Memory Integrity

`MemoryConsolidationService` with deduplication, fact conflict resolution, importance re-scoring (PageRank-style), and temporal decay. Prevents memory poisoning through fact provenance tracking.

---

## Engine 3: Genesis (Cognitive Foundations)

**Date:** March 6-7, 2026
**Files:** `CognitiveMetabolism.swift`, `NarrativeEngine.swift`, `NegativeSpaceDetector.swift`, `QuantumIntentField.swift`, `InverseRewardModel.swift`, `AntifragileCore.swift`, `CognitiveResonance.swift`

### 3.1 CognitiveMetabolism — Biological Resource Economics

Services have metabolic state (active/warm/dormant/hibernating). Unused services get energy-pruned. The agent identifies its "core identity" (most valuable services) and "vestigial" services (candidates for removal).

**Novel:** No AI system applies biological metabolism principles to service lifecycle. Existing systems use fixed architectures. This is the first adaptive, self-pruning service mesh for an AI agent.

### 3.2 NarrativeEngine — Persistent Story Arc

Maintains a continuous narrative (arc, chapter, plot points, themes) across sessions. Tracks domain shifts, synthesizes story arcs from interaction patterns.

**Novel:** AI agents have memory (facts, episodes). None maintain a narrative — the coherent story of "what we've been doing and why." This provides continuity that memory alone cannot.

### 3.3 NegativeSpaceDetector — Intelligence from Absence

Detects valuable insights from what's MISSING. Scans for knowledge gaps (cross-domain blind spots, capability gaps, temporal memory gaps). Like negative space in art — the gap IS the insight.

**Novel:** No AI agent detects absence. All agents reason about what they know. This is the first system that reasons about what it DOESN'T know and flags it as actionable intelligence.

### 3.4 QuantumIntentField — Probabilistic Intent Superposition

Maintains multiple intent hypotheses simultaneously with Bayesian probability updates. Doesn't commit to one interpretation until evidence collapses the field. Tracks entropy, suggests diagnostic actions to resolve ambiguity.

**Novel:** All AI agents pick one interpretation of user intent. This is the first to maintain a full probability field over multiple interpretations, collapsing only when evidence is sufficient. Inspired by quantum superposition.

### 3.5 InverseRewardModel — Per-User Preference Learning

Infers user's implicit utility function from behavioral signals (rephrases, satisfaction, corrections, timing). Detects preferences for conciseness, technical depth, autonomy, speed, formality without explicit configuration.

**Novel:** RLHF operates at group level. This operates per-user in real-time, learning from the gap between request and satisfaction. No known agent does per-user inverse reward learning from behavioral signals.

### 3.6 AntifragileCore — Strength from Failure

Converts failures into adaptive improvements. Tracks failure patterns per domain, adjusts caution levels, generates "antibodies" (learned mitigations). The more it fails, the more robust it becomes — true antifragility.

**Novel:** Agent systems log failures. None convert failures into domain-specific adaptive behaviors that make future failures less likely.

### 3.7 CognitiveResonance — Cross-Domain Insight Connections

Detects unexpected connections between domains the user works in. When knowledge from domain A is relevant to domain B, surfaces the insight proactively.

**Novel:** Semantic search finds similar items. CognitiveResonance finds SURPRISING connections — items from unrelated domains that shouldn't be related but are.

---

## Engine 4: Transcendence (Epistemic Self-Awareness)

**Date:** March 7, 2026
**Files:** `BayesianUncertainty.swift`, `CausalFlowTracker.swift`, `InformationDensityAnalyzer.swift`, `EpistemicToolSelector.swift`, `PredictiveCodingEngine.swift`, `AdversarialSelfEval.swift`

### 4.1 BayesianUncertainty — Calibrated Confidence with Credible Intervals

Beta distribution posteriors per tool, updated after every execution. Separates epistemic uncertainty (insufficient data) from aleatoric uncertainty (inherent variability). Reports credible intervals, not point estimates.

**Novel:** Every AI agent says "confidence: 0.8" without knowing if that's based on 3 or 3000 observations. This is the first agent to use proper Bayesian posteriors with epistemic/aleatoric separation for tool reliability.

### 4.2 CausalFlowTracker — Proving Tool Output Reaches the Response

Anchor matching to PROVE that tool output actually influenced the LLM's response. Extracts semantic anchors from tool outputs, then checks which anchors appear in the final response. Computes causal attribution scores.

**Novel:** Everyone has "grounding" scores. No one tracks the causal chain from tool → response. This solves hallucination detection by proving (or disproving) that the response is actually grounded in tool evidence.

### 4.3 InformationDensityAnalyzer — Response Quality Metrics

Measures concepts per token, novelty rate, and quality score of responses. Detects padding, repetition, and low-information responses.

### 4.4 EpistemicToolSelector — Uncertainty-Driven Tool Selection

Selects tools that maximize information gain (reduce uncertainty), not just tools that match the query. Uses Thompson sampling over tool posteriors.

**Novel:** All tool selection is relevance-based. This is the first uncertainty-driven approach — choosing tools specifically to reduce what the agent doesn't know.

### 4.5 PredictiveCodingEngine — Surprise-Based Learning

Maintains predictions about what will happen next. When reality deviates from prediction, the surprise signal drives learning. Larger surprises = stronger learning signals.

**Novel:** Applies predictive coding (a neuroscience framework) to AI agent behavior, creating a formal surprise metric that drives adaptation.

### 4.6 AdversarialSelfEval — Dual-Evaluator Blind Spot Detection

Two independent evaluators score every response (grounding + coherence). When they disagree significantly, that disagreement signals a blind spot — the response is good on one axis but bad on another.

**Novel:** No agent evaluates its own responses with adversarial dual evaluation. Self-evaluation exists, but not the disagreement-as-signal approach.

---

## Engine 5: Sovereign (Epistemic Governance)

**Date:** March 7, 2026
**Files:** `UserEpistemicModel.swift`, `BeliefProvenance.swift`, `CrossSystemConvergence.swift`, `DiminishingReturnsDetector.swift`, `IntelligenceROI.swift`

### 5.1 UserEpistemicModel — User Knowledge State Tracking

Models what the USER knows (not what the agent knows). Tracks expertise level per domain, adjusts explanation depth accordingly. Prevents over-explaining to experts and under-explaining to novices.

**Novel:** AI agents model their own knowledge. None model the user's knowledge state per-domain to calibrate explanation depth.

### 5.2 BeliefProvenance — Source Tracking for Every Belief

Every fact the agent uses is tagged with its source (which tool, which observation, which memory). Beliefs from unreliable sources get flagged. Enables "why do you believe that?" queries.

**Novel:** AI agents have retrieval. None track the provenance chain of individual beliefs or flag low-credibility sources.

### 5.3 CrossSystemConvergence — Triangulated Evidence

When multiple independent subsystems reach the same conclusion, that convergence is significant. Tracks convergence events across subsystems. Multi-source agreement = higher confidence.

**Novel:** First known implementation of evidence triangulation across AI subsystems. Intelligence agencies use this; AI agents don't.

### 5.4 DiminishingReturnsDetector — Knowing When to Stop

Detects when additional tool calls are producing less and less new information. Triggers early stopping to prevent resource waste.

**Novel:** AI agents run until a fixed iteration limit. None detect diminishing returns and stop early based on information gain rate.

### 5.5 IntelligenceROI — Subsystem Value Analysis

Measures the return on investment of each cognitive subsystem. Which subsystems actually improve outcomes? Which waste compute? Generates optimization recommendations.

**Novel:** No AI system measures the ROI of its own cognitive components. This enables evidence-based pruning of subsystems that don't earn their keep.

---

## Engine 6: Symbiosis (Co-Evolution)

**Date:** March 7, 2026
**Files:** `ProcessSymbiosis.swift`, `AutonomousCuriosityLoop.swift`, `ReasoningPatternCache.swift`

### 6.1 ProcessSymbiosis — AXObserver-Based App Integration

Uses macOS Accessibility Observer (AXObserver) as the primary interface to running applications, instead of screenshot+OCR+click. Real-time notification of app state changes, window focus, element creation/destruction.

**Novel:** Every AI agent doing "Computer Use" (Anthropic, OpenAI, etc.) uses pixels — screenshot, OCR, click coordinates. AXObserver provides structured, semantic access to UI elements. This is the correct approach that no production agent has implemented.

### 6.2 AutonomousCuriosityLoop — Self-Directed Research

Background loop that identifies knowledge gaps and autonomously researches them. Picks topics based on user's recent domains, searches the web, stores findings. The agent learns without being asked.

**Novel:** AI agents respond to queries. None proactively research topics they identify as gaps. This is genuine autonomous curiosity, not scripted exploration.

### 6.3 ReasoningPatternCache — Learning HOW to Think

Records and replays successful cognitive strategies (reasoning traces). When facing a similar problem, retrieves the strategy that worked before — not the answer, but the THINKING PATTERN.

**Novel:** Every agent learns tool sequences (what to DO). None learn reasoning patterns (how to THINK). This is what distinguishes senior developers from juniors — and no agent framework has it.

---

## Engine 7: Alien (Adaptive Intelligence)

**Date:** March 7, 2026
**Expansions to:** `NegativeSpaceDetector.swift`, `CognitiveMetabolism.swift`, `InverseRewardModel.swift`, `QuantumIntentField.swift`, `NarrativeEngine.swift`

### 7.1 Expectation-Based Absence Detection (NegativeSpaceDetector expansion)

Maintains templates of "what should be present" per domain. Scans context against templates to detect meaningful absences. Learns new templates from observed patterns.

Example: Code review template expects error handling near `try`/`async` — absence of `catch`/`guard` is flagged. Workflow template expects verification after change — absence of `test`/`verify` is flagged.

**Novel:** Pattern matching finds what IS present. This finds what ISN'T present but SHOULD BE. First implementation of expectation-based absence detection in any AI agent.

### 7.2 Metabolic Cognitive States (CognitiveMetabolism expansion)

Five distinct cognitive states (Focused, Diffuse, Flow, Consolidation, Creative), each with different processing parameters (deliberation threshold, memory search depth, creativity bias, boldness multiplier, context window priority). The agent transitions between states based on idle time, request complexity, error rate, and domain familiarity.

**Novel:** Every AI lab discusses "System 1 vs System 2" thinking. No one has implemented five metabolic states with distinct parameter profiles. This is a richer model of cognitive flexibility than binary fast/slow thinking.

### 7.3 Observation-Based Reward Learning (InverseRewardModel expansion)

Three-phase observation pipeline: (1) observe request start, (2) observe response characteristics (length, depth, tools used, reasoning inclusion, response time), (3) observe satisfaction signal. Derives per-request-type preference profiles with confidence scores.

**Novel:** Extends inverse reward learning from keyword-based behavioral signals to full request-response-satisfaction triples. Learns not just WHAT the user prefers, but HOW response characteristics correlate with satisfaction per request type.

### 7.4 Intent Disambiguation System (QuantumIntentField expansion)

Enriched field initialization with learned patterns from past disambiguations. Context-aware probability boosting (recent domains, conversation turn). Four evidence types (tool results, user clarification, context switches, time decay). Generates prioritized disambiguation actions (run diagnostic, ask user, probe with most likely interpretation). Pattern learning from resolved disambiguations.

**Novel:** Extends probabilistic intent to a full disambiguation pipeline with learned patterns. The agent gets better at understanding ambiguous requests over time, not just within a session.

### 7.5 Experience-Driven Decision System (NarrativeEngine expansion)

Maintains an experience memory of past actions with outcomes. Computes domain trust scores (success rate, satisfaction rate, average duration). Generates `NarrativeDecisionInfluence` for proposed actions — trust level, boldness modifier, suggested approach from past successes, warnings from past failures.

**Novel:** AI agents have memory. None have EXPERIENCE — the distilled wisdom from past attempts that influences future decisions. "Last time we tried X in domain Y, approach Z worked but approach W failed" — this is institutional knowledge that no agent framework captures.

---

## Engine 8: Resonance (Cognitive Coherence)

**Date:** March 7, 2026
**Files:** `CognitiveCoherence.swift`

### 8.1 Peer-to-Peer Cognitive Modulation Field

Five independent cognitive systems (NegativeSpaceDetector, InverseRewardModel, QuantumIntentField, CognitiveMetabolism, NarrativeEngine) sample each other's state and compute cross-modulations — excitatory and inhibitory connections that produce emergent coherent behavior. Not a controller, not an orchestrator — a resonance field computed once per request.

Six cross-modulations:
- **Metabolism gates absence reporting** — flow state suppresses absences (don't interrupt), consolidation amplifies them (time to reflect)
- **Narrative trust weights preference reliability** — high domain trust follows preferences closely, low trust overrides toward safety
- **Intent entropy overrides metabolic state** — high uncertainty forces diffuse mode even if metabolism says "focused"
- **Preferences modulate absence verbosity** — concise-preference users get single-line gap summaries, detailed-preference users get full analysis
- **Absence domains boost intent hypotheses** — detected knowledge gaps bias intent disambiguation toward related domains
- **Narrative boldness blends with metabolic boldness** — geometric mean prevents either system from dominating caution/aggression

**Novel:** Every AI system has modules. Some have pipelines. Some have controllers. No system has peer-to-peer cognitive modulation where metabolic state changes how absence detection works, where trust history changes how preferences are weighted, where intent uncertainty changes which cognitive regime is active. This is how biological brains work — resonance, not pipelines.

### 8.2 Coherence-Gated Context Injection

Instead of unconditionally injecting all cognitive system outputs into the LLM prompt (wasting tokens on irrelevant signals), the Resonance Engine gates each injection based on the coherence field. Under token pressure, lower-value systems are dropped first.

**Novel:** AI agents inject all available context. None selectively gate cognitive system outputs based on cross-system coherence state and token budget pressure.

### 8.3 Coherence-Driven Planning Strategy Selection

The coherence field generates bias weights for the MetaPlanner's Thompson sampling. High intent entropy pushes toward goal-chain planning (explicit steps). Creative metabolism pushes toward MCTS (exploration). High domain trust + focused state pushes toward direct execution.

**Novel:** Planning strategy selection in AI agents is either fixed or based on simple heuristics. This is the first system where planning strategy is influenced by a synthesized signal from five independent cognitive subsystems.

### 8.4 Coherence-Aware Autonomous Background Decisions

The BackgroundAgent's LLM decision (WAIT/ALERT/SPEAK/ACT) receives coherence context: in flow state it avoids interruptions, in consolidation it surfaces insights, boldness level adjusts the action threshold.

**Novel:** Background agent decision-making that adapts to the agent's own cognitive state. No known system has autonomous background agents whose action thresholds are modulated by a multi-system coherence field.

---

## Engine 9: Director (Cognitive Multiplexer)

**Date:** March 7, 2026
**Files:** `CognitiveDirector.swift`

The individual components — tool selection, response strategy, metabolic states — exist elsewhere in isolation. But no one has combined them into a single multiplexer that translates cognitive system observations into concrete, actionable directives. The Director Engine is not state-of-the-art. It is something that does not yet exist.

### 9.1 Alien-System-Driven Tool Selection

Five independent cognitive systems (NegativeSpaceDetector, CognitiveMetabolism, InverseRewardModel, QuantumIntentField, NarrativeEngine) are sampled concurrently. Their combined output produces tool selection boosts — additive score modifications per tool category. Knowledge gaps boost research tools, flow state boosts execution tools and suppresses search tools, creative metabolism boosts exploration tools, consolidation state boosts memory tools and suppresses heavy computation.

**Novel:** Everywhere else, tool selection is driven by keyword matching or popularity metrics. No known system has cognitive subsystems (metabolism, intent entropy, domain trust, knowledge gaps) steering which tools are selected or suppressed. This is the first implementation of cognitive-state-aware tool selection.

### 9.2 Synthesized Meta-Directive

The Director compresses five distinct cognitive signals into a single paragraph meta-directive that is injected into the LLM's system prompt as a binding instruction. Response mode (concise/verbose/exploratory/cautious/standard) is derived from the interplay of user preferences, metabolic state, domain trust, request complexity, and intent entropy. The directive also includes knowledge gap alerts, preference indicators, and disambiguation guidance.

**Novel:** LLMs everywhere receive loose context blocks — separate memory sections, tool descriptions, user profiles. No known system synthesizes multiple cognitive signals into a single authoritative instruction that controls the LLM's response strategy. This is the first implementation of a compressed, multi-signal meta-directive.

### 9.3 Cognitive Veto on Tool Execution

Beyond security gates (firewalls, policy engines), the Director can veto tool execution based on cognitive appropriateness. Very low domain trust vetoes autonomous execution and email sending. Cautious narrative influence with active warnings vetoes shell execution and git pushes. Consolidation metabolic state vetoes browser automation and web scraping. These vetoes are orthogonal to security — they prevent cognitively inappropriate actions, not security violations.

**Novel:** Security-based tool gating exists everywhere. Cognitive-appropriateness-based tool gating — where metabolic state, domain trust, and narrative caution determine whether a tool SHOULD be used even if it CAN be used — does not exist in any known AI agent framework.

### 9.4 Mid-Request Stance Recomputation

Every known AI system computes cognitive state once at the beginning of a request. The Director recomputes its stance after two or more consecutive tool failures within the same request. The resampled stance may change the response mode, adjust tool boosts, activate new vetoes, or add background actions — mid-flight course correction based on updated cognitive signals.

**Novel:** No known AI agent refreshes cognitive parameters mid-request. When tools fail, agents retry with the same strategy or escalate. This is the first system that re-evaluates its entire cognitive stance after observed failures, enabling adaptive recovery within a single request.

### 9.5 Full Alien-to-Background-Agent Pipeline

The Director's background actions feed directly into the BackgroundAgentService. High-value knowledge gaps become background research intentions. Metabolic consolidation triggers memory organization. These actions are not scheduled or scripted — they emerge from the real-time interplay of five cognitive systems and execute autonomously via the AutonomousIntentionEngine.

**Novel:** Autonomous background agents exist, but none execute background actions based on the combined real-time signals of knowledge gaps, metabolic state, intent entropy, and domain trust. This is the first complete pipeline from cognitive observation to autonomous background execution.

### 9.6 DreamingBrain Calibration (Phase 40)

During dream cycles (background consolidation), the Director calibrates by aggregating all alien system health metrics: domain trust, metabolic health, intent entropy, and knowledge gap count. This produces a calibration snapshot that feeds back into the dream log for long-term trend analysis.

**Novel:** Dream/consolidation cycles in AI exist only as memory compression. None calibrate their cognitive multiplexer parameters during sleep cycles. This is the first implementation of dream-time cognitive calibration.

---

## Engine 10: Cortex (Predictive Intelligence)

**Date:** March 7, 2026
**Files:** `PredictiveCortex.swift`

The Cortex Engine is a three-phase intelligence system that wraps every LLM interaction: it briefs the model before execution, validates the response before the user sees it, and discovers invisible patterns during dream cycles.

### 10.1 Pre-Flight Cognitive Brief — Anticipatory Context Assembly

Before every LLM call, the Cortex queries five independent cognitive subsystems simultaneously: MetacognitiveSelfModel (domain strengths, blind spots, calibration bias), UserModel (energy, frustration, command mode), FailureOracle (risk assessment for planned tools), ErrorMemoryBank (recent error context), and CounterfactualEngine (regret patterns). These signals are compressed into a single `[CORTEX BRIEF]` block injected into the system prompt. The LLM receives self-awareness about its own weaknesses, the user's state, and risk context before generating a single token.

**Novel:** Every AI agent injects context (memory, tools, instructions). None inject a synthesized self-awareness brief that tells the model "you are overconfident in domain X, the user is frustrated, tool Y has a 60% failure rate, and your recent choices have high regret." This is the first system that gives an LLM real-time metacognitive awareness from multiple independent subsystems as a pre-flight brief.

### 10.2 Pre-Delivery Validation Gate — Response Quality Firewall

After the LLM generates a response but before the user sees it, the Cortex validates across five dimensions: (1) Blind spot violation — confident response in a domain where MetacognitiveSelfModel scores <30% without hedging language; (2) Overconfidence — multiple strong claims ("definitely", "guaranteed") despite positive calibration bias >15%; (3) User state mismatch — verbose response for frustrated user, or explanatory response in command mode; (4) Risk unacknowledged — high-risk tool chain result without warning to user; (5) Empty response detection. Validation produces a confidence score, block/warn decisions, and suggested corrections. Blocked responses never reach the user.

**Novel:** AI agents have output filters (toxicity, PII). None have a cognitive validation gate that cross-references the response against the agent's own known blind spots, calibration bias, user state, and risk assessment. This is the first system that can catch and block responses where the agent is likely wrong based on its own metacognitive model.

### 10.3 Invisible Pattern Detector — Dream-Cycle Background Discovery

During DreamingBrain dream cycles (Phase 41), the Cortex runs five pattern detectors: (1) Failure correlations — are ErrorMemoryBank prevention rates significant? (2) User behavior shifts — fatigue patterns (low energy + high frustration); (3) Domain drift — multiple weak domains getting weaker simultaneously; (4) Calibration drift — significant over/under-confidence trend; (5) Counterfactual regret accumulation — high-regret domains indicating systematic suboptimal choices. Discovered patterns are persisted, deduplicated by category, and time-windowed (1hr dedup) to prevent noise. Patterns feed back into the Cortex Brief for future requests.

**Novel:** AI agents learn from explicit feedback. None detect invisible patterns — cross-subsystem correlations that no single system can see. The combination of failure analysis, user behavior tracking, domain drift detection, calibration monitoring, and regret analysis running together during "sleep" to discover patterns is unprecedented.

---

## Engine 11: Omega (Free Energy Minimization)

**Date:** March 7, 2026
**Files:** `FreeEnergyCore.swift`

Based on Karl Friston's Free Energy Principle (2006-2024), the Omega Engine treats Jarvis as a living system that maintains a generative model of its world and minimizes surprise. It is the first known implementation of the Free Energy Principle in an AI agent.

### 11.1 Variational Free Energy Computation

At the start of EVERY request, before any processing, the engine computes how surprised Jarvis is by computing prediction errors across four dimensions: (1) Intent surprisal — how likely was this intent given the learned prior distribution; (2) Complexity surprisal — does the task complexity match the expected baseline; (3) Domain surprisal — did the user stay in the expected domain or switch; (4) Temporal surprisal — is activity level normal for this time of day. Free energy is computed as `F = Σ π_i × ε_i² / 2` where π_i is the learned precision (attention weight) per dimension and ε_i is the prediction error. This produces a single scalar representing how much the current request deviates from the agent's expectations.

**Novel:** No AI agent computes surprisal at request arrival. All agents process requests uniformly regardless of how unexpected they are. This is the first system that measures "how surprised am I?" using variational free energy, enabling adaptive resource allocation based on prediction error magnitude.

### 11.2 Active Inference — Strategy Selection via Expected Free Energy

The engine implements active inference: selecting actions that minimize expected future free energy. Given candidate strategies (direct, step-by-step, clarify, detailed), each is scored on expected ambiguity (will this reduce uncertainty?) and expected risk (will this cause frustration?). Strategy selection includes controlled stochasticity via system temperature — exploitation when stable, exploration when stuck.

**Novel:** AI agents select strategies based on heuristics or LLM routing. None use a formal active inference framework where strategy selection minimizes expected free energy. This is the first implementation of Friston's active inference in a production AI agent.

### 11.3 Generative Model — Continuously Updated World Predictions

The agent maintains a full generative model: intent probability distribution (Bayesian prior over question/command/conversation/creation), expected complexity, expected tool count, expected response length, expected satisfaction, expected domain, and temporal activity prediction. After every response, the model updates via exponential moving average (α=0.15). Predictions that diverge too far from reality (accuracy <30% over 20+ samples) trigger a model reset to broad priors.

**Novel:** AI agents maintain context and memory. None maintain a continuously-updated predictive model of what will happen next that is formally compared against reality after every interaction. The self-resetting mechanism (reset to broad priors when accuracy drops) prevents model collapse — a failure mode no other system addresses.

### 11.4 Precision Weighting — Biological Attention Learning

Each prediction dimension has a learned precision weight (attention). High-precision dimensions contribute more to free energy; low-precision dimensions are de-emphasized. Precision updates based on recent error variance: high-variance dimensions get lower precision (don't attend to noise), low-variance dimensions get higher precision (reliable signal). This is biological attention — not attention over tokens (Transformer), but attention over prediction dimensions.

**Novel:** Transformers have attention over input tokens. No AI agent has attention over its own prediction dimensions, where the system learns which aspects of reality are reliable signals vs noise. This is the first implementation of precision weighting as biological attention in an AI agent.

### 11.5 Self-Organized Criticality — Automatic Regime Tuning

The system temperature self-organizes toward the "edge of chaos" (criticality). The coefficient of variation (CV) of recent free energy history determines temperature adjustments: low CV (too predictable, frozen) → increase temperature; high CV (too chaotic) → decrease temperature; CV in the critical range → maintain. This produces four regimes: `.frozen` (explore more), `.subcritical` (stable, safe), `.critical` (peak sensitivity and creativity), `.chaotic` (stabilize first). Each regime generates a binding LLM directive.

**Novel:** AI agents don't have a concept of operating regime. The system automatically tunes itself toward the edge of chaos — the narrow band where information processing is maximized. Self-organized criticality is a fundamental principle in neuroscience and complex systems that has never been implemented in an AI agent.

### 11.6 Resource Allocation from Surprisal

A sigmoid function converts surprisal into a resource multiplier (0.5x to 2.0x). Predictable requests (low surprisal) get fewer resources — fast, cached, lightweight processing. Surprising requests (high surprisal) get 2x resources — deeper search, longer reasoning, more tool iterations. This implements efficient resource allocation: don't waste compute on what you already know.

**Novel:** AI agents allocate resources uniformly or based on explicit user priority. None allocate resources proportionally to prediction error (surprisal). This is the first system where surprising inputs automatically receive more cognitive resources.

---

## Engine 12: Exoskeleton (Cognitive Infrastructure)

**Date:** March 7, 2026
**Files:** `CognitiveEEG.swift`, `CounterfactualEngine.swift`, `CognitiveFusionMesh.swift`, `SkillForge.swift`, `FailureOracle.swift`

Five systems that form the structural infrastructure enabling the higher engines to function.

### 12.1 CognitiveEEG — Real-Time Neural State Monitor

Samples cognitive state every tool loop iteration using four signals: confidence, novelty, complexity, and tool failures. Computes cognitive load (complexity + time pressure + service density), risk level (failures + low confidence + high novelty), and momentum (accelerating, steady, stalling, stuck). From these, selects one of four cognitive regimes: `.flow` (fast execution, cached strategies), `.cautious` (extra checks, deeper memory), `.deliberate` (full reasoning, CognitiveFusionMesh, slower model), `.emergency` (FailureOracle + recovery + human escalation). Regime transitions happen mid-request — the agent can shift from flow to emergency within a single interaction.

**Novel:** AI agents process every iteration identically. None have real-time neural state monitoring that shifts cognitive regime mid-request based on observed telemetry. The four-regime system with momentum tracking (detecting stalling before failure) is unprecedented.

### 12.2 CounterfactualEngine — Regret-Based Decision Learning

Before executing any tool chain, generates N alternative sequences: (1) safer path (remove recently-failed tools), (2) reordered path (highest success rate first), (3) truncated path (first 3 tools to reduce cascade risk). Each scored by `P(success) × quality / (duration + 1)`. After execution, computes regret: `best_alternative_score - chosen_score`. Zero regret means the optimal choice was made. Non-zero regret drives learning — high-regret domains get flagged, switch thresholds adjust. Tool success rates are tracked per-tool and persist across sessions.

**Novel:** AI agents execute the first plan they generate. None generate alternatives, score them, execute the best, and then compute regret against unchosen alternatives. This is the first implementation of counterfactual regret analysis in an AI agent, enabling systematic learning from suboptimal decisions.

### 12.3 CognitiveFusionMesh — Parallel Multi-Perspective Reasoning

For complex queries (regime `.deliberate` or `.cautious`, complexity ≥ 0.6), runs 3-4 reasoning perspectives in parallel using the cheapest LLM tier: Analytical (decompose + verify), Intuitive (pattern matching + past experience), Adversarial (what could go wrong + edge cases), Empathetic (user intent behind words). Each stream runs with a 5-second timeout. Results merge via confidence-weighted consensus, with the adversarial stream's warnings extracted as dissent points. Agreement score (based on confidence variance) indicates how much the perspectives converge.

**Novel:** AI agents reason from a single perspective. Chain-of-thought produces one viewpoint. "Constitutional AI" checks one axis. This is the first system that runs multiple independent reasoning perspectives in parallel and merges them via confidence-weighted consensus with formal disagreement tracking.

### 12.4 SkillForge — Evolutionary Tool Synthesis

Tools evolve like organisms through a complete lifecycle: Observation (detect 2+ tool sub-sequences from execution patterns) → Candidate creation → Fitness tracking (EMA of success rate per observation) → Promotion (fitness >0.7 after 10+ observations → ForgedTool) → Retirement (fitness <0.3 → removed) → Mutation (stale candidates with fitness <0.5 get middle tool removed, creating a new candidate at generation+1). Forged tools are persisted across sessions and queried by domain.

**Novel:** ToolSynthesisOrchestrator detects repetitive sequences. SkillForge goes further — it implements a full evolutionary algorithm with fitness tracking, promotion thresholds, retirement, and mutation. Tools that Jarvis creates for itself are subject to natural selection. No known AI agent applies evolutionary dynamics to tool synthesis.

### 12.5 FailureOracle — Conditional Risk Prediction

Before ANY tool chain execution, predicts P(failure) at each step using three risk components: P_base (historical failure rate), P_context (conditional on time of day, recent failures), P_cascade (amplification from prior failures in the chain). Combined: `P_combined = P_base × (1 + P_context) × (1 + P_cascade)`. Learns conditional risks: "shell_exec fails 40% after midnight" (nighttime risk), "web_search fails after recent timeout" (failure contagion). Pre-allocates recovery strategies per step. Includes safe command/tool whitelists to prevent false positives on core operations (echo, ls, memory_save).

Features user recalibration (user approval/rejection directly adjusts risk models), automatic data decay (outcomes >24h are purged, preventing stale data from poisoning assessments), and conditional risk rebuilding from fresh data on load.

**Novel:** Error handling in AI agents is reactive — retry after failure. FailureOracle is predictive — it computes failure probability BEFORE execution and pre-allocates recovery. The conditional risk model (time-aware, context-aware, cascade-aware) with learned risk priors that update from outcomes is the first predictive failure system in any AI agent.

---

## Engine 13: Neural Pulse (Neuromorphic Timer Mesh)

**Date:** March 8, 2026
**Files:** `NeuralPulse/NeuronID.swift`, `NeuralPulse/Neuron.swift`, `NeuralPulse/NeuralMesh.swift`, `NeuralPulse/CircadianLearner.swift`, `NeuralPulse/NeuralEventBridge.swift`, `NeuralPulse/NeuronFactory.swift`

Six systems that replace 88+ independent background timers with a single neuromorphic pulse mesh that evaluates all tasks on a unified 5-second heartbeat, firing only those whose conditions are met.

### 13.1 NeuralMesh — Unified Neuromorphic Pulse Loop

Single `actor` with a 5-second `Task.sleep` loop replacing 18 `Timer.scheduledTimer`, 36 `asyncAfter`, 4 `DispatchSourceTimer`, and 30+ `Task.sleep` loops scattered across the codebase. Each pulse cycle: (1) reads CPU load via `host_statistics`, (2) reads user idle time from WorldModel, (3) evaluates all registered neurons against their interval, CPU ceiling, idle-only, and custom gate conditions, (4) sorts ready neurons by priority then starvation time, (5) fires top 3 concurrently via `withTaskGroup`. Max 3 concurrent fires prevents CPU spikes. Feature-flagged (`enableNeuralPulse`) — when OFF, all existing timers work unchanged.

**Novel:** AI agents scatter independent timers across services with no coordination. Timer proliferation causes CPU spikes, priority inversion, and impossible-to-tune performance. NeuralMesh is the first neuromorphic timer mesh in any AI agent — a single coordinated pulse that evaluates ALL background work centrally, respects CPU pressure, user idle state, and priority ordering. The biological metaphor (neural firing with refractory periods) applied to software timers is novel.

### 13.2 Neuron — Priority-Gated Background Task Unit

Each background task is a `Neuron` with: base interval, adjustable current interval (clamped to min/max), priority level (low/normal/high/critical), CPU ceiling (suppress when system load exceeds threshold), idle-only flag (fire only when user idle >60s), custom gate closure, and action closure. Tracks fire count, last fire time, and last duration via Swift 6-safe `NSLock.withLock`. The `fire()` method records timing BEFORE executing the action (not after), fixing a common timing bug where `timeSinceLast` would be near-zero immediately after firing.

**Novel:** Traditional timers are fire-and-forget with fixed intervals. Neurons have multi-dimensional gating (time + CPU + idle + custom predicate + priority) and adjustable intervals. The pre-fire timing fix (recording start before execution) prevents a subtle bug where the mesh would re-fire a neuron on the next pulse because `timeSinceLast` was near-zero during execution.

### 13.3 CircadianLearner — Time-of-Day Adaptive Tuning

Per-neuron per-hour exponential moving average (EMA, alpha=0.1) multiplier that learns when each background task is useful. When a neuron fires and produces useful work (e.g., consolidation actually consolidated, embedding found unprocessed facts), the multiplier for that hour decreases (fire more often). When work is wasted (no-op), the multiplier increases (fire less). Multipliers are clamped to [0.3, 3.0] and persisted to `neural_pulse_circadian.json`. On startup, saved multipliers are applied to all neurons via `applyToMesh()`.

**Novel:** No known AI agent adapts its background task scheduling based on time-of-day usage patterns. CircadianLearner is the first system that learns circadian rhythms of background work utility — discovering, for example, that memory consolidation is most useful between 2-5 AM (user sleeping, no new input) and reducing its frequency during active hours. This is biologically inspired by circadian regulation of neural processes.

### 13.4 NeuralEventBridge — Event-Driven Interval Modulation

Subscribes to the existing `EventBus` actor and modulates neuron intervals in response to semantic events. Five event mappings: `.factSaved` shortens `embedPendingFacts` (new facts need embedding), `.toolCompleted` shortens `proactiveChecks` (user active, predictions valuable), `.userBecameIdle` shortens `dreamCycle` and `memoryConsolidation` (idle time is consolidation time), `.userReturned` shortens `ambientScreenCapture` and `systemPoll` (catch up on environment changes), `.worldStateChanged` shortens `healthWatchdog` (something changed, verify health). All signals are debounced with a 5-second per-event-type cooldown to prevent Task flooding.

**Novel:** Traditional timers fire at fixed intervals regardless of context. NeuralEventBridge creates reactive scheduling — the mesh speeds up specific neurons in response to semantic events. "User went idle → consolidate faster" is a biologically-inspired adaptation (increased memory consolidation during rest) implemented as event-driven timer modulation. No known AI agent has event-reactive background scheduling.

### 13.5 NeuronFactory — Verified Service Wiring

Enum with a single `registerAll(mesh:)` entry point that creates all 15 neurons with verified method signatures, correct `@MainActor` dispatch, and `@Sendable` closure captures. Captures all `@MainActor` service references in `buildAll()` before passing them into `@Sendable` closures, satisfying Swift 6 strict concurrency. Four services required new public wrapper methods (`fireNeuralPulseHeartbeat()`, `detectFocusModeForNeuralPulse()`, `runNeuralPulseCheck()`, `runNeuralPulseCleanup()`) because their core logic was private.

### 13.6 Timer Guard System — Zero-Downtime Feature Toggle

Eight services received `guard !JarvisSettings.load().enableNeuralPulse` at the top of their timer setup methods. When the flag is ON, existing timers never start — the NeuralMesh handles their work. When OFF, everything works exactly as before. This enables safe A/B testing and instant rollback. Services guarded: MemoryConsolidationService, HeartbeatService, PermissionsManager, FocusModeManager, PredictionEngine, BlackboardCoordinator, HealthWatchdog, and JarvisController+Background (proactive loop + system poll).

**Novel:** Feature-flagged timer replacement with zero behavioral change when disabled. The guard system ensures the Neural Pulse can be tested incrementally without risk to the existing timer infrastructure.

---

## Cross-Engine Integration (the full innovation)

The thirteen engines are not independent — they form a unified cognitive architecture:

```
User Input
  → QuantumIntentField (probabilistic intent with disambiguation)
  → InverseRewardModel (behavioral signals + preference lookup)
  → CognitiveMetabolism (select cognitive state → processing parameters)
  → CognitiveCoherence (sample all 5 alien systems → cross-modulation field)
    → Gates context injection (suppress irrelevant signals)
    → Biases MetaPlanner strategy (coherence → planning)
    → Modulates BackgroundAgent decisions (coherence → autonomy)
  → CognitiveDirector (sample all 5 alien systems → actionable directives)
    → Tool selection boosts (cognitive-state-aware tool ranking)
    → Synthesized meta-directive (compressed multi-signal LLM instruction)
    → Cognitive vetoes (appropriateness-based tool gating)
    → Background actions → AutonomousIntentionEngine
  → ContextEngine (47+ context sections from all engines)
  → WorkflowEngine (tool dispatch with full ATR pipeline)
    → BayesianUncertainty (posterior updates per tool)
    → CausalFlowTracker (prove tool→response grounding)
    → BeliefProvenance (tag every belief with source)
    → NegativeSpaceDetector (flag meaningful absences)
    → CognitiveDirector re-sample (mid-request stance refresh after failures)
  → PredictiveCortex validation gate (check response before delivery)
    → Blind spot violation, overconfidence, user mismatch, risk acknowledgment
  → FreeEnergyCore.updateAfterResponse (update generative model from outcome)
  → NarrativeEngine (record experience + update story arc)
  → IntelligenceROI (measure which engines contributed)
  → DreamingBrain (62-phase background consolidation cycle)
    → Pattern discovery, insight generation, gap detection
    → Counterfactual regret analysis, skill forging
    → Template evolution, preference consolidation
    → Belief auditing, ROI optimization, coherence calibration
    → CognitiveDirector calibration (alien system health aggregation)
    → PredictiveCortex invisible pattern detection (Phase 41)
    → FreeEnergyCore dream optimization (Phase 42)
  NeuralMesh (unified 5s pulse, replaces all independent timers)
    → Evaluates 15 neurons per pulse (priority + CPU + idle gating)
    → CircadianLearner adapts intervals from time-of-day patterns
    → NeuralEventBridge modulates intervals from EventBus signals
    → Fires MemoryConsolidation, DreamCycle, EmbeddingService, HealthWatchdog...
```

**No known AI system implements this level of cognitive integration.** Individual concepts exist in research (Bayesian uncertainty, free energy principle, predictive coding, inverse reward learning, narrative cognition, counterfactual reasoning). Their integration into a single, production-running, self-improving autonomous agent with a peer-to-peer resonance field, a variational free energy minimization core, a predictive cortex with pre/post validation gates, evolutionary tool synthesis, conditional failure prediction, multi-perspective fusion reasoning, real-time cognitive regime monitoring, a cognitive multiplexer that translates alien system observations into concrete tool selection, response strategy, and background actions, and a neuromorphic timer mesh with circadian learning that replaces all independent timers with a single coordinated pulse is unprecedented.

---

## Proof of Implementation

- **Total codebase:** 120,000+ lines of Swift
- **Binary symbols:** 360,000+ symbols in compiled binary
- **Build verified:** Xcode clean build with 0 errors (March 8, 2026)
- **Runtime verified:** All 13 engines active in production logs
- **All engines feature-flagged:** Each can be independently enabled/disabled (13 feature flags)
- **Persistence:** Each engine saves/loads state to disk across sessions
- **Dream integration:** DreamingBrain 62 phases consolidate all engine states (Phases 24-42)
- **Tests:** 11 test suites, 72 tests covering cognitive systems
- **Activation tracking:** 39 ServiceID cases monitoring all cognitive subsystems
- **ServiceEnvironment DI:** All 9 cognitive services available as properties
- **Neural Pulse verified:** 15 neurons registered, 3 timer guards confirmed ("Timer disabled — Neural Pulse active"), neurons firing in production (March 8, 2026)

---

## Prior Art Search Summary

| Innovation | Exists Elsewhere? | What's Different Here |
|-----------|-------------------|----------------------|
| Tool reliability contracts | No (SRE has service SLOs) | Per-tool, auto-generated, integrated with dispatch |
| Silent failure detection | No (chaos eng tests infra) | Per-tool-call, real-time, in dispatch loop |
| AI self-testing tools | No (CI tests human code) | Tests AI-synthesized tools before promotion |
| Bayesian tool posteriors | No (agents use point estimates) | Beta distributions with epistemic/aleatoric separation |
| Causal flow tracking | No (grounding scores exist) | Proves tool output actually reached response via anchor matching |
| Absence detection | No (cognitive science only) | First implementation in any AI agent |
| 5 metabolic states | No (System 1/2 only) | Five distinct cognitive parameter profiles |
| Per-user inverse reward | No (RLHF is group-level) | Real-time per-user from behavioral signals |
| Reasoning pattern cache | No (agents learn tool sequences) | Learns thinking strategies, not action sequences |
| Process Symbiosis (AXObserver) | No (all use pixels) | Semantic UI access vs screenshot+OCR+click |
| Autonomous curiosity | No (agents are reactive) | Self-directed gap identification and research |
| Experience-driven decisions | No (agents have memory) | Distilled wisdom from past attempts influences future boldness |
| Intent superposition | Research only (Anthropic/DeepMind) | Production implementation with disambiguation pipeline |
| User epistemic model | No | Tracks user's knowledge state per domain |
| Belief provenance | No | Tags every belief with source, flags low-credibility |
| Evidence triangulation | No (intelligence agencies only) | Cross-subsystem convergence detection |
| Diminishing returns detection | No (fixed iteration limits) | Information-gain-based early stopping |
| Intelligence ROI | No | Measures value of each cognitive subsystem |
| Narrative continuity | No (memory ≠ narrative) | Persistent story arc across sessions |
| Antifragile adaptation | No (agents log failures) | Converts failures into domain-specific antibodies |
| Peer-to-peer cognitive modulation | No (all use pipelines/controllers) | Cross-system resonance field where each system modulates others |
| Coherence-gated context injection | No (agents inject all context) | Token-budget-aware selective injection based on coherence state |
| Coherence-driven planning | No (fixed or simple heuristics) | Planning strategy biased by synthesized 5-system coherence signal |
| Coherence-aware background autonomy | No | Background agent decisions modulated by multi-system coherence field |
| Cognitive-state-aware tool selection | No (keyword/popularity only) | 5 alien systems steer tool boosts via metabolism, trust, gaps, intent |
| Compressed multi-signal meta-directive | No (agents inject loose context) | Single authoritative LLM instruction synthesized from 5 cognitive signals |
| Cognitive veto on tools | No (security gates only) | Appropriateness-based gating from domain trust, metabolism, narrative caution |
| Mid-request stance recomputation | No (single compute at start) | Full cognitive re-evaluation after consecutive tool failures |
| Alien-to-background-agent pipeline | No (scripted/scheduled only) | Background actions emerge from real-time 5-system cognitive interplay |
| Dream-time cognitive calibration | No (memory compression only) | Multiplexer calibration during sleep cycles from aggregated alien health |
| Pre-flight cognitive brief | No (agents inject loose context) | Synthesized self-awareness from 5 subsystems injected before LLM call |
| Pre-delivery validation gate | No (output filters for toxicity only) | Cross-references response against blind spots, calibration bias, user state, risk |
| Invisible pattern detection | No (agents learn from explicit feedback) | Dream-cycle cross-subsystem pattern discovery (failure, behavior, drift, regret) |
| Variational free energy computation | No (neuroscience only) | First FEP implementation in AI agent — surprisal across 4 dimensions |
| Active inference strategy selection | No (heuristic routing) | Strategy selection minimizing expected free energy (ambiguity + risk) |
| Continuously-updated generative model | No (agents have memory, not predictions) | Self-resetting predictive model with formal accuracy tracking |
| Precision weighting (biological attention) | No (Transformer attention is over tokens) | Learned attention over prediction dimensions — attend to reliable signals |
| Self-organized criticality | No (fixed parameters) | Automatic regime tuning toward edge of chaos via temperature dynamics |
| Surprisal-based resource allocation | No (uniform processing) | 0.5x-2.0x resource multiplier based on prediction error magnitude |
| Real-time cognitive regime switching | No (uniform iteration processing) | 4 regimes (flow/cautious/deliberate/emergency) with mid-request transitions |
| Counterfactual regret analysis | No (agents execute first plan) | Alternative generation, scoring, post-execution regret computation for learning |
| Parallel multi-perspective reasoning | No (single-perspective CoT) | 3-4 concurrent reasoning streams with confidence-weighted consensus merge |
| Evolutionary tool synthesis | No (agents use fixed tool sets) | Full lifecycle: observation → fitness tracking → promotion → retirement → mutation |
| Conditional failure prediction | No (reactive retry only) | Predictive P(failure) per step with time-aware, cascade-aware conditional risk |
| Neuromorphic timer mesh | No (independent timers everywhere) | Single coordinated pulse evaluating all background tasks with priority, CPU, idle gating |
| Circadian adaptive scheduling | No (fixed timer intervals) | Per-neuron per-hour EMA multiplier learns when background work is useful |
| Event-driven timer modulation | No (timers ignore context) | Semantic events (user idle, fact saved) reactively shorten neuron intervals |

---

## License

All inventions described herein are disclosed under the GNU Affero General Public License v3.0 (AGPL-3.0). Commercial licensing available from the inventor.

**This document constitutes prior art.** Any subsequent patent application covering substantially similar concepts is anticipated by this disclosure.

---

*Signed: Adel El-Ouariachi*
*Date: March 8, 2026*
*Repository: https://github.com/AdelElo13/JarvisMacApp*
