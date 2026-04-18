# CRAFT Recipe `.txt` Format Specification

**Version:** 1.0
**Status:** LOCKED for Phase 1 specimen publication. Schema-level changes follow the amendment process in PERMANENCE-POLICY.md.
**Applies to:** every recipe `.txt` file served from this repository.

This spec defines the structure of every recipe file in this library, so that a human, an AI, or an automated parser can locate any section of any recipe without guessing. The section order mirrors the published recipe page on CRAFTFramework.ai — downloading a `.txt` gives the same content in the same order as reading the page, top to bottom.

---

## 1. File-level conventions

| Item | Value |
|---|---|
| Character encoding | UTF-8 |
| Byte-order mark | None (no BOM) |
| Line endings | LF (`\n`) only — no CRLF |
| Max line width | Soft 80 columns for prose; not enforced for code blocks, URLs, or table content |
| Filename | `{RCP-ID}-{SLUG}.txt` — both `RCP-ID` and `SLUG` freeze at creation (PERMANENCE-POLICY P1) |
| Filename case | Uppercase for `RCP-ID` and `SLUG` segments; hyphens as separator; no spaces; no underscores |
| File extension | `.txt` only |

Example filename: `RCP-000-000-006-FIRST-PRINCIPLES-INNOVATOR.txt`

---

## 2. Top-of-file header block

Every file begins with a header block containing the license and file-level metadata. The header is fixed in structure so that parsers can locate it deterministically.

### 2.1 License block (first 9 lines, verbatim)

```
# ===========================================================
# CRAFT Framework Cookbook - Proprietary Content
# ===========================================================
# SPDX-License-Identifier: LicenseRef-CRAFT-Proprietary
# (C) 2025-2026 Ketelsen Digital Solutions LLC.
# All Rights Reserved.
# CRAFTFramework.ai - Licensed via membership.
# Terms: craftframework.ai/terms
# ===========================================================
```

Do not edit. Do not translate. Do not add lines between the dividers. This exact block appears identically in every file.

### 2.2 File metadata block

Immediately after the license block, separated by one blank line, comes the file metadata block. Format is commented key-value pairs, one per line, readable as a loose YAML subset:

```
# FILE METADATA
# --------------------------------------------------------
# recipe_id:         RCP-000-000-006
# slug:              FIRST-PRINCIPLES-INNOVATOR
# recipe_title:      First Principles Innovator
# cookbook:          CAT-001 CORE
# canonical_url:     https://craftframework.ai/rcp-000-000-006-first-principles-innovator/
# download_url:      https://raw.githubusercontent.com/CRAFTFramework/craft-framework-recipe-library/main/RCP-000-000-006-FIRST-PRINCIPLES-INNOVATOR.txt
# library_entered:   2026-04-17
# last_updated:      2026-04-17
# file_format_ver:   1.0
# ============================================================
```

Required keys: all listed above. A parser encountering a missing required key should treat the file as malformed.

### 2.3 Lifecycle status block

Immediately after the metadata block, separated by one blank line. Present on every file. Structure depends on the recipe's current lifecycle stage (see SPEC-RECIPE-LIFECYCLE §3):

**For active recipes (EXPERIMENTAL / TESTED / OFFICIAL):**

```
# LIFECYCLE STATUS
# --------------------------------------------------------
# stage:             tested
# stage_label:       Tested & Approved
# stage_since:       2026-04-17
# deprecated:        false
# ============================================================
```

**For DEPRECATED recipes:**

```
# LIFECYCLE STATUS
# --------------------------------------------------------
# stage:             deprecated
# stage_label:       Deprecated
# stage_since:       2026-06-01
# deprecated:        true
# deprecation_date:  2026-06-01
# replacement_id:    RCP-CWK-120
# replacement_url:   https://craftframework.ai/rcp-cwk-120/
# deprecation_reason: Merged into RCP-CWK-120 with RCP-CWK-102 and RCP-CWK-103
#                    for comprehensive competitive analysis workflow.
# ============================================================
```

Followed immediately (before section 3.1 below) by a human-readable banner, in plain text:

```

   ╔══════════════════════════════════════════════════════╗
   ║  THIS RECIPE HAS BEEN REPLACED                       ║
   ║                                                      ║
   ║  As of 2026-06-01, this recipe has been merged       ║
   ║  into RCP-CWK-120.                                   ║
   ║                                                      ║
   ║  → Use RCP-CWK-120 instead                           ║
   ║    https://craftframework.ai/rcp-cwk-120/            ║
   ║                                                      ║
   ║  Your existing work with this recipe remains valid.  ║
   ║  This file is kept for reference and continuity.     ║
   ╚══════════════════════════════════════════════════════╝

```

