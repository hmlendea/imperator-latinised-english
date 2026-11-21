# Ambiguities and open questions

Items that repository evidence does not resolve, or that the maintainer must decide. Each records what is known, what is unknown, and the impact.

## Engine-contract items

| # | Question | Known | Unknown | Impact |
|---|----------|-------|---------|--------|
| Q1 | Exact `replace` precedence mechanism | The `replace` subtree is applied after other sources; every shipped override lives there | Whether precedence is guaranteed by directory name, by a load phase, or by both | A future engine change could alter precedence silently |
| Q2 | Trackers beyond the observed range | Observed trackers `0`–`7`; `:0` dominates (7,198 of 8,691) | What trackers `1`–`7` mean, and whether they must be preserved exactly | An incorrect tracker could change string interpretation |
| Q3 | Duplicate-key semantics | Only one record per key was authored; no duplicates were found | Whether the last or first record wins | Matters only if duplicates are ever introduced |
| Q4 | Behaviour of an unknown key | Absent from any shipped file | Whether an unknown key is dropped silently or logged | Affects the diagnostic model for E7 |

## Authoring items

| # | Question | Known | Unknown | Impact |
|---|----------|-------|---------|--------|
| Q5 | Threshold for a substitution | A record is shipped only when a latinisable substitution preserves meaning and grammar | Whether any written rule exists beyond maintainer judgement | Reviewers must reproduce the sense judgement independently |
| Q6 | Rejection rationale | Rejections are omissions with no record | Why a specific record was left at vanilla | Distinguishing deliberate suppression from an oversight requires re-deriving the substitution |

## Coverage items

| # | Question | Known | Unknown | Impact |
|---|----------|-------|---------|--------|
| Q7 | Whether more coverage is planned | Coverage is partial by design; `README.md` states it is expanded file by file | Whether remaining files are intended for future coverage | No roadmap exists to state intent |
| Q8 | Metrics provenance | `.temp/vanilla_files.md` states 9,347 of 62,528 | The recomputed shipped count is 8,691 records | A discrepancy of 656 records between the tally and the shipped corpus |
| Q9 | The `.temp` tally accuracy | It lists per-file counts | Whether the discrepancy is from later edits or a counting difference | Should be recomputed before being cited |

## Documentation items

| # | Question | Known | Unknown | Impact |
|---|----------|-------|---------|--------|
| Q10 | Presence of a `ROADMAP.md` or `CHANGELOG.md` | Neither exists | Whether they are planned | Planning and change history are not recorded |
| Q11 | Localisation status wording | `README.md` and the Workshop page state "Partial (In progress)" | The definition of "in progress" as a completion target | Status is qualitative |

## Distribution items

| # | Question | Known | Unknown | Impact |
|---|----------|-------|---------|--------|
| Q12 | Whether all three channels publish every release | All three workflows trigger on `v*.*.*` tags or manual dispatch | Whether the maintainer dispatches all three each release | A given release may be published to a subset of channels |
| Q13 | Descriptor sync enforcement | Both descriptors are currently identical | Whether any check enforces it | Drift is possible without detection |

## Recommended resolutions

1. Recompute the coverage tally from the shipped corpus and update `.temp/vanilla_files.md` (Q8, Q9).
2. Decide whether a `ROADMAP.md` should record remaining coverage intent (Q7, Q10).
3. Document the engine `replace` mechanism from an authoritative source if one is available (Q1).
4. Add a descriptor-equality check to the release procedure if drift is a concern (Q13).
