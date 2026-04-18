# CRAFT Recipe Library

Downloadable `.txt` copies of recipes published on [CRAFTFramework.ai](https://craftframework.ai). One file per recipe, stable URL, fallback for any AI that can't reach the live site.

---

## What this is

Every recipe on CRAFTFramework.ai has a matching `.txt` file in this repository. The `.txt` mirrors the full recipe content — intro, TL;DR, execution steps, recipe code, FAQ, and the AI-to-AI metadata block — in a single plain-text file.

The primary use case is AI tools that cannot reach the CRAFT website in-session (egress restrictions, offline runs, or any other reason a live fetch fails). Users download the `.txt`, attach it to their chat, and the AI proceeds with the same recipe content it would have read from the site.

Secondary uses: archival, offline review, citation in other work, pipeline ingestion.

---

## Using a recipe file

1. Open the recipe's page on [CRAFTFramework.ai](https://craftframework.ai).
2. Click the **Download recipe** link near the top of the page.
3. The link points here — raw GitHub content, single `.txt` file.
4. Save or copy the file, then attach it to your AI session or paste its contents directly.

The URL pattern is:

```
https://raw.githubusercontent.com/CRAFTFramework/craft-framework-recipe-library/main/{RCP-ID}-{SLUG}.txt
```

Any file matching this pattern is a recipe. Any file not matching it (a README, LICENSE, policy document, or format spec) is metadata about the library itself.

---

## Permanence

These URLs are meant to work for a long time, and CRAFT has committed in writing to the specific operational rules that keep them working. The commitments are enumerated in [PERMANENCE-POLICY.md](./PERMANENCE-POLICY.md) — six plain-English rules about what CRAFT will not do to these files or their URLs. The policy is version-locked: changes run through a documented amendment process, not a silent edit.

Permanence here is a policy outcome, not a technical guarantee. No file host can promise a URL forever; CRAFT can promise — and has promised — not to be the one that breaks it.

---

## Structure

All recipe files live at the repository root. Filenames follow the pattern `{RCP-ID}-{SLUG}.txt`. The `RCP-ID` encodes the cookbook and position within it; the `SLUG` freezes at creation and never changes (see PERMANENCE-POLICY P1).

### Cookbooks

Recipes are organized in three active cookbooks on CRAFTFramework.ai. The `.txt` files in this repo map one-to-one to their published recipe pages.

- **CAT-001 CORE.** Framework infrastructure recipes. Required for any CRAFT-enabled AI session. Filenames begin with `RCP-001-` or the `RCP-000-` foundational range.

- **CAT-CWK COWORK.** Recipes designed for Claude Cowork sessions. Filenames begin with `RCP-CWK-`.

- **CAT-CWK-ADM COWORK ADMIN.** Administrative and operational recipes for running a CRAFT project at scale, organized across eight volumes (setup, deployment, handoffs, lessons-learned, personas, specifications, and two development volumes). Filenames begin with `RCP-CWK-ADM-`.

### Finding a specific recipe

- From CRAFTFramework.ai: open the recipe page, click the download link.
- Directly in this repo: search by recipe ID or slug.
- Programmatically: construct the raw URL using the `RCP-ID-SLUG` from the recipe page and the URL pattern above.

---

## License

All recipe content in this repository is proprietary to Ketelsen Digital Solutions LLC and licensed via CRAFT Framework membership. See [`LICENSE`](./LICENSE) and [craftframework.ai/terms](https://craftframework.ai/terms).

Downloadable `.txt` format does not change the license. Files are provided to members for their own CRAFT-enabled AI sessions. Redistribution, republication, or use outside CRAFT membership terms is not permitted.

---

## Reporting issues

If a raw URL stops working, a file is missing that should be here, or you suspect a policy violation, open an issue against this repository. Violations and breakages will be acknowledged and either repaired or documented with a formal amendment.

For questions about the recipes themselves — execution, customization, composition — see [CRAFTFramework.ai](https://craftframework.ai) or the framework's support channels.

---

*This repository is part of the CRAFT Framework. Recipe pages live at [craftframework.ai](https://craftframework.ai); this library is the download-accessible complement.*
