# BALROG parity proposal for PR #117

**Status: PROPOSED_NOT_APPROVED_NOT_RUN.** We request review of the experiment and private credential provisioning. No real-model parity or paid model run has been performed or authorized by this proposal. `parity_experiment.json` remains `[]`.

The [machine-readable plan](plan.proposed.json) binds all 255 task IDs, manifest hashes, native budgets and proposed settings. The [adapter specification](../../../docs/adapters.mdx) requires matched runs and an additional standard-agent evaluation for a custom-agent adapter.

## Primary matched comparison

Use the original BALROG **naive** agent at `b7afe79e3e4265811cfa985ed7c95c4d1a11e3f5` on both sides: original `Evaluator.run_episode` versus the implemented Harbor `balrog-native` bridge. Preserve the same public text, prompts, action handling, model parameters, dependencies, seeds and native progression. Models receive no privileged oracle state.

Proposed model: **`gpt-4o-mini-2024-07-18`**, through 2077ai's proposed endpoint `https://app.ppapi.ai/v1`, with temperature 1, maximum output tokens 8,192 and text history 16. Exact snapshot availability is **unconfirmed**; there will be no silent alias substitution. [Proposed settings](settings.proposed.json) are nonsecret and require confirmation.

| Environment | Fixed cases | Original seeds | Native action limit |
|---|---:|---|---:|
| BabyAI | 50: 5 types × 10 | 0–9 | 64 or 128 by type |
| Baba Is AI | 120: 40 types × 3 | 0–2 | 100 |
| TextWorld | 30: 3 types × 10 | 0–9 | 80 |
| Crafter | 10 | 0–9 | 2,000 |
| NLE | 5 | 0–4 | 100,000 |
| MiniHack | 40: 8 types × 5 | 0–4 | 100 |

NLE's native inactivity timeout of 150 calls without a game-clock advance also remains unchanged; it is not 150 elapsed game turns or a reward-progress timeout. This is a fixed selected scope, not the full universe of possible benchmark worlds. No cases are filtered by model or oracle success.

## Ordered stages and cost gates

| Stage | Per side | Both sides | Gate before launch |
|---|---:|---:|---|
| Paired sanity | 10 selected tasks | 20 episodes | Confirm exact selection and finite sanity limits |
| First full pair | 255 tasks × 1 run | 510 episodes | Review both sanity sides; approve full-pair limits |
| Two additional pairs | 255 tasks × 2 runs | 1,020 episodes | Review one complete run on each side; approve scale-up |

Primary total: **1,550 episodes**, of which **1,530** enter formal statistics. Complete each pair before advancing; do not run all three repetitions on one side first. Sanity executions do not enter formal arrays.

The ten sanity IDs are fixed in the JSON: seed 0 of BabyAI `goto` and `putnext`; Baba Is AI `make-win` and `two-room-make-you-make-win`; TextWorld treasure hunter and cooking; Crafter; NLE; and MiniHack MazeWalk 9×9 and Quest Easy. They cover interaction families across all six environments without selection by success. The current `--split sanity` selects **58** tasks, so the public launchers need explicit task-ID selection before this smaller paid stage.

Start at concurrency **1**, with no automatic job retry. Request finite cost, token and runtime limits for each stage, plus provider RPM/TPM/account quotas and an agreed retry allowance. No provider price or dollar estimate is assumed. The sum of native action allowances is 543,520 per full side and 3,466,624 across the proposed primary executions; these are theoretical logical-call ceilings excluding retries, **not usage forecasts or spending permission**. NLE dominates this bound. Measure sanity usage and retry costs before estimating later stages; stop at approved limits and preserve incomplete attempts.

## Decisions needed before paid execution

1. **Original scope and outstanding oracle gate.** The [migrated reference run](../docs/separate_verifier_full_validation.md) completed 255/255 with zero exceptions, but contains 239 full-score oracles and 16 diagnostics. It is not 100% full-score validation or model parity. Confirm the treatment below before accepting the guide's oracle prerequisite.
2. **NLE and MiniHack.** Keep NLE's original scorer and explicitly partial references, or agree an upstream ascension-event correction on both sides? Its implemented reachable-key ceiling is 0.8067964442444019; no rescaling is proposed. Keep MiniHack's original 100-action instance with the documented unresolved case, or approve a symmetric new Boxoban budget revision? These changes remain unapplied. See the [NLE](../docs/nle_scoring_review.md) and [MiniHack](../docs/minihack_seed_and_budget_review.md) reviews.
3. **Crafter oracle and grading policy.** Review the separate [V45 privileged-reference evidence](../docs/crafter_v45_validation.md). Acceptance and production promotion remain pending. Its Harbor runs used privileged reference access and the explicit native-state fallback (`replay_verified=false`), not exact fresh replay. Separately approve the [trusted native-state fallback](../docs/crafter_scoring_review.md) for upstream object-order replay nondeterminism; preserved native scoring does not establish deterministic replay. V45 is reference evidence, not the model agent or a parity result.
4. **Model, platform and credentials.** Confirm the dated model, effective settings and limits. The team's proposed formal platform is Daytona on both sides. Only local Docker is currently implemented and reference-tested; first validate the game sidecar, collection hook and separate verifier on Daytona. If a platform blocker arises, obtain approval for an alternative rather than mixing platforms. Provide 2077ai and Daytona credentials through a private secret channel—never a PR comment or committed file.
5. **Standard CLI agent.** Scenario 3 also requires a standard-agent evaluation. Please select a pinned Codex or Claude-Code version/model, coverage, repeats and separate budget, and confirm whether the current task interface or a separate compatibility dataset should be used. Harbor supplies these agents; this adapter has no validated CLI-agent experiment/config/results yet. Its counts and costs are excluded from the primary totals above.

Before launch, freeze the reviewed adapter commit, task/runtime/image hashes, model and effective settings; recheck the Harbor revision. Version 0.26.0 is the completed local reference baseline, not a promise about future upstream releases. Validate the launchers against the agreed configuration schema, including top-level `n_concurrent_trials`, alongside the explicit sanity selection. The proposed 1,800-second outer deadline must also be agreed on both sides; infrastructure expiry cannot become a task score or a shorter native budget.

## Reporting and failure handling

For each complete run, report native progression per environment and the equally weighted mean of six environment means, not a flat mean over unequal task counts. After three runs per side, report **mean ± sample SEM**, `sqrt(sum((x-mean)^2)/(n*(n-1)))`, with raw run arrays. One run has no defined SEM. Check range overlap for each environment and the aggregate; overlapping SEM intervals alone do not satisfy the repository criterion. All-zero outcomes are weak evidence and trigger review rather than an automatic parity claim.

Preserve genuine agent failures at their native score. Record infrastructure errors separately, preserve every attempt and usage record, and never replace a missing result with zero or retain only a better retry. Configuration changes create a new paired experiment revision. Publish reproducible commands, redacted trajectories, token usage, costs and authentic artifact links only after results exist and publication is authorized. Existing oracle, AutoAscend and privileged-controller research stays separate from model parity.
