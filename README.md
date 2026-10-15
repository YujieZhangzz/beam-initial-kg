# HIV virologic failure: evidence explorer

An interactive explorer for an initial knowledge graph of factors associated with HIV virologic
failure. It contains 1,489 relationships among 961 entities, supported by 839 PubMed articles.

**Open the explorer:** https://yujiezhangzz.github.io/beam-initial-kg/

**Expanded version (v5):** https://yujiezhangzz.github.io/beam-initial-kg/v5/ (`v5/index.html`).
It adds 3,257 abstracts from two further sources: articles cited by the KG articles but not yet in
the corpus, and MedCPT retrieval with seven HIV-specific queries based on the Andersen model
(provider relationship, clinic and pharmacy services, retention in care, regimen characteristics,
support and reminders, stigma / health literacy / substance use, beliefs and competing
priorities). It contains 4,649 relationships among 2,589 entities, supported by 2,992 articles
published 1993–2026. Every article shows its retrieval source(s) and publication year. A
year-range slider and source checkboxes at the top filter every tab. The earlier `/v4/` link
redirects here.

The explorer is a single self-contained page (`index.html`) with these tabs:

- **Relationships**: a searchable, filterable table. Click a row to read the verbatim sentence from
  each supporting abstract, with a link to PubMed and its evidence type.
- **Graph**: the network, with a slider for the minimum number of supporting articles per
  connection.
- **Factor × outcome**: a matrix of the most-supported factors against key outcomes.
- **Pathways**: chains of steps leading to virologic failure, selected by an explicit rule.
- **Methods**: search terms, extraction and entity-merging rules, and limitations.

## How the graph was built

Abstracts came from two sources:

- a PubMed keyword search (976 abstracts);
- MedCPT semantic retrieval run through the LitSense 2.0 API (387 additional abstracts).

A large language model (claude-sonnet-5) extracted relationships that each abstract explicitly
reports, together with a verbatim evidence sentence. Relationships whose sentence could not be
found word for word in the abstract were removed.

In a second pass, each relationship's direction was read strictly from its evidence sentence:

- positively associated: more of the subject goes with more of the object;
- negatively associated: more of the subject goes with less of the object;
- direction not stated.

The same pass recorded the evidence type: independent predictor (adjusted analysis), association,
or mediation. Synonymous entity names were then merged by hand-written rules and embedding
similarity. The Methods tab gives the full details.

This is a pilot for inspection and critique, not a validated evidence synthesis. Article counts
show how often a finding is reported. They do not measure effect size or study quality.

The page opens offline from a downloaded copy, except the Graph tab, which loads its drawing
library (vis-network) from a CDN.