For active recipes, no banner is drawn — the file proceeds directly to section 3.1 after the lifecycle block.

---

## 3. Section order and structure

Recipe content sections follow the live webpage order, top to bottom. Every section uses the same header style for parsing consistency:

```
# ============================================================
# SECTION N: <SECTION TITLE IN UPPERCASE>
# ============================================================
```

The `N` is the webpage-order number (1 through 9). Skipped sections (see 3.4) retain their number so downstream sections stay aligned.

### 3.1 Section catalog

| # | Section | Source on page | Required? |
|---|---|---|---|
| 1 | INTRO — Introduction | L1 (left column) | Yes |
| 2 | RECIPE HEADER — title, description, metadata badges | L2 (left column) | Yes |
| 3 | TL;DR — summary, step outline, differentiator, best-for, time, difficulty | L3 (left column) | Yes |
| 4 | HOW TO START — numbered step list (no checkboxes per Q-T1) | L4 (left column) | Conditional (see 3.4) |
| 5 | HOW AI READS THIS RECIPE — behavioral prose | L5 (left column) | Yes |
| 6 | WHEN TO USE THIS RECIPE — triggers, anti-patterns, comparisons | L6 (left column) | Yes |
| 7 | RECIPE FAQ — Q&A pairs, variable count | L7 (left column) | Yes |
| 8 | RECIPE CODE — full copy-paste-ready CRAFT recipe | WPRM Notes (right column) | Yes |
| 9 | AI-TO-AI — machine-readable metadata and execution guidance | Bottom accordion | Yes |

The webpage is a two-column plus accordion layout; the `.txt` flattens it by presenting the left column (sections 1–7) first, then the right column (section 8), then the accordion (section 9). This preserves the "human-facing prose first, machine-facing JSON last" reading flow.

### 3.2 Section content rules

- Section titles in the `.txt` are always uppercase.
- Section bodies use natural paragraph text, numbered lists, or key-value lines as appropriate for the content. No markdown syntax is required; if used, standard conventions apply (`#` for subheaders, `-` for bullets, `**` for emphasis) but must not confuse plain-text readers.
- No HTML tags. Recipe content that uses HTML on the webpage is rendered to plain text in the `.txt`.
- URLs are written in full (`https://...`), not as markdown links, so they remain clickable in any text viewer.
- Code blocks (section 8 recipe code) may contain any characters; they are copied verbatim from the WPRM Notes field.

### 3.3 Section dividers

Between any two sections, insert one blank line, then the section header (with its 3-line divider), then one blank line, then the section body.

### 3.4 Conditional section 4 — HOW TO START

