# 0004 — Public control repo, with v1 restricted to public/non-sensitive targets

- **Status:** Accepted
- **Date:** 2026-10-01
- **Deciders:** operator
- **Related:** `DESIGN.md` §1, §5.1, §12, §13.1

## Context

The control repo holds far more than the control plane: the specification files, the
workflows, the board (tracking issues), and the **session logs** — verbatim reasoning
traces that may quote repository content. Its visibility therefore decides the
visibility of all of that.

A **public** control repo is simple and transparent, but a public board and public
session logs about a *private* target repository would leak that repository's existence,
its file contents, and reasoning about it. The requirement that session logs be readable
"only to mission operators" is incompatible with a public repo unless the targets
themselves are public.

## Decision

The control repo is **public** in v1 — control plane, board, and session logs alike —
and v1 **targets only public / non-sensitive repositories**. The constraint is enforced
**in the specification's scope** (`visibility: public`, a `private: false` criterion),
so a mission cannot be created against a private repository; the check is a required
rubric item at freeze.

## Consequences

**Positive**
- Transparency and simplicity: one repo, no segmentation, no separate private store.
- Session logs can be committed to the control repo for a durable audit trail.
- The privacy rule is enforced by construction, not by convention.

**Negative**
- v1 cannot be used on private or sensitive repositories at all; such a mission is
  refused.
- If that restriction is ever relaxed, session logs and raw board evidence must move to
  private storage, and the board must stop carrying raw content snippets — a follow-up
  decision, not a small change.
