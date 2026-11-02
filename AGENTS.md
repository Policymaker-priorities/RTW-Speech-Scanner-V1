# Instructions for AI agents

Read [HANDOVER.md](HANDOVER.md) first: it gives the current state and the ordered next steps. Then use [README.md](README.md) for the layout. The pipeline is in `scanner-code/eps-pipeline/eps`.

## Rules

- **Tests:** run `python -m pytest` from `scanner-code/eps-pipeline/eps` before and after changes. Three failures in `tests/test_pipeline.py` are known and listed in the handover. Anything else is new.
- **Quotes:** a model must never write quote text. Quotes are copied from the source by code.
- **Prompts:** changing a prompt invalidates the response cache and re-bills finished documents, so prefer validation-side fixes and confirm first.
- **Relevance:** judge "economics-relevant" by whether economics research could inform the policy choice, not by topic. See H-99 in `docs/DECISIONS.md`.
- **Costs:** full runs use paid API credit or Codex usage. Confirm before starting one.
- **Branches:** do not mix `main` (Anthropic models) with `codex-native` (Codex). Their outputs are not comparable.
- **Decisions:** add a numbered entry to `docs/DECISIONS.md` for any design decision. Never commit API keys.
- **Keep it current:** update HANDOVER.md when the state or next steps change.
