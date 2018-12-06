Curation Guidelines for INDRA errors
====================================
This document outlines the most common type of errors identified in the BEL statements
extracted from INDRA.

When they're encountered:

1. Add a column with the label ‘Error Type’ to your document
2. Whenever you find a type of error mentioned in the table, please put the type of error in the column. If there a
   are multiple errors, separate them with a comma.
3. If the error does not correspond to any of those categories, add a new error type to this table and give an example

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

Not codable
~~~~~~~~~~~
Cannot be code in BEL

Reversed subject/object
~~~~~~~~~~~~~~~~~~~~~~~
Subject and object are flipped in the statement.


