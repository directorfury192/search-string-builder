# DB_Scopus - Database Profile

Database: Scopus (Elsevier). Where to paste: Scopus > Search > Advanced document search > the query box.
Sources: https://service.elsevier.com/app/answers/detail/a_id/11365/supporthub/scopus/ and https://blog.scopus.com/posts/6-simple-search-tips-lessons-learned-from-the-scopus-webinar

## Default search fields
`TITLE-ABS-KEY ( ... )` = title, abstract and keywords. Put this tag in front of EVERY concept group. (A group without a field tag is searched in all fields, which is much broader.)
Alternatives to offer: `TITLE ( ... )` (title only, most precise), `TITLE-ABS ( ... )`, `ALL ( ... )` (everything, broadest).

## Operators and order of precedence
Scopus processes operators in this order: **OR first, then AND, then AND NOT.**
Example: `KEY(mouse AND NOT cat OR dog)` is read as `KEY((mouse) AND NOT (cat OR dog))`.
- Always use parentheses to make the grouping explicit.
- Put AND NOT at the END of the query, as one block.
- Because OR is processed before AND, never write unbracketed mixes like `professional AND trajectory OR career AND choice`; use phrases instead: `"professional trajectory" OR "career choice"`.
Parentheses examples: `influenza OR flu AND avian` is read as `(influenza OR flu) AND avian` in Scopus - but write the brackets anyway so the meaning is obvious.

## Phrases and exact match
- Double quotes = **loose phrase**: words must appear together, but plurals and spelling variants are still included, and punctuation is ignored. `"heart attack"` also finds heart attacks, heart-attack.
- Without quotes, `heart attack` finds heart and attack anywhere (implicit AND).
- Braces = **exact phrase**: `{oyster toadfish}` matches exactly what is typed, including stop words, spaces and punctuation. `{heart-attack}` and `{heart attack}` give different results. Wildcards inside braces are treated as literal characters.
- **When the user asks for an exact match on a word, use braces: `{cat}`** (quotes are not enough in Scopus because loose phrases still include plurals/variants).

## Automatic features
- Lemmatization: singular/plural and adjective forms are found automatically (attack/attacks; wide/wider).
- Equivalents: ω = omega; behaviour = behavior (US/UK spellings matched automatically in most cases).
- Accented characters work with or without accents (Dvořák = Dvorak).
- Punctuation (commas, ?, ! etc.) ignored, except hyphens and dots, which make a loose phrase: heart-attack is searched as "heart attack".
- Stop words (the, it, of) are ignored unless inside quotes or braces.

## Wildcards and truncation
- `?` = exactly one character: `wom?n` finds woman, women.
- `*` = any number of characters, including none: `comput*` finds computer, computers, computerize, computerization; `*tocopherol` finds α-tocopherol, tocopherol.
- Wildcards work inside loose phrases: `"criminal* liab*"` finds criminally liable, criminal liability.
- Wildcards cannot stand alone; a hyphen/dot/slash between a wildcard and a word drops the wildcard (`abs(iwv-*)` is searched as `abs(iwv)`).
- Truncate at the right stem: `propert*` (finds property AND properties) - NOT `property*` (misses properties).
- Prefer lemmatization over wildcards for simple plurals; use wildcards for genuinely different endings (model* = model, models, modeling, modelling).

## Dates
Field `PUBYEAR` with `>` / `AFT` (after), `<` / `BEF` (before), `=` / `IS` (equal).
For an inclusive range Y1-Y2 write: `PUBYEAR > (Y1-1) AND PUBYEAR < (Y2+1)`. Example for 1999-2025: `PUBYEAR > 1998 AND PUBYEAR < 2026`. Single year: `PUBYEAR = 2020`.

## Subject filter step (Scopus Subject Areas)
Ask for the subject areas, match each to the closest option below, show the user a preview of the tags selected and let them correct it. Syntax: `SUBJAREA ( TAG1 OR TAG2 )`. Every Scopus journal/book has at least one ASJC subject area. SUBJAREA accepts only the four-letter top-level codes in the two tables below (all 27 Scopus subject areas). The "Includes" column lists the narrower subjects that fall under each code, to help you match what the user says (e.g., "religion" -> ARTS, "social work" -> SOCI, "counseling" -> PSYC). Narrower subjects cannot be searched on their own with SUBJAREA. Source: https://www.elsevier.support/scopus/answer/what-is-the-complete-list-of-asjc-subject-areas-in-scopus

### STEM subject areas