Section 4 ("How To Start") is conditional pending Q-T11 (deferred SP07 Step 2 decision: does L4 survive as a plain numbered list, or collapse into section 3's TL;DR step summary?). Two valid states:

- **If section 4 survives:** render it normally with header, numbered step list, and divider.
- **If section 4 collapses into section 3:** the `.txt` skips the header entirely. The TL;DR in section 3 carries the expanded step content. Section 5 follows section 3 directly (with a blank-line gap but no "section 4 omitted" marker).

Number alignment is maintained: section 5 is always numbered `SECTION 5:` regardless of whether section 4 exists.

### 3.5 Section 9 — AI-TO-AI

The final section is a JSON block for machine consumption. It MUST contain:

- `lifecycle` object (per SPEC-RECIPE-LIFECYCLE §7 schema) — duplicates and extends the top-of-file lifecycle status
- `execution` object (parameters, tone calibration, failure modes, common mistakes)
- `recipe_meta` object (difficulty, time, requirements, combo stage)
- `edge_cases` array

Exact JSON schema is deferred to SP07 Phase 1 Step 4 (JSON schema design). Until that schema is finalized, section 9 may include a provisional JSON block whose structure is updated retroactively when the schema lands.

JSON block format:

```
# ============================================================
# SECTION 9: AI-TO-AI
# ============================================================

{
  "lifecycle": { ... },
  "execution": { ... },
  "recipe_meta": { ... },
  "edge_cases": [ ... ]
}

# ============================================================
# END OF FILE
# ============================================================
```

The JSON block is valid JSON (parseable by any standard parser). No trailing commas. No inline comments inside the JSON itself. The surrounding `#`-line dividers are outside the JSON.

### 3.6 End-of-file marker

Every file ends with:

```
# ============================================================
# END OF FILE
# ============================================================
```

Followed by exactly one trailing newline.

---

## 4. Example skeleton

A complete (but contentless) file follows this skeleton:

```
# ===========================================================
# CRAFT Framework Cookbook - Proprietary Content
# ===========================================================
# SPDX-License-Identifier: LicenseRef-CRAFT-Proprietary
# (C) 2025-2026 Ketelsen Digital Solutions LLC.
# All Rights Reserved.
# CRAFTFramework.ai - Licensed via membership.
# Terms: craftframework.ai/terms
# ===========================================================

# FILE METADATA
# --------------------------------------------------------
# recipe_id:         RCP-XXX-XXX-XXX
# slug:              EXAMPLE-SLUG
# recipe_title:      Example Recipe Title
# cookbook:          CAT-CWK COWORK
# canonical_url:     https://craftframework.ai/.../
# download_url:      https://raw.githubusercontent.com/.../
# library_entered:   YYYY-MM-DD
# last_updated:      YYYY-MM-DD
# file_format_ver:   1.0
# ============================================================

# LIFECYCLE STATUS
# --------------------------------------------------------
# stage:             experimental
# stage_label:       Experimental
# stage_since:       YYYY-MM-DD
# deprecated:        false
# ============================================================

# ============================================================
# SECTION 1: INTRO
# ============================================================

<intro paragraph(s)>

# ============================================================
# SECTION 2: RECIPE HEADER
# ============================================================

<title, description, metadata badges>

# ============================================================
# SECTION 3: TL;DR
# ============================================================

<summary, step outline, differentiator, best-for, time, difficulty>

# ============================================================
# SECTION 4: HOW TO START
# ============================================================

<numbered steps — omit entire section if Q-T11 collapses it into section 3>

# ============================================================
# SECTION 5: HOW AI READS THIS RECIPE
# ============================================================

<behavioral prose>

# ============================================================
# SECTION 6: WHEN TO USE THIS RECIPE
# ============================================================

<triggers, anti-patterns, comparisons>

# ============================================================
# SECTION 7: RECIPE FAQ
# ============================================================

<Q&A pairs, variable count>

# ============================================================
# SECTION 8: RECIPE CODE
# ============================================================

<full CRAFT recipe from WPRM Notes>

# ============================================================
# SECTION 9: AI-TO-AI
# ============================================================

{
  "lifecycle": { ... },
  "execution": { ... },
  "recipe_meta": { ... },
  "edge_cases": [ ... ]
}

# ============================================================
# END OF FILE
# ============================================================
```

---

## 5. Versioning

- `file_format_ver` in the metadata block records which version of this spec a file was authored against.
- Backward-compatible format changes (added optional fields, clarified rules) increment the minor version: 1.0 → 1.1.
- Breaking changes (renamed fields, reordered sections, removed sections) increment the major version: 1.x → 2.0. A major-version change requires a PERMANENCE-POLICY amendment because it affects how downstream consumers parse every file.

The current specification version is shown at the top of this document and in every file's metadata.

---

## 6. What this spec does not cover

- **Recipe content quality, voice, or style.** Governed by SP02 positioning anchor and SP03 editorial framework in the CRAFT project, not here.
- **JSON schema for the AI-to-AI section.** Deferred to SP07 Phase 1 Step 4. When that schema lands, section 3.5 above is updated with a concrete reference and the format version increments.
- **The sync workflow** — how `.txt` files are generated from live recipe pages and kept in sync. Governed by SP08 Phase 2 (SPEC-RECIPE-TXT-SYNC once written).
- **The recipe lifecycle itself** — stage definitions, transition rules, deprecation semantics. Governed by SPEC-RECIPE-LIFECYCLE in the CRAFT project.

---

## 7. Open items

- `Q-SP08-5` (new): Reserve a `checksum` field in metadata? Would enable integrity verification after download. Not in v1.0. Revisit if tampering becomes a concern.
- `Q-T11` (inherited from SP07): Does section 4 survive or collapse into section 3? Design decision, not spec decision. Spec handles both cases (see 3.4).
- `SP07 Phase 1 Step 4`: AI-to-AI JSON schema. When this lands, update section 3.5 reference and increment to 1.1 or 2.0 depending on compatibility.

---

*This specification is authored as part of SP08 Phase 1 (P067-H019). Changes follow the amendment process in `PERMANENCE-POLICY.md`.*
