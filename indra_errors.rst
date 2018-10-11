Curation Guidelines for INDRA errors
====================================

This file outlines the most common type of errors identified in the BEL statements
extracted from INDRA.

Gene-centric
~~~~~~~~~~~~

- **Knock Down**. A knock down of the gene is not labelled as such.

- **Gene skipping**.

- **Promoter activity**.

Relationship
~~~~~~~~~~~~

- **Target**. 

- **Modulate**.

- **Mediates**.

Identification
~~~~~~~~~~~~~~

The Named-entity recognition system labels an entity wrong. For example, confusing an abbreviation
with a different meaning (e.g., FIP means USF2 but is also a recombinant protein (FasL Interfering Protein))

Negation
~~~~~~~~

- **But not**.

- **Negative mediator**.

Subject/object
~~~~~~~~~~~~~~

If the subject or the object are in the evidence but don’t have a relationship

Not Evidence
~~~~~~~~~~~~

If the evidence chosen cannot\should not be coded in BEL. Also if it’s incomplete or unclear


Site of Modification
~~~~~~~~~~~~~~~~~~~~

If the specific site of protein modification (amino acid residue) is not correct 


Physical Contact Missing
~~~~~~~~~~~~~~~~~~~~~~~~

If the evidence does not describe a direct increase/decrease