| Subject Area | Tag | Includes (examples) |
|---|---|---|
| Engineering | ENGI | Aerospace, Automotive, Biomedical, Civil & Structural, Computational Mechanics, Control & Systems, Electrical & Electronic, Industrial & Manufacturing, Mechanical Engineering, Mechanics of Materials, Ocean, Safety/Risk/Reliability & Quality, Media Technology, Building & Construction, Architecture |
| Materials Science | MATE | Biomaterials, Ceramics & Composites, Electronic/Optical/Magnetic Materials, Materials Chemistry, Metals & Alloys, Polymers & Plastics, Surfaces/Coatings & Films |
| Chemical Engineering | CENG | Bioengineering, Catalysis, Chemical Health & Safety, Colloid & Surface Chemistry, Filtration & Separation, Fluid Flow & Transfer Processes, Process Chemistry & Technology |
| Chemistry | CHEM | Analytical, Electrochemistry, Inorganic, Organic, Physical & Theoretical, Spectroscopy |
| Computer Science | COMP | AI, Computational Theory, Computer Graphics & CAD, Networks, Applications, Computer Vision, Hardware, HCI, Information Systems, Signal Processing, Software |
| Earth & Planetary Sciences | EART | Atmospheric Science, Geology, Geophysics, Geotechnical Engineering, Oceanography, Space & Planetary Science, etc. |
| Energy | ENER | Energy Engineering & Power Technology, Fuel Technology, Nuclear Energy & Engineering, Renewable Energy |
| Environmental Science | ENVI | Ecology, Environmental Chemistry, Environmental Engineering, Pollution, Waste Management, Water Science, etc. |
| Mathematics | MATH | Applied Mathematics, Computational Mathematics, Control & Optimization, Modelling & Simulation, Numerical Analysis, Statistics & Probability, etc. |
| Physics & Astronomy | PHYS | Condensed Matter, Acoustics, Nuclear/High-energy, Optics, etc. |
| All Physical Sciences | CENG OR CHEM OR COMP OR EART OR ENER OR ENGI OR ENVI OR MATE OR MATH OR PHYS | Combined physical sciences |

### Social sciences, humanities, health and life sciences subject areas

| Subject Area | Tag | Includes (examples) |
|---|---|---|
| Arts and Humanities | ARTS | History, Language and Linguistics, Archaeology, Classics, Conservation, History and Philosophy of Science, Literature and Literary Theory, Museology, Music, Philosophy, **Religious Studies** (theology, ministry, congregations), Visual and Performing Arts |
| Social Sciences | SOCI | Sociology, Anthropology, Education, Communication, Cultural Studies, Gender Studies, Demography, Development, Geography/Planning, Law, Political Science and International Relations, Public Administration, Library and Information Sciences, Urban Studies, Health (social science), **Social Work**-related research, Life-span and Life-course Studies |
| Psychology | PSYC | Clinical, Applied, Developmental and Educational, Social, Experimental and Cognitive, Neuropsychology (trauma, counseling, mental health research often sits here) |
| Business, Management and Accounting | BUSI | Management, Marketing, Organizational Behavior and HR, Strategy, Tourism, Accounting |
| Economics, Econometrics and Finance | ECON | Economics, Econometrics, Finance |
| Decision Sciences | DECI | Information Systems and Management, Management Science, Statistics and Probability (applied) |
| Nursing | NURS | Nursing specialties, including community, mental health and palliative care nursing |
| Health Professions | HEAL | Allied health, occupational therapy, physical therapy, speech-language pathology, chiropractic, emergency medical services |
| Medicine | MEDI | All clinical medicine, including Psychiatry and Mental Health, Public Health, Health Policy, Family Practice, Geriatrics |
| Neuroscience | NEUR | Behavioral, cognitive and clinical neuroscience |
| Pharmacology, Toxicology and Pharmaceutics | PHAR | Pharmacology, Toxicology, Pharmaceutical Science |
| Agricultural and Biological Sciences | AGRI | Agronomy, Ecology, Food Science, Forestry, Plant and Animal Science |
| Biochemistry, Genetics and Molecular Biology | BIOC | Biochemistry, Genetics, Molecular and Cell Biology |
| Immunology and Microbiology | IMMU | Immunology, Microbiology, Virology |
| Veterinary | VETE | Veterinary medicine |
| Dentistry | DENT | Dentistry |
| Multidisciplinary | MULT | Broad journals such as Nature, Science, PLOS ONE |

Common combined filters:
- All Social Sciences & Humanities: `SUBJAREA ( ARTS OR SOCI OR PSYC OR BUSI OR ECON OR DECI )`
- All Health Sciences: `SUBJAREA ( MEDI OR NURS OR HEAL OR DENT OR VETE )`
- Religion + social care topics (e.g., pastoral or spiritual care): `SUBJAREA ( ARTS OR SOCI OR PSYC OR NURS OR MEDI )` - pastoral/spiritual care research is spread across religion, social science, psychology, nursing and medicine (chaplaincy) journals, so filtering to ARTS and SOCI alone can miss a lot.

