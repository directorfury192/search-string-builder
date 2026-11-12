# DB_EBSCO_Academic_Search_Complete - Database Profile

Database: Academic Search Complete on the EBSCOhost platform (the same syntax works in most EBSCOhost databases, e.g. Academic Search Premier, Applied Science & Technology Source, and EBSCO Discovery Service).
Where to paste: Advanced Search > first search box, with the field drop-down left at "Select a field (optional)" and the search mode set to "Proximity" in the new EBSCO interface (its default; it honors explicit AND/OR/NOT) or "Boolean/Phrase" in classic EBSCOhost.
Sources: https://connect.ebsco.com/s/article/Applying-Search-Modes-in-EBSCOhost-and-EBSCO-Discovery-Service-in-the-New-EBSCO-User-Interfaces?language=en_US ; https://connect.ebsco.com/s/article/Searching-with-Wildcards-in-EDS-and-EBSCOhost?language=en_US ; https://connect.ebsco.com/s/article/How-can-I-search-for-content-by-date-using-the-DT-field-code?language=en_US ; https://connect.ebsco.com/s/article/Browsing-Subjects-in-the-New-EBSCO-Interfaces?language=en_US

## Default search fields
For EACH concept, search title+abstract (XB), author keywords (KW) and, if supplied, that concept's subject headings (DE), joined with OR:
```
( XB ( kw1 OR "kw phrase 2" ) OR KW ( kw1 OR "kw phrase 2" ) OR DE ( "SUBJECT heading 1" OR "SUBJECT heading 2" ) )
```
Then join the concept groups with AND. This means a concept can be matched in the title/abstract, in the author keywords, or by subject heading.
- If XB returns an error in the user's interface, replace `XB ( ... )` with `TI ( ... ) OR AB ( ... )`.
- Broader option (offer when results are too few): drop the field codes and search the default fields (authors, subjects, keywords, titles, abstracts): `( kw1 OR kw2 OR DE "SUBJECT 1" )`.
- Narrower option: TI only.

## Field codes
| Code | Field | Notes / example |
|---|---|---|
| TI | Title | TI "fatigue crack" |
| AB | Abstract | AB ("civil liberties") |
| XB | Title and abstract | XB therapy |
| KW | Author-supplied keywords | KW wages |
| DE | Subject terms (exact, phrase-indexed) | DE "Buckling (Mechanics)" |
| SU | Subject (word-indexed, broader than DE) | SU MOTION pictures |
| SH | Controlled subject headings from the thesaurus (exact) | SH "MOTION picture industry" |
| MH | Subjects, keyword search incl. geographic terms | MH Polynomials |
| TX | All text, including full text | TX cronyism (very broad) |
| LA | Language | LA english |
| RV | Peer reviewed (Y/N) | RV Y |
| DT | Date of publication | DT 20040101-20241231 |
DE is the default for subject headings. Use SU when the user wants a looser, word-level subject match; use SH/MH only if the user's database lists them.

## Default limiters (always add unless the user says otherwise)
`AND RV Y AND LA english` (peer-reviewed, English).

## Dates (DT)
- Range: convert years to Jan 1 of the start year through Dec 31 of the end year in YYYYMMDD: 2004-2024 becomes `DT 20040101-20241231`.
- Single year: `DT 2001`. Specific date: `DT 19690721`.
- Relative: 1-3 digit numbers mean "last N days": `DT 30` (last month), `DT 365` (last year).

## Operators
AND, OR, NOT. Use parentheses around every OR list and every concept group so the grouping is never ambiguous. Put all exclusions in one NOT block at the end.

## Phrases and exact match
Double quotes search the exact phrase. When the user wants a single word searched exactly, put it in quotes and do not truncate it. Note: a wildcard inside quotes still expands.

## Wildcards and truncation
- `*` = any number of characters (best with at least 3 leading letters): `comput*` finds computer, computing, computation. Inside a word: `hea*one`. Between words, `*` = any one word: `midsummer * dream`.
- `#` = one OPTIONAL character - ideal for US/UK spellings: `colo#r` (color/colour), `p#ediatric` (pediatric/paediatric), `model#ing` (modeling/modelling).
- `?` = exactly one character: `ne?t` (neat, nest, next). A `?` at the END of a word is ignored; to use it there write `#?` (`Monday#?` finds Mondays).
- Combine: `colo#r*`, `p#ediatric*`.
- Restrictions: no wildcard as the first character; if only one letter precedes a wildcard there must be another literal letter within the first four characters (`f#r*` ok, `f??*` not ok).
- Using a wildcard or truncation switches off plurals/possessives and synonym expansion for that term (`pediatric*` will NOT find paediatric; `colo#r` will not find colors). Truncation can still trigger "Apply equivalent subjects" if that option is on.
- `*` expands to a maximum of 2,000 terms.
- Wildcards do not work with Chinese, Japanese or Korean.

## Search modes
Use Proximity mode in the new EBSCO interface (default; explicit Boolean operators are honored) or Boolean/Phrase in classic EBSCOhost. Do NOT use Find all my search terms (implicit AND), Find any of my search terms (implicit OR), SmartText (paste a paragraph) or Natural Language with a built string - they reinterpret the query.

## Subject filter step (EBSCO Subjects)
Ask the user to find subject headings for EACH concept: in Academic Search Complete, open Advanced Search > "Subjects" (Subject Terms/Thesaurus), search each keyword, and note the matching subject terms; clicking a term shows broader and narrower terms to consider. Collect subject terms concept by concept so they go inside the right concept group. Ask how they should be combined (normally OR within the concept). Use the exact wording and capitalization the user copies. Never invent headings.

