# User Guide

This guide is for researchers using Search String Builder in ChatGPT. You don't need to know any database syntax.

## 1. Start the plugin

1. In ChatGPT, open a **new chat**.
2. Type `@Search String Builder` and pick the entry listed under **Plugins**.
   - If you also see a file with a similar name under **Files**, don't pick it. Files are old uploads, not the plugin.
3. Check that the plugin chip appears in your message, then type your request.

You can also click **Plugins** below the message box and choose it there.

## 2. Answer the interview

The plugin asks one question at a time. Answer each one before it moves on.

| Step | What it asks | Tips |
| --- | --- | --- |
| Database(s) | Scopus, Web of Science, EBSCO, or several | Choosing several saves time: you enter your keywords only once. |
| Number of concepts | A whole number | 3–5 is recommended. Fewer can be too broad; more can be too narrow. If you're unsure, ask a subject librarian. |
| Keywords per concept | A list for each concept | Paste a list, use SHIFT+ENTER for new lines, or separate items with commas or semicolons. Include synonyms and related terms. |
| Exact match | Single words that must not be expanded | Say "none" if you're unsure. Phrases are always searched as phrases. |
| Subject filters | Database-specific | Optional. For EBSCO, look up headings in the database's **Subjects** list and copy them exactly. |
| Years | A range | For example, 2015–2026. |
| Exclusions | Words to leave out | Optional. Exclusions can remove relevant papers, so add them after you've tested the search. |

## 3. Use the string

Every answer includes:

- **The string** in a copy-ready block
- **Where to paste it** in that database
- **Why it's built this way:** a short, plain-language explanation
- **Tips** if you get too many or too few results

### Where to paste

| Database | Where | Settings |
| --- | --- | --- |
| Scopus | Advanced document search > query box | — |
| Web of Science | Advanced Search > Query Preview box | Database set to Web of Science Core Collection |
| EBSCO | Advanced Search > first search box | Field drop-down on "Select a field (optional)". Search mode: **Proximity** (new interface) or **Boolean/Phrase** (classic). |

## 4. Other things you can do

- **Translate a string:** "Translate this Scopus string to Web of Science:" followed by the string. The plugin lists what it found and asks you to confirm before rebuilding.
- **Add a database:** "Add a new database profile for IEEE Xplore." See [ADDING_A_DATABASE.md](ADDING_A_DATABASE.md).
- **Ask why:** "Why did you use braces here?" The plugin explains its choices.

## 5. Good habits

- **Always run the string** in the database. The plugin can't see results.
- **Save your final strings** with the date you ran them, which systematic reviews need for reporting.
- **Check your concepts with a librarian** for any formal review.

## Troubleshooting

| Problem | What to do |
| --- | --- |
| The plugin answers with an old version or mentions a ZIP file | You picked a file instead of the plugin. Start a new chat and pick the entry under **Plugins**. Delete old ZIPs from your ChatGPT Library. |
| The database shows a syntax error | Paste the error into the chat and ask the plugin to fix the string. |
| Too many results | Ask for title-only searching, add a subject filter, narrow the years, or remove broad wildcard terms. |
| Too few results | Ask for broader fields, remove the subject filter, or add synonyms to each concept. |
