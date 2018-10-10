Curation using INDRA
====================
This document describes a procedure for using `INDRA <https://github.com/sorgerlab/indra>`_
for acquiring automatically extracted relations in BEL for curation.

1. Identification of target entities
------------------------------------
Curation begins from a seed list of entities. Often, this will be genes of interest
to a project or based on a rational assessment of information density in a network.

2. Gather statements from INDRA
-------------------------------
After acquiring statements from the `INDRA REST Database <https://indra.readthedocs.io/en/latest/modules/sources/indra_db_rest/index.html>`_,
several filters are made to the resulting

1. Statements containing chemicals are filtered. They are more difficult to curate because of the heterogeneity of
   chemical nomenclatures and identifiers, and many times can be replaced by the use of databases like ChEMBL, CTD,
   PubChem, etc.
2. Confidences are calculated for each statement based on INDRA's BELIEF engine, which takes into account high-quality
   material that has been previously curated in Pathway Commons, Selventa's Large BEL Corpus, and other sources.
   Statements of different levels of granularity are linked, and confidences can be calculated.
3. When several text-based evidences are available for a given statement, one is chosen randomly so as to avoid
   curator fatigue.

3. Preparation of Curation Sheets
---------------------------------
The filtered content is exported to a CSV file containing the following columns:

1. INDRA UUID. A unique identifier assigned to each statement in the INDRA database
2. INDRA Confidence. The estimated percentage (0.0 - 1.0) for how correct a statement is
3. Text Reference. The PubMed identifier of the article from which the statement was automatically extracted
4. Text. The text from which the statement was extracted
5. INDRA API. The text mining system used by INDRA to extract the statement
6. BEL Subject
7. BEL Predicate
8. BEL Object
9. Checked
10. Correct
11. Changed
12. Annotations

4. Curation
-----------
Each statement should be read and assessed by the curator, then an "x" should be placed in the "Checked" column.

- If the statement was correct, an "x" should be placed in the "Correct" column.
- Otherwise, the statement should be fixed (assignment of entity types, relation, etc.) and an "x" should be placed
  in the "Changed" column.
- If the statement is total nonsense, then no checks should be placed in either the "Correct" or "Changed" columns.

If there are other BEL that can be extracted, make a new line with all of the same provenance information
(uuid, reference, evidence, etc.) and just place an "x" in the "Changed" column.

If there are any annotations (cell type, species, cell line, tissue, experimental context, etc.) that are
obvious from the evidence, then they can be denoted in the "Annotations" column using the BEL idiom of
`SET ANNOTATION ...` statements.

5. Re-Curation
--------------
Finally, the statements should be exported to BEL and checked using the
`re-curation procedure <https://github.com/pharmacome/curation/blob/master/recuration.rst>`_.
