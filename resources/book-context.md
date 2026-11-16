# Book Context

Book Context is the knowledge base for one book. Each book lives in its own folder under `books/`. Books never share context.

## Structure

```text
books/<book-name>/
├── book.yaml               # identity, language, genre, audience, synopsis (see resources/book-context.md)
├── voice.md                # narrative voice, POV, tense, style rules, intentional stylistic choices
├── structure.md            # narrative structure, part/chapter outline
├── manuscript/             # chapters: 01-title.md, 02-title.md, ...
├── bible/                  # the Book Bible (owned by story-architect)
│   ├── characters.md       # profiles, motivations, arcs, knowledge
│   ├── relationships.md
│   ├── locations.md
│   ├── world-rules.md      # established narrative rules
│   ├── objects.md
│   ├── timeline.md         # chronology and important events
│   ├── glossary.md         # terminology and proper names
│   ├── facts.md            # established facts + creative decisions
│   ├── open-questions.md   # unresolved questions, intentional mysteries
│   └── inconsistencies.md  # known inconsistencies and their status
├── decisions/
│   ├── editorial.md        # editorial decisions (what the author accepted/rejected)
│   └── translation.md      # translation glossary and decisions, per target language
├── translations/<lang>/    # translated manuscript, one folder per language
├── reports/                # saved agent reports (editorial, beta-reader, research, validation)
├── build/                  # formatter output (PDF, LaTeX), cover specs and prompts
└── publication.yaml        # publication information (platform, ISBN, categories, keywords, status)
```

For `type: technical` books the `bible/` folder is the **knowledge base**, maintained by `technical-architect`: `reader.md`, `objectives.md`, `concepts.md`, `glossary.md`, `code-examples.md`, `tooling.md`, `references.md`, `open-questions.md`. Character, world and timeline files are not used.

Create only what you need. A new book can start with `book.yaml` and `manuscript/`.

## Rules

1. **Isolation.** One folder per book.
2. **Author approval.** Agents propose changes (see Context Update Proposal in `resources/standards.md`). They do not overwrite.
3. **Fact status.** Entries are `confirmed`, `assumed` or `proposed`. Prefer a short line per entry such as `- [confirmed, ch.3] Marta is left-handed.`
4. **History.** Changes to established facts are recorded in `bible/facts.md` or `decisions/editorial.md` with the reason and date, so decisions cannot disappear silently.
5. **No secrets.** Never store credentials or tokens in Book Context.
6. **Plain files.** Markdown and YAML only. Version the book with git if desired.

## Who maintains what

| Area | Maintained by | Read by |
|---|---|---|
| `book.yaml`, `voice.md`, `structure.md` | Author (agents propose) | All |
| `bible/` | `story-architect` (fiction) / `technical-architect` (technical) | All |
| `decisions/editorial.md` | `editor` (records author's decisions) | All |
| `decisions/translation.md`, `translations/` | `translator` | `editor`, `publisher` |
| `reports/` | Agent that produced the report | Author |
| `build/` | `formatter`, `illustrator` | `publisher` |
| `publication.yaml` | `publisher` | `formatter`, `illustrator` |

"Maintained by" means the agent proposes updates and, once approved, can apply them. It does not mean the agent edits freely.

## Reference fields (`book.yaml`, `publication.yaml`)

Not enforced by tooling. Only `title` and `language` are required.

```yaml
book.yaml:
  title: string                 # required
  subtitle: string
  type: fiction | technical      # default fiction. Selects story-architect (fiction) or technical-architect (technical)
  author: string
  language: es                  # required; default manuscript language (ISO 639-1)
  additional_languages: [en]    # planned or existing translations
  genre: string
  subgenres: [string]
  audience: string              # target readers
  synopsis: string
  status: idea | drafting | revising | final | published
  narrative:
    pov: first | second | third-limited | third-omniscient | mixed
    tense: past | present | mixed
  notes: string

publication.yaml:
  platform: kdp                 # extensible: other platforms later
  formats: [paperback, hardcover, ebook]
  isbn:
    paperback: string | null
    hardcover: string | null
    ebook: string | null
  categories: [string]
  keywords: [string]            # platform limits apply; verify in official docs
  description_file: string
  pricing: {}                   # set only with author approval
  page_count: integer | null    # final count, needed for spine width
  paper: string | null          # paper type, needed for spine width
  readiness: not-started | in-progress | ready-for-review | approved
  # Never store credentials, tokens or API keys here.
```
