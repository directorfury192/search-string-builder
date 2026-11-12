# How It Works

## Structure

Search String Builder is a **skills-only plugin**. It has no server and no connection to outside services. It is a set of text files that ChatGPT reads when your request matches the plugin's description.

| File | Role |
| --- | --- |
| `SKILL.md` | The instructions: the interview rules, output format, quality checks and boundaries. Its `description` line tells ChatGPT when to use the plugin. |
| `references/00_Shared_Workflow.md` | The step-by-step interview shared by all databases, with sources for the 3–5 concept guidance. |
| `references/DB_*.md` | One profile per database: field tags, operators, phrase and exact-match rules, wildcards, dates, subject filters, worked examples and pitfalls. |
| `assets/DB_TEMPLATE_New_Database.md` | A blank profile used when adding a database. |

The plugin reads the relevant `DB_` profile before building, checking or translating a string. The rules in a profile override the model's general knowledge, which keeps strings consistent with each vendor's documentation.

## Design principles

- **One question at a time.** Researchers aren't asked for everything at once.
- **No suggested concepts.** Choosing research concepts is part of the research. The plugin refers users to a subject librarian instead.
- **No made-up subject headings.** Subject terms come from the user, or from the fixed code lists in the profiles (Scopus Subject Areas, Web of Science Categories and Research Areas).
- **Silent quality checks.** Before showing a string, the plugin checks for balanced parentheses, field tags on every concept, straight quotes, exclusions placed at the end, and operator limits.
- **Explain everything.** Every string comes with a plain-language explanation.

## Syntax decisions

These corrections were made while converting the original prompts. They are recorded here so contributors understand why the profiles read the way they do.

| Database | Decision | Why |
| --- | --- | --- |
| All | Straight quotes only | Curly quotes are treated as ordinary characters and break phrase searching. |
| All | `propert*`, not `property*` | `property*` does not match "properties." |
| Scopus | Exact match uses `{braces}` | Quotes in Scopus are a *loose* phrase that still matches plurals and variants. |
| Scopus | `TITLE-ABS-KEY` on every concept | A concept group without a field tag searches all fields. |
| Scopus | Precedence is OR, then AND, then AND NOT | Unbracketed mixes such as `career AND choice OR ...` are read differently than they look. |
| Scopus | `AND NOT` goes at the end, as one block | Following Elsevier's guidance. |
| EBSCO | Each concept is `( XB(...) OR KW(...) OR DE(...) )`, joined with AND | Lets each concept match in the title/abstract, the author keywords, or the subject headings. Tested in Academic Search Complete. |
| EBSCO | Proximity or Boolean/Phrase search mode | SmartText and Natural Language modes reinterpret the string. |
| Web of Science | `TS=` alone, not `TI= OR AB= OR TS=` | Topic already covers title, abstract and keywords. Repeating it wastes operators against the 49-operator limit. |
| Web of Science | Categories under `WC=`, Research Areas under `SU=` | They are separate schemes with separate field tags. |
| Web of Science | "Social Sciences Other Topics," with no hyphen | It must match Clarivate's exact name. |

## Testing

Version 1.0.0 was tested in all three databases with a religion and social care topic. Scopus, Web of Science Core Collection and EBSCO Academic Search Complete each accepted the generated strings and returned results.

## Origin

The plugin began as three separate custom-GPT prompts by Arielle Miller, one each for Scopus, EBSCO and Web of Science. When OpenAI retired custom GPTs in favor of plugins in 2026, the prompts were combined into one skill, with a shared interview and one profile per database.
