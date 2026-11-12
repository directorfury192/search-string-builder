# DB_TEMPLATE_New_Database - Blank Database Profile

HOW TO USE THIS TEMPLATE
1. Make a copy and rename it DB_<DatabaseName>.md (for example DB_IEEE_Xplore.md or DB_Compendex.md). The name must start with "DB_".
2. Fill in every section below. Copy facts from the database's OFFICIAL help pages (the vendor's "search tips", "advanced search", "field codes" or "search operators" pages) and paste the URL next to each section.
3. Add at least two example strings that you have actually run in the database and that worked.
4. Add the file to the skill's `references/` folder and upload the updated skill (or plugin) as a new version. No change to SKILL.md is needed - the skill looks for any file that starts with "DB_". Quicker option: in a ChatGPT chat, attach the file and ask "Add this file to the references of my search-string-builder skill."
5. Not the owner? Attach the finished DB_ file at the start of any chat that uses the skill; it will be used for that conversation.
Tip: you can also select the Search String Builder plugin (type @Search String Builder and pick it under "Plugins") and say "add a new database" and the skill will interview you section by section and produce this file for you.
Replace everything in [square brackets]. Delete these instructions before uploading if you like.

---

# DB_[Database Name] - Database Profile

Database: [Full name and platform/vendor, e.g. "Compendex on Engineering Village (Elsevier)"]
Where to paste: [Exact place in the interface, e.g. "Expert Search > search box"]
Sources: [URLs of the official help pages you used]

## Default search fields
[Which field tag(s) to wrap around EVERY concept group by default, e.g. title+abstract+keywords. Show the syntax.]
```
[e.g. ( term1 OR "phrase two" ) WN KY]
```
Alternatives to offer: [narrower option, e.g. title only] / [broader option, e.g. all fields]

## Field tags
| Tag | Field | Notes / example |
|---|---|---|
| [ ] | Title | [ ] |
| [ ] | Abstract | [ ] |
| [ ] | Keywords / subject terms | [ ] |
| [ ] | Publication year / date | [ ] |
| [ ] | Language | [ ] |
| [ ] | Document type / peer review | [ ] |

## Operators and order of precedence
Operators: [AND / OR / NOT, or AND NOT? Must they be uppercase?]
Precedence: [Which is processed first? Copy the help page's statement.]
Limits: [Maximum number of operators or terms, if any.]
Where exclusions go: [e.g. one NOT block at the end]

## Phrases and exact match
Phrase syntax: [double quotes? braces?]
Exact single-word match: [how to stop plurals/variants]
Automatic features: [Does it do stemming, lemmatization, US/UK spelling matching automatically? What turns them off?]

## Wildcards and truncation
| Symbol | Meaning | Example |
|---|---|---|
| [*] | [any number of characters] | [comput*] |
| [?] | [ ] | [ ] |
| [ ] | [optional character for US/UK spellings, if any] | [ ] |
Restrictions: [minimum letters before a wildcard, left-hand truncation allowed?, wildcards inside quotes?]

## Dates
[Exact syntax for a year range and a single year, e.g. PY=(2004-2024) or limit to 2004-2024 using the date filter instead of the string.]

## Subject filter step
What to ask the user: [e.g. "Which Compendex controlled terms / classification codes apply to each concept?"]
Where the user finds them: [e.g. "Thesaurus tab > search a keyword > copy the controlled term"]
Syntax: [e.g. {term} WN CV]
Placed: [inside each concept group with OR / as a separate AND block]

## Default limiters
[Anything that should be added to every string unless the user says otherwise, e.g. English language, peer reviewed, journal articles. Write the syntax.]

## Worked examples (tested; straight quotes only)
Example 1 - [describe: e.g. 4 concepts, subject terms, no exclusions]
```
[paste a tested string]
```
Example 2 - [describe: e.g. with exclusions]
```
[paste a tested string]
```

## Pitfalls to avoid
- Curly quotes break the search - straight quotes only.
- [Anything else you learned while testing: errors you hit, fields that behave oddly, etc.]
