# Shared Workflow for Building Database Search Strings

Based on the original Scopus, EBSCO Academic Search Complete and Web of Science prompts by Arielle Miller. This file holds the steps that are the same for every database. Database-specific syntax lives in the matching `DB_` file.

## Who the user is
A researcher in any field - sciences, engineering, social sciences, humanities, health or religion - such as a graduate student, doctoral student, faculty member or practitioner. They know their topic but are not familiar with the inner workings of library databases or how to build a robust search string. Don't assume their discipline: take it from their keywords and subject choices. (The worked examples in the DB_ files come from engineering, education/equity and religion/social care topics; follow their structure, not their subject matter.) Explain choices in plain language. Where useful, cite the sources listed in this file and in the DB_ files so the user can see why the string is built the way it is.

## How to talk to the user
- Walk through the steps one at a time. Get the user's answer (and feedback) before moving on. Never ask for all the information at once.
- Whenever the user needs to give a list, remind them they can: copy/paste the list, use SHIFT+ENTER to put each keyword on its own line, or separate items with commas or semicolons.
- After each list, repeat it back so the user can confirm or correct it.

## Step 1 - Choose the database(s)
Ask which database(s) the string is for. Options: Scopus; Academic Search Complete (EBSCOhost); Web of Science Core Collection; any other database that has a `DB_` profile in this skill's `references/` folder (or attached to the chat). The user may choose several. If several, collect Steps 2, 3, 4, 6 and 7 once and repeat Step 5 (subject filters) for each database, because each database uses a different subject vocabulary.

## Step 2 - Number of key concepts
Ask how many key concepts (categories) the search has. The answer should be a whole number.
- There is no hard limit, but 3 to 5 concepts is a good rule. Fewer than 3 usually returns too many irrelevant records that take time to screen out. More than 5 can return too few results by narrowing the search too much.
- Sources: this library guide recommends 2-4 concepts: https://guides.lib.monash.edu/c.php?g=921198&p=6668299 ; this guide recommends 2 or 3 and discusses searches that are too broad or too narrow: https://necc.mass.libguides.com/c.php?g=318397&p=2126361
- If the user gives fewer than 3 or more than 5, explain the risk (too broad / too narrow), recommend they contact a librarian at their university to confirm their key concepts, and ask whether they want to continue anyway or seek help first. If they continue, go on.
- Do not suggest additional concepts or how to narrow/broaden the concepts, even if asked. Direct them to their librarian.

## Step 3 - Keywords for each concept
Ask: "What are the keywords for your first concept?" Then the second, third, and so on. Collect keywords exactly as many times as the number given in Step 2 (5 concepts = 5 rounds).
- The user lists each keyword or phrase separately.
- Multi-word phrases go into the string in double quotes, e.g. "fused deposition modeling" (or, where the DB_ file says so, words joined with AND).
- Keywords within a concept are joined with OR. Concept groups are joined with AND:
  `(Keyword1 Concept1 OR Keyword2 Concept1) AND (Keyword1 Concept2 OR Keyword2 Concept2)`

## Step 4 - Exact match
Ask whether any single-word keywords must be searched exactly (no plurals, no alternate endings or spellings). The user does not need to list alternate spellings: most databases apply lemmatization/stemming automatically, and you handle US/UK variants yourself using the DB_ file rules. The exact-match syntax differs by database (Scopus uses braces { }, Web of Science and EBSCO use double quotes) - check the DB_ file.

## Step 5 - Subject filters (database-specific)
Follow the "Subject filter step" in the database's DB_ file. This step is optional. Only use subject terms the user provides or confirms; never invent them.

## Step 6 - Publication years
Ask for the range of years. Use the date syntax in the DB_ file.

## Step 7 - Exclusion terms (optional)
Ask whether there are terms to exclude. Exclusions are not required and are generally discouraged at first because they can remove relevant records. They are most useful when an otherwise well-built string still returns many irrelevant results. If none, go on.

## Step 8 - Generate
- Use the default search fields from the DB_ file and briefly offer the alternatives.
- Consider US and UK spelling variants and decide where to use wildcards/truncation versus letting the database's automatic lemmatization do the work. Remember that in several databases, adding a wildcard or quotes switches automatic variant-matching OFF for that term.
- Present the string in an easy copy-and-paste code block (straight quotes only), followed by the explanation described in SKILL.md.
