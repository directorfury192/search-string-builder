# Adding a Database

Search String Builder reads one **profile file** per database from its `references/` folder. Any file whose name starts with `DB_` counts as a supported database, so adding a database means adding one file. The instructions in `SKILL.md` don't need to change.

A profile answers what the plugin needs to know to build a correct string:

- which field tags to use (title, abstract, keywords)
- how operators, phrases, exact match and wildcards work
- how dates are written
- how to add subject filters
- examples of strings that actually work

## Option A: let the plugin interview you (easiest)

1. In ChatGPT, select the plugin and type: `Add a new database profile for IEEE Xplore` (or your database).
2. Keep the database's official help pages open, such as "Search tips," "Advanced search" and "Field codes." Paste what they say as the plugin asks for each section, or let it look things up and cite the page.
3. Give it at least **two strings you've tested** in the real database.
4. It hands back a file such as `DB_IEEE_Xplore.md`.

## Option B: fill in the template

1. Copy [`DB_TEMPLATE_New_Database.md`](../plugin/search-string-builder/skills/search-string-builder/assets/DB_TEMPLATE_New_Database.md).
2. Rename it `DB_<DatabaseName>.md`.
3. Replace everything in [square brackets] with facts and source links from the official help pages.
4. Add at least two tested example strings, using straight quotes only.

## Using the new profile

- **Just for yourself, right away:** attach the `DB_` file at the start of any chat with the plugin. It will use the file for that conversation.
- **For everyone:** contribute it to this repository (below).

## Contributing a profile to this repository

1. Open an [issue](../../../issues) titled "New database profile: <name>" and attach the file, or
2. Fork the repo, add the file to `plugin/search-string-builder/skills/search-string-builder/references/`, and open a pull request.

Please include:
- the official help-page links you used
- at least two example strings you ran successfully, with the date you ran them

Contributions are published under the same CC BY-NC 4.0 license as the rest of the project.

## Tips for a good profile

- **Examples matter most.** The plugin copies the structure of your examples closely.
- **Write down surprises** under "Pitfalls," for example "wildcards turn off spelling variants" or "category names must be quoted."
- **Keep it focused.** One database per file.
