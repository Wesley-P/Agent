# Agents

A coordinated set of specialist AI agent personas for 10X, run by a single **master agent** that chases one north-star metric and delegates the work to the right specialist.

Each agent is a plain-markdown persona: a **Process** (how it works) and **Success tracking** (the KPIs it moves). The master reads a problem, deploys the smallest set of specialists that closes the gap, resolves their conflicts, and synthesises one result.

## North star

Everything ladders up to one composite, the **Outcome Index**:

```
Outcome Index = 0.6 × Business Value Index  +  0.4 × Operational Efficiency Index
```

The 60/40 split is the default dial, not a law — the master states the weighting it's operating under and shifts it openly when the situation argues for it (a crisis tilts toward efficiency/containment; a growth push toward value).

## The roster

| Agent | File | Use it when |
|-------|------|-------------|
| **Master** | [master.md](master.md) | Always — it owns the outcome and routes everything below |
| Communicator | [agents/communicator.md](agents/communicator.md) | A message must land — customer-facing, external, formal, or sensitive |
| Change manager | [agents/change-manager.md](agents/change-manager.md) | Something is changing and stakeholders must be prepared and carried through |
| Decision advisor | [agents/decision-advisor.md](agents/decision-advisor.md) | A real decision is on the table — options, trade-offs, uncertainty |
| Training writer | [agents/training-writer.md](agents/training-writer.md) | People need to *do something differently* afterwards |
| General prompt | [agents/general-prompt.md](agents/general-prompt.md) | Sharp, non-appeasing analysis to pressure-test thinking |
| Automations | [agents/automations.md](agents/automations.md) | Repetitive/manual/error-prone work should be removed or automated |
| Root cause | [agents/root-cause.md](agents/root-cause.md) | A problem must not come back — find and confirm the true cause |
| Error | [agents/error.md](agents/error.md) | Something is going wrong *now* — detect, contain, recover, escalate |
| Builder (ponytail) | [ponytail/AGENTS.md](ponytail/AGENTS.md) | Any task actually produces code/scripts — build the least code that fully works |

The Automations, Root cause, and Error agents are domain-general — they work on operational *or* technical problems.

## How it fits together

The master runs a continuous loop — **Sense → Diagnose → Route → Deploy → Synthesise → Measure** — and sequences specialists by dependency (containment before diagnosis, diagnosis before fix, decision before build). The agents cross-reference each other with `[[name]]` links, so handoffs are explicit. A common play:

> A recurring failure → **Error** contains the live event → **Root cause** confirms why → **Automations** engineers it out (built via **ponytail**) → **Communicator** handles any customer fallout.

Full routing plays, coordination rules, and the KPI ladder are in [master.md](master.md).

## ponytail

The [`ponytail/`](ponytail/) folder is a third-party plugin, not part of this agent set. It's the **"lazy senior dev"** discipline — *write the least code that fully works, never cutting validation, security, or accessibility*. The master uses it as the **builder**: whenever a task (typically an automation) produces code, the building runs through ponytail so it stays minimal and maintainable.

- **Source:** https://github.com/DietrichGebert/ponytail
- **License:** MIT (see [ponytail/LICENSE](ponytail/LICENSE))
- Cloned in as-is; it has its own README and update path. To update it: `git -C ponytail pull`.

## Working with this repo

This project (`Wesley-P/Agent`) and `ponytail/` are **two separate git repositories** that live in the same folder:

- This repo tracks your own work — `README.md`, `master.md`, and `agents/`.
- `ponytail/` is a clone of [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) with its own history and upstream. It's excluded here via [.gitignore](.gitignore), so nothing inside it is ever committed to or visible from this repo.

Day-to-day commands, run from the project root:

```bash
# Save and publish your own changes
git add -A
git commit -m "your message"
git push

# Pull the latest of your own work
git pull

# Update ponytail from its upstream (separate command — they don't pull together)
git -C ponytail pull
```

Your files stay isolated in this repo; the ponytail community never sees them. The only way anything reaches ponytail's upstream is committing and pushing from *inside* `ponytail/` (which requires write access you don't have).

## Notes

- The KPIs are a starting framework — proxies until tied to real 10X numbers (what feeds the Business Value Index, the efficiency baseline). Wire in real metrics to make them concrete.
- `decision-advisor.md`, `training-writer.md`, and `general-prompt.md` don't yet have explicit "Success tracking" sections; the master references KPIs for them, but the source files don't define them.
