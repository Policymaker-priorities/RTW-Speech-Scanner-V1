# Handover: Economics policy statements

*Written 2 November 2026 by Xavier Fletcher, at the end of their time on the project.*

**The question:** do economists accurately know what policymakers want from research? This repository builds one input to that study: verbatim policy statements by the heads of UK departments and US agencies.

**"Economics-relevant" is deliberately broad.** A statement qualifies if it is a policy choice that economics research could produce evidence about, in any field (crime, health, defence and so on). It is not limited to money and markets. See H-99 in the decision log.

**Companion project:** which research policy documents cite, in [RTW-Overton-Analysis](https://github.com/xav-fl/RTW-Overton-Analysis).

## Where things stand

| Piece | Status |
|---|---|
| Final dataset | **Done for July 2026:** 311 statements (172 UK, 139 US) in [`datasets/speeches_jul2026.csv`](datasets/speeches_jul2026.csv) |
| Documents | **Collected for January–July 2026:** about 6,600 documents |
| Codex bundle (Codex, not Claude, runs the pipeline over all those documents) | **Sent out:** v4 was tested on 10 October 2026 and shared with the project leads through Google Drive. **Check whether they ran it** |
| JEL protocol v2.0 | **Written, never run on a real model.** It sits on the `jel-v2` branch |
| Quote context kit | **Done, but untested on a real model.** It is a stand-alone tool for the project leads, in [`quote-context-kit/`](quote-context-kit) |

## What to do next

1. **Find out what happened to the Codex run.** Results should be in the `returns` folder of the shared "Codex Bundle" Drive folder, as `eps-output.zip`. Ask the project leads whether it ran. Xavier's repository records do not show this.
2. **Decide which dataset is the real January–July one.** Codex output uses a different model for every judgement, so it is not directly comparable with the July dataset. If January–July is needed with Anthropic models, run `main` over the full period, which costs API credit.
3. **Decide on JEL v2.0.** The published dataset uses v1. To adopt v2.0, test `jel-v2` on a small run and compare it with v1 before merging. `codex-native-jel-v2` is the Codex equivalent.
4. **Tidy up** using the list under "Known problems".

## Decisions you should not undo by accident

- **The model never writes the quote.** It returns pointers into the source document, and code copies the text, so every quote is verbatim.
- **Changing an extraction prompt mid-run invalidates the cache and re-bills finished documents.** Prefer fixes in the validation step.
- **Bracketed context in `quote_in_context` is checked word for word against the source.**
- **Every design choice has a numbered entry** in [`docs/DECISIONS.md`](docs/DECISIONS.md) (H-1 to H-101). Add to it. H-102 to H-114, on the `codex-native` branch, cover the Codex variant.

## Known problems

- **Three tests fail on `main`,** all long-standing and all in `tests/test_pipeline.py`: `test_cross_paragraph_units_rejected`, `test_press_release_quoted_passage_is_attributable` and `test_attribution_frame_trimmed_from_press_release_quote`. The other 313 pass and 1 is skipped.
- **Outdated instructions:** `RUNNING.md` has paths from Xavier's machine, and `TESTING.md` expects an old test count.
- **Stale branch:** `initial-upload-branch` on GitHub is old and fully contained in `main`, so it can be deleted.
- **Lots of old runs:** in `scanner-code/eps-pipeline/eps/runs/`, only `jul2026-uk` and `jul2026-us` produced the final dataset. The rest are pilots and trials.

## Access you will need

- **GitHub:** this repository is public under Xavier's personal account (`xav-fl`). Pushing needs collaborator access or a transfer.
- **Anthropic API key** (`ANTHROPIC_API_KEY`) for `main`. Runs bill per call, and an earlier run on this project stopped when credit ran out. The same command resumes it.
- **Google Drive:** the "Codex Bundle" folder belongs to Xavier, so ask for access. The bundle zips are not in this repository, but `codex-native` and its tags `codex-bundle-v1` to `v4` hold what built them.

## Where to find things

| What | Where |
|---|---|
| Overview and repository layout | [README.md](README.md) |
| Dataset columns | [datasets/README.md](datasets/README.md) |
| Intention labels | [docs/INTENTION_CODEBOOK.md](docs/INTENTION_CODEBOOK.md) |
| Decision log | [docs/DECISIONS.md](docs/DECISIONS.md) |
| Running the pipeline | [scanner-code/eps-pipeline/eps/RUNNING.md](scanner-code/eps-pipeline/eps/RUNNING.md) |
