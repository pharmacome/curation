Recuration Guidelines
=====================
These guidelines were originally written for the re-curation of several
NeuroMMSig subgraphs in the Alzheimer's Disease Knowledge Assembly during
the Human Brain Pharmacome project, but may be generally applicable to
other BEL scripts as well.

Normalizing Entities
--------------------
Chemicals
~~~~~~~~~
1. Normalize chemical entities to preferred namespaces (*ChEBI*, *ChEBML*,
   *PubChem*) whenever posssible. *MeSH* is explicitly discoraged becuase it is
   difficult to look up their structures as SMILES or InChI, even with
   resolving services like UniChem
2. Formalize knowledge about chemicals that have not yet been encoded in
   *ChEBI* (such as Selventa chemicals [*SCHEM*], the BELIEF chemical namespaces, etc.),
   drawing from other public resources (*PubChem*, *MeSH*, *CAS*, *ChEMBL*,
   UniChem, BridgeDB, ChemSpider, etc.) whenever possible

Protein Complexes and Families
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
`FamPlex <https://github.com/sorgerlab/famplex>`_ has emerged as a
resource that maps families and protein complexes (including the Selventa
mappings *SFAM* and *SCOMP* as well as other widely used namespaces like
PFAM and InterPro).

1. Normalize all entities to FamPlex
2. Formalize knowledge about new families by making a pull request to
   FamPlex. See: https://github.com/sorgerlab/famplex#contributing

Other Entities
~~~~~~~~~~~~~~
We are also building a terminology at https://github.com/pharmacome/terminology.
This should not be done lightly, so see https://github.com/pharmacome/terminology#contributing
for contribution guidelines and rules.

Checking Correctness
--------------------
- If statement can be asserted from the given evidence, add the annotation
  ``SET Confidence = "High"``
- If the statement is wrong, fix it and add the annotation
  ``SET Confidence = "Medium"``
- If it's not clear what BEL should represent the biology, add
  ``SET Confidence = "Low"`` for later discussion
- If the evidence string contains no reasonable biological knowledge/is
  nonsense, delete it and the related statements entirely. It's okay to remove
  BEL statements that are not supported.

Finalization
~~~~~~~~~~~~
After all relevant statements have been checked for correctness, the
curation leader will check all statements with ``SET Confidence = "High"``
or ``SET Confidence = "Medium"`` and change to ``SET Confidence = "Very High"``
if they agree. If they do not agree, they will fix it themselves.
