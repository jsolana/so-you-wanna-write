# So You Wanna Write

A small set of AI agents that help you write, edit, translate, typeset, illustrate and publish a book. It works for **novels** and for **technical or non-fiction books**.

The agents are plain Markdown, independent of any LLM provider. Each agent is one file in `.claude/agents/`, which Claude Code loads automatically as a subagent. In any other assistant, paste the agent's file (the header is harmless) plus `resources/standards.md`.

**Principles:** the author decides everything; agents give honest feedback and never overwrite your work or your Book Context without approval; Spanish is the default language (English supported, overrides on request); agents work alone and only delegate through explicit requests.

## Agents

| Agent | Use it to |
|---|---|
| `story-architect` | **Fiction.** Design plot, characters and world; check continuity; keep the Book Bible. |
| `technical-architect` | **Technical / non-fiction.** Design structure and learning path; check terminology, concept order and code consistency; keep the knowledge base. |
| `editor` | Review chapters honestly: clarity, structure, language. Adapts to the book type. Can ask the architect for deeper analysis. |
| `beta-reader` | See how a simulated reader (or learner) experiences the text. |
| `researcher` | Get sourced research, with confidence levels. |
| `translator` | Translate preserving voice, terminology and decisions. |
| `formatter` | Typeset in LaTeX and produce a validated PDF with a publishing profile. |
| `illustrator` | Get cover concepts, English image prompts and cover specs. |
| `publisher` | Prepare descriptions, metadata and a publication package. It never publishes anything itself. |


## Quick start

1. Create `books/my-book/` with a `book.yaml` and a `manuscript/` folder (copy `books/sample/` if you want a model):

   ```yaml
   title: My Book
   type: fiction        # or: technical
   language: es         # manuscript language
   genre: ...
   audience: ...
   synopsis: ...
   ```

2. Ask for work by naming the agent and the book:
   - Claude Code: `Use the editor agent to review chapter 1 of books/my-book, depth full`
   - Other assistants: paste the agent's file + the standards file, add the manuscript and the relevant Book Context files, then state the task.
3. Review the result. Agents propose changes to the Book Context (*Context Update Proposals*); nothing is saved until you approve.

## How to write a good book with the agents

**Novel**

1. **Design.** `story-architect` helps you explore the concept, conflict, structure, characters and world. You choose among options. Approved decisions go into `bible/`, `structure.md` and `voice.md`.
2. **Research** (optional). `researcher` for real-world details.
3. **Write, then check.** After each chapter or batch, run `story-architect` in `continuity` mode, then update the Book Bible with what you approve.
4. **Revise.** `editor` reviews chapters (`proofread`, `line`, `developmental` or `full`). For deeper structural or continuity questions the editor ends with a *Delegation to story-architect* request. The architect returns evidence-based findings and the editor writes the final report.
5. **Reader test** (optional). `beta-reader` with a profile of your target readers.

**Technical or non-fiction book** (`type: technical`)

1. **Design.** `technical-architect` in `design` mode: define the target reader, prerequisites and objectives, choose a structure (tutorial, reference, cookbook, project-based), and outline chapters with their objectives. Results go into `bible/` (the knowledge base).
2. **Verify facts** (optional). `researcher` checks claims, versions and standards against official documentation.
3. **Write, then check.** After each chapter, `technical-architect` in `consistency` or `learning-path` mode: terminology, concepts used before introduced, code consistent with the text.
4. **Revise.** `editor` evaluates clarity, accuracy, progression and examples, and delegates to `technical-architect` when needed.
5. **Reader test** (optional). `beta-reader` as a learner at your target level.

**Production (both)**

1. `editor` does a final review; you approve the final text.
2. `translator` (optional) produces the target-language edition in `translations/<lang>/`.
3. `formatter` builds the PDF from a profile (`resources/formatter/profiles.yaml`) and writes a validation report. It gives you the final page count.
4. `illustrator` prepares cover concepts, prompts and specs. Spine width needs the final page count. Generated art still has to be assembled into a print-ready cover.
5. `publisher` reviews readiness and prepares description, metadata and the package. You publish manually on the platform. Automated publication is not implemented.

If the text changes after formatting, rerun the formatter and recalculate the spine.

## Delegation in Claude Code

Subagents cannot start other subagents. When the editor ends with a delegation request, ask Claude to run the architect with that request and then hand the findings back to the editor.

## Repository layout

```text
.claude/agents/<agent>.md    The agents: one file each (Claude Code subagent header + full definition)
resources/                      Shared resources
  standards.md               Rules shared by all agents
  book-context.md            Book Context structure, ownership and fields
  templates.md               Editorial report, Book Bible, knowledge base, validation, publication package
  formatter/                 profiles.yaml (publishing profiles) and book.tex (LaTeX base)
books/<book-name>/           One isolated Book Context per book (you create these)
books/sample/                Example book (Spanish) with a sample editor report
```

Book Context structure and who maintains each file: `resources/book-context.md`.

## Notes

- Publishing profiles ship without numbers. The formatter and illustrator read current official platform documentation and record source and date.
- Never put passwords, tokens or API keys in a book folder or in a prompt.
- To add or change an agent: edit `.claude/agents/<agent>.md`, keep the 12-section structure, and put shared rules in `resources/standards.md`. Keep only agent files in `.claude/agents/`.
