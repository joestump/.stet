# `.stet` — Joe's personal Stet configuration

This is the `$USERNAME/.stet` tier of the [Stet](https://github.com/joestump/stet)
configuration topology (ADR-0015), following the `.github` convention: a versioned
repo holding the three Stet primitives that resolve across user → org → project:

| Primitive | Where | What |
|---|---|---|
| **Agents** | `agents/` | Named, versioned actors — harness + model + persona + skills + verbs + guardrails (ADR-0016) |
| **Verbs**  | `verbs/`  | Emoji markup verbs binding to declarative workflows (ADR-0005) |
| **Skills** | `skills/` | Reusable, distilled instructions injected into dispatches (ADR-0012) |
| **Workflows** | `workflows/` | The declarative definitions verbs bind to via `workflowID` (ADR-0005) |

Configs are plain YAML (ADR-0017). Other `.stet` repos can `import` this one,
pinned to a ref; downstream policy may require the pinned SHA be GPG-signed.

> **Status:** the tiered resolver is still in design (stet spike #11/#12); today
> Stet ships a single-tier in-app config. This repo lands the convention ahead of
> the code so the shapes are real and dogfooded from day one.

## How `workflowID` resolves

A verb's `workflowID` is a **symbolic key, not a file path**. Resolution order
(once the tiered resolver lands): project `.stet` → org `.stet` → this repo's
`workflows/<id>.yaml` → the app's bundled defaults. Today the app resolves only
its bundled registry (`BundledWorkflows`, embedded YAML); the `workflows/` here
mirror those defaults verbatim so this repo is self-contained and ready to
diverge from them.
