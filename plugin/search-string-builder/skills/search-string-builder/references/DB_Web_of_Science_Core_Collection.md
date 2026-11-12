# DB_Web_of_Science_Core_Collection - Database Profile

Database: Web of Science Core Collection (Clarivate).
Where to paste: Web of Science > Advanced Search > "Query Preview" box (make sure the database selector says Web of Science Core Collection), then click Search.
Sources: https://webofscience.help.clarivate.com/en-us/Content/search-operators.html ; https://webofscience.help.clarivate.com/Content/search-rules.htm ; https://webofscience.help.clarivate.com/en-us/Content/wos-core-collection/woscc-search-field-tags.htm

## Default search fields
Use `TS=( ... )` (Topic) on EVERY concept group. Topic already searches Title, Abstract, Author Keywords and Keywords Plus, so writing `TI=() OR AB=() OR TS=()` repeats the same terms three times, triples the operator count (see the 49-operator limit below) and adds nothing.
Offer the user these alternatives:
- More precise: `(TI=( ... ) OR AB=( ... ))` per concept - title/abstract only, no Keywords Plus (Keywords Plus terms come from the titles of a paper's references and can pull in loosely related papers).
- Most precise: `TI=( ... )`.
- Broadest: `ALL=( ... )` (all fields; right-hand truncation only).

## Field tags
| Tag | Field | Notes |
|---|---|---|
| TS | Topic | Title + Abstract + Author Keywords + Keywords Plus |
| TI | Title | |
| AB | Abstract | |
| AK | Author Keywords | |
| KP | Keywords Plus | Words/phrases that appear frequently in the titles of an article's references but not in its own title |
| ALL | All fields | Funding details not included |
| PY | Year Published | Must be combined with another field using AND or NOT. Includes Early Access year and Final Publication year. Clarivate notes long year ranges can slow processing. |
| WC | Web of Science Categories | e.g. WC=("Engineering, Mechanical") |
| SU | Research Areas | e.g. SU=("Materials Science") |

## Operators and precedence
Order of precedence: NEAR/x, SAME, **NOT, AND, then OR**. Always use parentheses to override precedence and make grouping explicit:
- `influenza OR flu AND avian` finds influenza OR (flu AND avian).
- `(influenza OR flu) AND avian` finds avian together with influenza or flu.
Limit: **a maximum of 49 Boolean operators** in a query. Count them and tell the user the count. If the count is close to or over 49, warn the user and suggest splitting into two searches combined later in Search History (e.g., `#1 AND #2`).

## Lemmatization, stemming and exact match
- Web of Science automatically applies lemmatization (cite finds citing, cites, cited, citation; defense finds defence) and stemming (removes -ing, -es) in Topic and Title searches, and matches US/UK spelling variants (color/colour) automatically.
- **Quotes turn these off**: `"mouse"` finds mouse but not mice; `"color"` finds color but not colour; `"soil drainage"` finds the exact phrase only. Use quotes for exact match requests and for phrases.
- **Wildcards turn lemmatization off** for that term: `color*` finds color, colors, colorful but NOT colour. To get both, use `colo$r*` or `color* OR colour*`.
- If a query exceeds the allowed number of terms, lemmatization is turned off for the whole query and only exact matches are returned.
- Left-hand truncation can turn lemmatization off: `*valves` finds bivalves but not bivalve; `*valve*` finds both.
- Lemmatization/stemming apply only to English search terms.
- Do not ask the user about spelling variants - decide yourself. Reference list of US/UK variants: https://webofscience.zendesk.com/hc/en-us/articles/20016111175441-US-and-UK-Spelling-Variations

## Wildcards
- `*` = zero or more characters: `s*food` (seafood, soyfood).
- `?` = exactly one character: `wom?n` (woman, women); `Barthold?` (Bartholdi, Bartholdy - not Barthold).
- `$` = zero or one character - ideal for US/UK spellings: `flavo$r`, `odo$r`, `model$ing` (modeling, modelling).
- Combine: `organi?ation*` finds organisation(s/al), organization(s/al); `l?chee$` finds lichee, lichees, lychee, lychees.
- At least 3 characters before a right-hand or internal wildcard in Title/Topic (`zeo*` ok, `ze*` not).
- Left-hand truncation (`*oxide`) allowed in Topic, Title and identifying codes only, with at least 3 characters after the wildcard; not allowed in ALL= (right-hand only there), Author or Cited Author.
- No wildcards after special characters (/ @ #) or punctuation, and none in years (`PY=200*` not allowed).
- Avoid very broad truncation (it can return incomplete results).
- Wildcards are valid only with Latin-alphabet languages.

## Hyphens, apostrophes and formulas
- Hyphens and apostrophes are treated as spaces: `TS=hydro-power` finds hydro-power and hydro power; `TS=hydro*power` finds hydropower and hydroelectric power. For hyphenated terms consider both forms.
- Chemical formulas: do not split alphanumeric characters (`KxFe2-ySe2`, not `K x Fe 2-y Se 2`); quotes are fine.

## Dates
`PY=(2004-2024)` for a range; `PY=2007` for one year. PY must be ANDed with other fields.

## Subject filter step (Categories and Research Areas)
Two optional sub-steps, asked one at a time:
1. Web of Science Categories (tag WC). Tell the user they can browse the full list at https://webofscience.help.clarivate.com/en-us/Content/wos-core-collection/wos-core-collection.htm (expand "Subject Categories"). Every journal/book in the Core Collection is assigned at least one category. Category names contain commas - always quote them: `"Engineering, Mechanical"`.
2. Research Areas (tag SU). List: https://webofscience.help.clarivate.com/Content/research-areas.html . Research Areas are a broader scheme shared across all Web of Science databases; some names overlap with categories, but the two schemes are separate.
Combine whatever the user gives into ONE subject block ANDed to the query:
- both: `AND (WC=("Engineering, Mechanical" OR "Materials Science, Multidisciplinary") OR SU=("Engineering" OR "Materials Science"))`
- only one: `AND WC=( ... )` or `AND SU=( ... )`
### Non-STEM and health names (exact spelling matters)
Names must match Clarivate's list exactly, including "&" and commas. Show the user the names you plan to use and let them confirm before you generate the string. If they're unsure, point them to the official lists linked above. Research Areas (SU) are broad; Web of Science Categories (WC) are narrower and often split one field into several (e.g., Psychology has six WC categories).

**Research Areas (SU=)**
- Arts & Humanities: Architecture; Art; Arts & Humanities Other Topics; Asian Studies; Classics; Dance; Film, Radio & Television; History; History & Philosophy of Science; Literature; Medieval & Renaissance Studies; Music; Philosophy; Religion; Theater
- Social Sciences: Archaeology; Area Studies; Biomedical Social Sciences; Business & Economics; Communication; Criminology & Penology; Cultural Studies; Demography; Development Studies; Education & Educational Research; Ethnic Studies; Family Studies; Geography; Government & Law; International Relations; Linguistics; Mathematical Methods In Social Sciences; Psychology; Public Administration; Social Issues; Social Sciences Other Topics; Social Work; Sociology; Urban Studies; Women's Studies
- Health and behavioral areas (Life Sciences & Biomedicine): Behavioral Sciences; Geriatrics & Gerontology; Health Care Sciences & Services; Neurosciences & Neurology; Nursing; Pediatrics; Psychiatry; Public, Environmental & Occupational Health; Rehabilitation; Substance Abuse
- Also: Information Science & Library Science

**Web of Science Categories (WC=) - common non-STEM and health examples**
- Religion & humanities: Religion; Philosophy; Ethics; History; Humanities, Multidisciplinary; Literature; Cultural Studies; Area Studies; Medieval & Renaissance Studies; Folklore; Film, Radio, Television
- Social sciences: Social Work; Sociology; Family Studies; Social Issues; Social Sciences, Interdisciplinary; Social Sciences, Biomedical; Anthropology; Ethnic Studies; Women's Studies; Education & Educational Research; Communication; Political Science; Public Administration; Law; Criminology & Penology; Urban Studies; Demography; Economics; Management; Business; Industrial Relations & Labor; Information Science & Library Science; Linguistics
- Psychology: Psychology, Clinical; Psychology, Multidisciplinary; Psychology, Social; Psychology, Developmental; Psychology, Applied; Psychology, Experimental
- Health: Psychiatry; Nursing; Public, Environmental & Occupational Health; Health Policy & Services; Health Care Sciences & Services; Rehabilitation; Substance Abuse; Gerontology; Geriatrics & Gerontology; Medical Ethics

Tip: Research Areas and Categories often share a name (e.g., Religion, Social Work, Nursing, Psychiatry). When the user names one of these, use it in both WC and SU only if they ask for both; otherwise one is enough.

Note for the user: subject headings are standardized terms used to describe what a resource is about, which lets you retrieve by topic rather than by title words alone.

## Exclusions
One block at the end: `NOT TS=( "carbon fiber" OR honeycomb )`.

## Worked examples (straight quotes, ready to paste)

Example 1 - default Topic search, categories + research areas, no exclusions
```
TS=(ABS OR "FD ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" OR "fused deposition ABS") AND TS=("composite mechanics" OR "constitutive model*" OR "FEA simulation" OR "finite element analysis" OR "model accuracy" OR "local controlled propert*") AND TS=(FDM OR "fused deposition model$ing" OR "fused filament fabrication" OR "additive manufacturing" OR "3D print*" OR FFF) AND TS=(tensile OR flexural OR fatigue OR compression OR "mechanical propert*") AND PY=(1999-2025) AND (WC=("Engineering, Mechanical" OR "Engineering, Multidisciplinary" OR "Engineering, Manufacturing") OR SU=("Engineering" OR "Science & Technology Other Topics"))
```
(27 operators - well under 49.)

Example 2 - same with exclusions
```
TS=(ABS OR "FD ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" OR "fused deposition ABS") AND TS=("composite mechanics" OR "constitutive model*" OR "FEA simulation" OR "finite element analysis" OR "model accuracy" OR "local controlled propert*") AND TS=(FDM OR "fused deposition model$ing" OR "fused filament fabrication" OR "additive manufacturing" OR "3D print*" OR FFF) AND TS=(tensile OR flexural OR fatigue OR compression OR "mechanical propert*") AND PY=(1999-2025) AND WC=("Engineering, Mechanical" OR "Engineering, Manufacturing") NOT TS=("carbon fiber" OR fibrous OR honeycomb OR FGAM OR FGM)
```

Example 3 - title/abstract option, research areas, exclusions
```
(TI=(female OR wom?n OR non-binary) OR AB=(female OR wom?n OR non-binary)) AND (TI=(black OR african OR caribbean OR afro-caribbean OR afro-latina OR "african american") OR AB=(black OR african OR caribbean OR afro-caribbean OR afro-latina OR "african american")) AND (TI=(science OR technology OR engineering OR mathematics OR stem) OR AB=(science OR technology OR engineering OR mathematics OR stem)) AND (TI=(doctoral* OR doctorate* OR postdoctoral* OR phd OR post-doctoral*) OR AB=(doctoral* OR doctorate* OR postdoctoral* OR phd OR post-doctoral*)) AND PY=(2004-2024) AND SU=("Women's Studies" OR "Social Sciences Other Topics" OR "Engineering" OR "Education & Educational Research") NOT TS=("south afric*" OR "k 12" OR "high school" OR undergraduate)
```
(46 operators - close to the 49 limit; an example of when to tell the user the count and consider Topic-only.)

Example 4 - non-STEM (religion / social care), categories + research areas
```
TS=(congregation* OR church*) AND TS=("pastoral care" OR "spiritual care") AND TS=("trauma-informed") AND PY=(2015-2026) AND (WC=("Religion" OR "Social Work" OR "Psychology, Clinical") OR SU=("Religion" OR "Social Work" OR "Psychiatry"))
```
(11 operators. `church*` and `congregation*` switch lemmatization off for those words, so the singular and plural are both covered by the wildcard. Hyphens are treated as spaces, so "trauma-informed" also finds "trauma informed".)

## Pitfalls to avoid
- Curly quotes break the search - straight quotes only.
- Putting Web of Science Categories under SU (they belong under WC).
- Adding a hyphen to "Other Topics" names: it's "Social Sciences Other Topics" and "Arts & Humanities Other Topics", not "Social Sciences - Other Topics".
- Repeating TI/AB/TS for the same terms (redundant; burns operators).
- `property*` misses "properties"; use `propert*`.
- Wildcard on a term silently drops UK/US matching - use `$` where spelling differs.
