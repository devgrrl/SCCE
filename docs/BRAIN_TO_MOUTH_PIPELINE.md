# Brain To Mouth Pipeline

Status: implemented single-lane boundary in an unfinished product; calibration remains provisional

## Contract

The SCCE runtime must follow one inspectable lane:

1. source evidence and typed observations
2. graph/hyperedge admission and alpha-normalized field/frontier activation
3. directed PPR and configured PowerWalk expansion
4. learned turn-requirement field
5. cognitive-operator activation
6. bounded proposals containing claims, relations, steps, and artifacts
7. per-claim basis classification
8. candidate generation and requirement-aware judge selection
9. entailment, truth state, certification, and slot planning
10. one bounded support-recovery transition when the selected route is under-supported
11. terminal low-support policy selection after acquisition exhaustion
12. semantic Mouth realization and final Walsh surface gate
13. typed critic and at most two revision rounds when needed
14. emitted answer plus durable basis-aware events and trace

The Mouth is realization-only. It receives selected semantic slots, relations, force, and evidence bindings. It may realize creative material already authorized by the planner, but it may not select facts, invent factual support, manufacture citations, or expose control identifiers as prose.

## Runtime Boundaries

- Kernel orchestration: packages/kernel/src/kernel.ts
- Retrieval scoring: packages/kernel/src/retrieval.ts
- Candidate scoring: packages/kernel/src/candidate.ts
- Requirement field/operator activation: packages/kernel/src/turn-requirements.ts
- Cognitive proposal planning: packages/kernel/src/cognitive-planner.ts
- Requirement-aware judging: packages/kernel/src/judge.ts
- Certification checker: packages/kernel/src/semantic-proof-engine.ts
- Truth contract: packages/kernel/src/truth-contract.ts
- Entailment propagation: packages/kernel/src/entailment.ts
- Mouth planning/realization: packages/kernel/src/mouth.ts
- Surface energy ranking: packages/kernel/src/walsh-surface-energy.ts
- Bounded answer revision: packages/kernel/src/answer-revision.ts

## General-Cognition Boundary

The requirement field has 16 dimensions. Its evidence is learned frame, pattern,
phrase-unit, dialogue-move, and construct activation with character and UTF-8 byte
spans, plus explicit structured requirements when supplied. It does not classify a
turn from English command verbs. The field activates 17 cognitive operators, and only
operator-supported work becomes a cognitive proposal.

Each proposal preserves requirement coverage and typed claim bases:
`direct_evidence`, `source_synthesis`, `reasoned_inference`, `causal_inference`,
`temporal_inference`, `counterfactual`, `learned_prior`, `invented`, `conjectured`,
`translated`, `action_result`, or `unsupported`. Candidate and judge code may select
among those proposals; the Mouth may only realize the selected meaning and force.

The revision coordinator critiques the realized answer against the requirement field,
selected proposal, claim bases, citations, validation results, action receipts, and
surface invariants. It runs zero, one, or two rounds. A proposed revision is rejected
unless it improves quality by at least `0.025`; citation mismatch, test weakening,
action without a receipt, and telemetry leakage are hard failures.

## Bounded Low-Support Recovery

Low support is a transition condition, not a final answer. Before Mouth realization, the kernel may take one bounded recovery transition:

```text
under-supported candidate
-> learn from eligible local state or perform configured search/fetch
-> canonical typed ingestion with provenance and temporal metadata
-> graph/frontier update
-> replan once
```

The transition may not bypass canonical ingestion, promote unbound fetched text directly to evidence, or retry indefinitely. Replanning can select a source-backed correction or a qualified reasoned/prior-bound answer. A negative factual answer requires contradiction evidence or a temporally incompatible/earlier proof path; absence of positive support alone is not proof of negation.

If the acquisition attempt is exhausted and a factual or reasoned turn remains under-supported, the current user policy licenses one bounded creative continuation. Admission requires all of the following:

- active learned graph or language priors contribute semantic material not copied from the request;
- the candidate passes non-echo, risk, and unsupported-fact gates;
- every creative claim carries `invented` basis;
- the evidence set is empty and provenance is `generated_not_evidence`;
- no factual certification is attached.

This policy does not turn an empty runtime into a knowledge source. When connector, graph, and language state are all empty, the planner selects a non-assertive terminal answer limited to source-derived content that actually exists, and the Mouth realizes it. Hardcoded prose and fabricated factual content are not recovery mechanisms.

## Evidence and Truth Gating

- SCCE can answer without proof. It cannot represent unsupported output as proved.
- Every emitted answer carries an answer basis: sourced, reasoned, prior-bound, creative, speculative, or unsupported.
- Certification verdicts are mapped to typed truth state when certification is attempted.
- Unsupported truth states are treated as under-supported in assistant-force gating.
- Source-bound and certified states can surface factual language; unsupported states cannot claim certification.
- Terminal creative continuation is explicitly invented, evidence-free, and non-certified even when it follows a factual or reasoned request.

## Mouth Preservation

- Semantic preservation scoring is applied across generated candidates.
- Surface candidates are realized from semantic values and learned language memory, not from semantic role IDs or hardcoded fallback sentences.
- Forbidden/drift/leak checks penalize or reject candidates.
- Proof, validation, receipt, and control state remain structured rather than being appended to answer prose.
- Surface energy rows include score traces for inspection.
- The final Walsh/surface gate is rerun after realization transforms; a failed final surface is not emitted.
- An empty Mouth surface is an internal continuation signal for kernel recovery/replanning or terminal selection, not a final user response.

## Trace Surfaces

The following runtime artifacts are emitted for inspection:

- retrieval score traces
- candidate score traces
- surface-energy score traces
- selected mouth candidate and preservation score
- answer basis and certification marker
- turn-requirement field and contributing activation spans
- cognitive-operator activation rows
- cognitive proposals, per-claim bases, and selected proposal
- typed revision defects, attempts, and disposition

## Current mathematical status

- Unconfigured α thresholds are deterministic Type-7 quantiles over the active relation-strength slice. They are relative normalization, not externally calibrated admissibility.
- Directed PPR has an independent dense linear oracle in tests. PowerWalk uses deterministic second-order transitions and content-addressed train/validation partition identity; learned PPMI representations expand production field seeds.
- Configured relation-potential scoring reaches the production field and uses disjoint coefficient-training, calibration-fit, and holdout folds. No representative fitted model is configured, so the normal fallback is identity and no uplift is claimed.
- Requirement-field, operator, reasoning, invention, proposal-diversity, judge, and Mouth coefficient sets are versioned and traced, but the checked-in defaults are bootstrap/provisional rather than representative outcome-fitted models.
- Answer-level calibration remains explicitly `uncalibrated` where no task-specific calibration model is loaded.

## Launch Safety Notes

- No cloud inference required.
- No external retrieval-to-prompt fallback path.
- No second runtime lane.
- Postgres remains canonical durable store.
- Local checks establish only the contracts they execute.