## Exclusions
One block at the very end: `AND NOT TITLE-ABS-KEY ( term1 OR "phrase two" )`.

## Worked examples (straight quotes, ready to paste)

Example 1 - subject area, no exclusions
```
TITLE-ABS-KEY ( ABS OR "FD-ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" ) AND TITLE-ABS-KEY ( "composite mechanics" OR "constitutive model*" OR "FEA simulation" OR "finite element analysis" OR "model accuracy" OR "local controlled propert*" ) AND TITLE-ABS-KEY ( FDM OR "fused deposition model*" OR "fused filament fabrication" OR "additive manufacturing" OR "3D print*" OR FFF ) AND TITLE-ABS-KEY ( tensile OR flexural OR fatigue OR compression OR "mechanical propert*" ) AND PUBYEAR > 1998 AND PUBYEAR < 2026 AND SUBJAREA ( ENGI OR MATE )
```

Example 2 - subject area and exclusions
```
TITLE-ABS-KEY ( ABS OR "FD-ABS" OR "ABS filament" OR "acrylonitrile butadiene styrene" ) AND TITLE-ABS-KEY ( "composite mechanics" OR "constitutive model*" OR "FEA simulation" OR "finite element analysis" OR "model accuracy" OR "local controlled propert*" ) AND TITLE-ABS-KEY ( FDM OR "fused deposition model*" OR "fused filament fabrication" OR "additive manufacturing" OR "3D print*" OR FFF OR "rapid prototyping" ) AND TITLE-ABS-KEY ( tensile OR flexural OR fatigue OR compression OR "mechanical propert*" ) AND PUBYEAR > 1998 AND PUBYEAR < 2026 AND SUBJAREA ( ENGI ) AND NOT TITLE-ABS-KEY ( "carbon fiber" OR fibrous OR honeycomb OR metal OR lattice )
```

Example 3 - no subject areas, no exclusions
```
TITLE-ABS-KEY ( female OR wom?n OR non-binary ) AND TITLE-ABS-KEY ( black OR african OR caribbean OR afro-caribbean OR afro-latina OR "african american" ) AND TITLE-ABS-KEY ( science OR technology OR engineering OR mathematics OR stem ) AND TITLE-ABS-KEY ( doctoral OR postdoctoral OR doctorate-holding OR phd OR post-doctoral ) AND TITLE-ABS-KEY ( academia OR professorial OR professor OR academe OR postdocs OR workforce OR "professional advancement" OR "professional trajectory" OR "research career" OR "research scientist" OR "academic career" OR "career trajectory" OR "career choice" ) AND PUBYEAR > 2003 AND PUBYEAR < 2025
```

Example 4 - exclusions, no subject areas
```
TITLE-ABS-KEY ( female OR wom?n OR non-binary ) AND TITLE-ABS-KEY ( black OR african OR caribbean OR afro-caribbean OR afro-latina OR "african american" ) AND TITLE-ABS-KEY ( science OR technology OR engineering OR mathematics OR stem ) AND TITLE-ABS-KEY ( doctoral OR postdoctoral OR doctorate-holding OR phd OR post-doctoral ) AND TITLE-ABS-KEY ( "professional trajectory" OR "career trajectory" OR "career choice" ) AND NOT TITLE-ABS-KEY ( "high school" OR athlet* OR k-12 OR elementary OR medical OR male )
```

Example 5 - non-STEM (religion / social care), subject areas, no exclusions
```
TITLE-ABS-KEY ( congregations OR churches ) AND TITLE-ABS-KEY ( "pastoral care" OR "spiritual care" ) AND TITLE-ABS-KEY ( "trauma-informed" ) AND PUBYEAR > 2014 AND PUBYEAR < 2027 AND SUBJAREA ( ARTS OR SOCI OR PSYC OR NURS )
```
(Without braces, Scopus lemmatization also finds congregation, church and church's. Use `{churches}` only if the user explicitly wants that exact word. The loose phrase "trauma-informed" also finds "trauma informed care", "trauma-informed practices", and so on.)

## Pitfalls to avoid
- Curly quotes (“ ”) break the search - use straight quotes only.
- Leaving a concept group without `TITLE-ABS-KEY` silently broadens it to all fields.
- Unbracketed AND inside an OR list (OR binds first in Scopus).
- Putting AND NOT in the middle of the query.
- Using quotes when the user wants an exact match - use braces.
