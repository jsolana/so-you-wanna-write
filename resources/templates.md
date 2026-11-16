# Templates

Copy what you need. Sections: [Editorial report](#editorial-report), [Book Bible (fiction)](#book-bible-fiction), [Knowledge base (technical)](#knowledge-base-technical), [Validation report](#validation-report), [Publication package](#publication-package).


## Editorial report

- **Book:** <title>
- **Scope:** <chapters / passages>
- **Review depth:** proofread | line | developmental | full
- **Date:** <YYYY-MM-DD>

### 1. Overall assessment

### 2. What works well

### 3. Critical issues

```text
[Severity | Type] Location
Problem:
Why it matters:
Reader impact:
Suggestion:
```

### 4. Narrative and structural observations

### 5. Character analysis

### 6. Style and language observations

### 7. Spelling and grammar corrections

| Original | Correction | Reason |
|---|---|---|

### 8. Prioritized recommendations

1. [Severity] ...

---
Severity: Critical | Major | Minor | Optional. Type: Objective error | Potential inconsistency | Strong recommendation | Subjective suggestion.
Findings from `story-architect` (if any) are attributed in the relevant sections.

## Book Bible (fiction)

Copy the files you need into `books/<book-name>/bible/`. Each entry carries a status (`confirmed`, `assumed`, `proposed`) and a source (chapter or "author decision").

### characters.md

```markdown
### <Name>
- Role: 
- Summary: 
- Motivation / goal: 
- Fear / flaw: 
- Arc: 
- Background: 
- Voice (how they speak): 
- Knowledge (what they know, and since when): 
- Facts:
  - [confirmed, ch.1] ...
  - [assumed] ...
```

### relationships.md

```markdown
- <A> ↔ <B>: <nature of relationship>, <how it changes> [status, source]
```

### locations.md

```markdown
### <Place>
- Description: 
- Connected to: 
- Events that happen here: 
- Facts: [status, source]
```

### world-rules.md

```markdown
- <Rule> [status, source] — limits / exceptions:
```

### objects.md

```markdown
### <Object>
- Properties: 
- Owner / location over time: 
- Significance: 
```

### timeline.md

```markdown
| When | Event | Who | Where | Source | Status |
|---|---|---|---|---|---|
```

### glossary.md

```markdown
- <Term / proper name>: <definition or note>. Spelling: <exact form>. [status]
```

### facts.md

```markdown
### Established facts
- [confirmed, ch.3] ...

### Creative decisions
- <date> <decision> — <reason> — approved by author

### Changes to established facts
- <date> <what changed> — <reason> — approved by author
```

### open-questions.md

```markdown
- <Question> — type: unresolved | intentional mystery | unreliable narration | not yet revealed — where raised: 
```

### inconsistencies.md

```markdown
- <Description> — category: actual contradiction | potential inconsistency — evidence: — status: open | resolved (how)
```

## Knowledge base (technical)

Files under `bible/` maintained by `technical-architect`.

### reader.md

```markdown
- Target reader: 
- Prerequisites (what they already know): 
- Goal after reading: 
- Out of scope: 
```

### objectives.md

```markdown
### Part / Chapter <n>
- The reader will be able to: 
```

### concepts.md

```markdown
| Concept | Introduced in | Requires | Status |
|---|---|---|---|
```

### code-examples.md

```markdown
| Listing | Chapter | Language / version | Run? (yes/no, date) | Notes |
|---|---|---|---|---|
```

### tooling.md

```markdown
- <Tool/library>: version <x>, environment <y>. [status, source]
```

### references.md

```markdown
- [1] <Source: title, author/institution, date, link> — used in: 
```

`glossary.md` and `open-questions.md` follow the fiction templates above.

## Validation report

- **Book:** <title>
- **Profile:** <profile id> (source: <URL>, verified: <date>)
- **File:** <PDF path>
- **Engine / command:** <engine and command>
- **Date:** <YYYY-MM-DD>

| # | Check | Result (pass / fail / not checked) | Evidence |
|---|---|---|---|
| 1 | Compiles without errors; warnings reviewed | | |
| 2 | Page dimensions match profile | | `pdfinfo` output |
| 3 | Margins/gutter; no text outside page | | |
| 4 | Missing glyphs / font substitutions | | log, `pdffonts` |
| 5 | Fonts embedded where required | | `pdffonts` |
| 6 | Overfull boxes; incorrect hyphenation | | |
| 7 | Unexpected blank pages | | |
| 8 | Chapter opening pages | | |
| 9 | Page numbering and running headers | | |
| 10 | Widows / orphans / stranded headings | | |
| 11 | TOC entries and page numbers | | |
| 12 | PDF metadata | | |
| 13 | Platform export requirements | | |

### Issues requiring author decision

-

### Readiness statement

<"Technically validated against profile X" only if every applicable check passed. Otherwise: "Not yet publication-ready", with remaining items. Platform acceptance can only be confirmed by the platform's own checker.>

## Publication package

- **Book:** <title>
- **Platform:** <e.g. KDP> | **Docs consulted:** <URL, date>
- **Formats:** <paperback / hardcover / ebook>
- **Language / edition:** <language>

### Assets

| Asset | Path | Status (ready / missing / unverified) | Notes |
|---|---|---|---|
| Final manuscript | | | reviewed and approved by the author |
| Interior file | | | validation report: |
| Cover (front / full wrap) | | | spec checked on: |
| Description | | | |
| Author bio | | | |

### Metadata

- Title / subtitle:
- Author name:
- Categories:
- Keywords:
- ISBN (decision and number):
- Rights and territories:
- Platform declarations (e.g. AI-generated content disclosure, as required by official docs):
- Price (set by the author):

### Open items

-

### Confirmations required from the author

- [ ] Final text approved
- [ ] Price approved
- [ ] Publication request submitted by the author on the platform
