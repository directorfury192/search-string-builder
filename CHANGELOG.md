# Changelog

## 1.0.0 (November 2026)

First public release.

- Builds advanced search strings for Scopus, Web of Science Core Collection and EBSCO Academic Search Complete through a step-by-step interview.
- Builds one search for several databases at once, collecting your keywords only once.
- Translates existing search strings between databases.
- Handles each database's syntax for you: field tags, wildcards, exact match, US/UK spellings, date formats and operator limits.
- Includes subject filters for the sciences, engineering, social sciences, humanities, health and religion: all 27 Scopus subject areas, plus Web of Science Research Areas and Categories.
- Explains every string in plain language, with tips for too many or too few results.
- Can be extended with new database profiles built from official help pages.

### History before release

- **0.4.0:** the skill no longer assumes users are in engineering; it now serves any discipline. Public contact email updated.
- **0.3.0:** added social sciences, humanities, health and religion subject lists for all three databases. Fixed Web of Science "Other Topics" names, which have no hyphen.
- **0.2.0:** display name and starter prompts added.
- **0.1.0:** converted from three custom-GPT prompts into a single ChatGPT skill and plugin. Corrected several syntax issues in the original prompts (see [docs/HOW_IT_WORKS.md](docs/HOW_IT_WORKS.md)).
