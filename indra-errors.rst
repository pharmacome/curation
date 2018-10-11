Curation Guidelines for INDRA errors
====================================

This file outlines the most common type of errors identified in the BEL statements
extracted from INDRA.

Gene-centric
~~~~~~~~~~~~

- **Knock Down**. A knock down of the gene is not labelled as such.

- **Gene skipping**. Exon/intron regulation is not labelled as such.

- **Promoter activity**. Missing promotor activity labels.

Relationship
~~~~~~~~~~~~

- **Target**. Labelled as target but not clear from the evidence. 

- **Modulate**. Labelled as modulation but not clear from the evidence. 

- **Regulate**. Labelled as regulation but not clear from the evidence.  

- **Mediate**. Labelled as mediation but not clear from the evidence. 

Identification
~~~~~~~~~~~~~~

The Named-entity recognition system labels an entity wrong. For example, confusing an abbreviation
with a different meaning (e.g., FIP means USF2 but is also a recombinant protein (FasL Interfering Protein))

Negation
~~~~~~~~

- **But not**. False positive negation.

- **Negative mediator**.

Subject/object
~~~~~~~~~~~~~~

Subject and object are correctly labelled but there is not relationship between them.

Not Evidence
~~~~~~~~~~~~

The evidence information is not sufficient to code the BEL statement.

Site of Modification
~~~~~~~~~~~~~~~~~~~~

The entity was labelled with the wrong modification site.

Physical Contact Missing
~~~~~~~~~~~~~~~~~~~~~~~~

The relationship was labelled as directed but the evidence does not show that.
