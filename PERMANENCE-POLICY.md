# CRAFT Recipe Library — Permanence Policy

This repository hosts downloadable `.txt` copies of every recipe published on CRAFTFramework.ai. Each recipe has a stable URL of the form:

```
https://raw.githubusercontent.com/CRAFTFramework/craft-framework-recipe-library/main/{RCP-ID}-{SLUG}.txt
```

URL stability on the public internet is not a technical guarantee — no file host contractually promises that a URL will resolve to the same content in perpetuity. What CRAFT can do, and what this document commits to, is enumerate the specific operational behaviors we will not take against these files. The permanence of these URLs rests on the rules below.

This policy is public, auditable, and version-locked. Users, partners, and AIs that consume CRAFT recipes can rely on it — and hold CRAFT accountable when it changes.

---

## The six commitments

**P1. We will not rename a recipe `.txt` file.**

Once a file is committed under a given `{RCP-ID}-{SLUG}.txt` name, that name is permanent. The `{SLUG}` portion freezes with the recipe ID at creation. Rewording the recipe title later does not rename the file. A file renamed on GitHub breaks every external reference to its raw URL.

**P2. We will not delete a recipe `.txt` file.**

Deprecating a recipe does not remove it. A deprecated recipe keeps its `.txt` file in place, updated to carry a deprecation banner at the top with the date, reason, and a link to the successor recipe (if any). This mirrors the CRAFT recipe lifecycle principle that no recipe is ever erased from the record (see SPEC-RECIPE-LIFECYCLE in the CRAFT project repo). Bookmarks, citations, and in-progress work relying on a deprecated recipe continue to resolve.

**P3. We will not rename the CRAFTFramework GitHub organization.**

The hostname component of the raw URL (`raw.githubusercontent.com/CRAFTFramework/...`) depends on the org name staying `CRAFTFramework`. Any org rename would break every URL served from this repo. A future migration off GitHub, if one ever becomes necessary, is a policy change — not a silent event — and follows the change-control process below.

**P4. We will not rename the `craft-framework-recipe-library` repository.**

Same reason as P3, one level deeper. The repo slug is part of every URL.

**P5. We will not rename the default branch.**

The branch name `main` is baked into every URL. We will not migrate to a differently-named default branch.

**P6. We will not use GitHub's built-in redirects or branch moves.**

GitHub provides "silent" compatibility features — rename-with-redirect for repos, automatic forwarding for renamed users or orgs — that preserve links while allowing the underlying name to change. We will not rely on these. Using a redirect to paper over a rename is, in effect, a rename; both are forbidden. Any change to P1–P6 runs through the change-control process below — there is no inline exception.

---

## Auditability

Every commitment above is falsifiable. Anyone can verify compliance:

- **File renames (P1) and deletions (P2)** — visible in this repo's commit history. A rename or delete appears as a discrete commit with the author, date, and (in the case of a rename) both the old and new path. If you see one, the policy has been broken.
- **Org, repo, and branch renames (P3–P5)** — visible in GitHub's public activity log and in the repo's URL itself. If the URL pattern stops working, something changed.
- **Redirect usage (P6)** — the first page users are redirected to should not be a GitHub-provided redirect. If a raw URL transparently resolves via redirect to a different path, that is a policy violation.

Anyone who discovers a policy violation is invited to open a public issue against this repo. Violations will be acknowledged and either repaired (if possible) or documented with a formal amendment (see below).

---

## Change control

This policy is version-locked. Changes to any of P1–P6 require:

1. A dedicated subproject action in the CRAFT project management system (a new subproject or a formal amendment to SP08, with explicit approval from the project owner).
2. A dated amendment section appended to this document, explaining what changed and why.
3. A commit message on this file that references the amendment.

Editorial fixes (typos, clarifications that do not alter the commitments) can be made as normal commits with a clear commit message and no P-commitment change. These do not require amendment.

If CRAFT ever decides to retire this download library, that decision itself is a change requiring amendment. The existing files stay in place; they do not disappear.

---

## Scope

This policy covers recipe `.txt` files served from this repository and the URL pattern that serves them. It does not cover:

- Recipe content on CRAFTFramework.ai itself (governed separately by the recipe lifecycle specification).
- Other CRAFT repositories.
- Membership, licensing, or terms-of-use (see `craftframework.ai/terms` and the `LICENSE` file in this repo).
- Technical availability guarantees from GitHub (we do not control, and therefore do not promise, GitHub's uptime or API stability).

---

## Version history

- **v1.0** — 2026-04-17 (SP08 Phase 1, H019). Initial policy committed.

---

*This policy is part of the CRAFT Framework's auditable-pillar work. For questions about the policy itself, see the CRAFT project handoff record. For questions about the recipes, see `craftframework.ai`.*