### Non-STEM topics (social sciences, humanities, religion, health)
Academic Search Complete is multidisciplinary, so the subject step works the same way for non-STEM topics: the user looks up each keyword under **Subjects** and copies the exact heading. Unlike Scopus and Web of Science, EBSCO has no short code list of subject areas, so never supply subject headings from memory - EBSCO's wording is specific (inverted forms and a capitalized first word, like "ACRYLONITRILE butadiene styrene resins" in Example 1), and a heading that doesn't exist silently returns nothing. If the user can't find a heading, build the concept from keywords only.

Tips to share with the user when finding non-STEM headings:
- Search the Subjects list with the plainest form of the word (e.g., "pastoral" rather than "pastoral care practices") and look at the broader and narrower terms offered.
- Religion and ministry topics often sit under headings that start with "CHURCH", "CLERGY", "PASTORAL", "SPIRITUAL" or the denomination name.
- Social care topics are often indexed under headings for the population served rather than the practice. Ask the user to check both.
- Geographic places are subject terms too (searched with MH, which includes geographic subject terms).

**Related EBSCOhost databases for non-STEM topics.** If the user's institution has them, the same string syntax works across EBSCOhost, and they can select several databases at once (Choose Databases). Subject vocabularies and field codes differ between databases, so subject headings must be looked up in each database's own thesaurus. Most use DE for subject headings, but CINAHL uses MH, so check the database's Field Codes help page before relying on a subject field code. Common ones:
- Religion: ATLA Religion Database
- Sociology and social work: SocINDEX; Social Work Abstracts
- Psychology and counseling: APA PsycInfo
- Nursing and allied health: CINAHL
- Education: ERIC; Education Source
- Humanities: Humanities Source
- Business: Business Source
Recommend checking with the library which of these are available. When several databases are searched together, leave out DE subject terms (each database has its own) or use SU for a looser word-level subject match.

## Exclusions
One block at the end: `NOT ( term1 OR "phrase two" )`, or field-specific: `NOT XB ( term1 OR term2 )`.

## Worked examples (straight quotes, ready to paste)

Example 1 - subjects, no exclusions
```
( XB ( ABS OR "FD-ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" ) OR KW ( ABS OR "FD-ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" ) OR DE ( "ACRYLONITRILE butadiene styrene resins" ) ) AND ( XB ( "composite mechanics" OR "constitutive model*" OR "FEA simulation" OR "finite element analysis" OR "model accuracy" OR "local controlled propert*" ) OR KW ( "composite mechanics" OR "constitutive model*" OR "FEA simulation" OR "finite element analysis" OR "model accuracy" OR "local controlled propert*" ) OR DE ( "COMPUTER simulation" OR "SIMULATION methods & models" OR "FINITE element method" ) ) AND ( XB ( FDM OR "fused deposition model#ing" OR "fused filament fabrication" OR "additive manufacturing" OR "3D print*" OR FFF ) OR KW ( FDM OR "fused deposition model#ing" OR "fused filament fabrication" OR "additive manufacturing" OR "3D print*" OR FFF ) OR DE ( "THREE-dimensional printing" OR "FUSED deposition modeling" OR "RAPID prototyping" ) ) AND ( XB ( tensile OR flexural OR fatigue OR compression OR "mechanical propert*" ) OR KW ( tensile OR flexural OR fatigue OR compression OR "mechanical propert*" ) OR DE ( "TENSILE strength" OR "MECHANICAL behavior of materials" ) ) AND RV Y AND LA english AND DT 19990101-20251231
```

Example 2 - subjects and exclusions
```
( XB ( ABS OR "FD-ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" ) OR KW ( ABS OR "FD-ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" ) OR DE ( "ACRYLONITRILE butadiene styrene resins" ) ) AND ( XB ( "finite element analysis" OR "FEA simulation" OR "constitutive model*" ) OR KW ( "finite element analysis" OR "FEA simulation" OR "constitutive model*" ) OR DE ( "FINITE element method" ) ) AND ( XB ( FDM OR "fused filament fabrication" OR "3D print*" ) OR KW ( FDM OR "fused filament fabrication" OR "3D print*" ) OR DE ( "THREE-dimensional printing" ) ) AND RV Y AND LA english AND DT 20000101-20251231 NOT ( "carbon fiber" OR honeycomb OR kevlar OR DE "FIBROUS composites" )
```

Example 3 - no subjects, no exclusions, default fields (broad option)
```
( female OR woman* OR non-binary ) AND ( Black OR African OR Caribbean OR Afro-Caribbean* OR Afro-Latina* OR "African American*" ) AND ( science OR technology OR engineering OR mathematics OR STEM ) AND ( doctoral* OR postdoctoral OR post-doc* OR doctorate-holding OR PhD OR postgraduate ) AND ( attrition OR retention ) AND RV Y AND LA english AND DT 20040101-20241231
```

Example 4 - non-STEM (religion / social care), keywords only (no subject headings looked up yet)
```
( XB ( congregation* OR church* ) OR KW ( congregation* OR church* ) ) AND ( XB ( "pastoral care" OR "spiritual care" ) OR KW ( "pastoral care" OR "spiritual care" ) ) AND ( XB ( "trauma-informed" ) OR KW ( "trauma-informed" ) ) AND RV Y AND LA english AND DT 20150101-20261231
```
(Once the user has looked up subject headings, add each concept's headings inside its group as `OR DE ( "HEADING 1" OR "HEADING 2" )`, as in Examples 1-2.)

## Pitfalls to avoid
- Curly quotes break the search - straight quotes only.
- Applying a field code to only the first concept group (the others then fall back to default fields).
- NOT placed inside an OR list (`a OR b NOT c`) - put exclusions in one block at the end.
- Running the string in SmartText, Natural Language, Find all or Find any mode.
