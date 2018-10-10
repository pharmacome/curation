Chemical Biology Curation Guidelines
====================================
This document containts an initial (and as-of-yet incomplete) set of
guidelines for representing quantitative information in BEL. They do
not require any special extensions to its syntax, and should be
compatible with any of the available parsers/compilers.

There is currently a BEL enhancement propopsal for BEL 2.0.0+ for
`native support of numeric annotations <https://github.com/belbio/bep/pull/16>`_
that would benefit from public input, so that's highly encouraged!

Inhibitors
----------
This example will focus on the ability for lovastatin (CHEMBL1487) to
inhibit human HMG-CoA reductase (CHEMBL402, UniProt:P04035, HGNC:HMGCR,
HGNC:5006).

Simple Representation
~~~~~~~~~~~~~~~~~~~~~
.. code-block::

	a(CHEMBL:CHEMBL1487) =| act(p(UNIPROT:P04035))

Medium-Granular Representation with BEL Default Namespace
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block::

	a(CHEMBL:CHEMBL1487) =| act(p(UNIPROT:P04035), ma(cat))

Specific Representation
~~~~~~~~~~~~~~~~~~~~~~~
Using BEL 2.0, the molecular function HMGCR that lovastatin inhibits
is its (hydroxymethylglutaryl-CoA reductase (NADPH) activity (GO:0004420).

.. code-block::

	a(CHEMBL:CHEMBL1487) =| act(p(UNIPROT:P04035), ma(GO:0004420))

In general, it might not be so obvious how specific of a GO term to
choose. Additionally, a protein may have multiple functions. Complementary
to GO is the ExPASy enzyme classification, which is also encoded in ChEBI
and can be automatically added to BEL.

Assay Metadata
~~~~~~~~~~~~~~
Taking inspiration from the ChEBML schema, several pieces of metadata
can make inhibition experiments more useful:

1. Target Type (e.g., cell line, organism, single protein, complex, etc.)
2. Measurement Type (e.g., IC50, pIC50, EC50, pEC50, Ki)
3. Measurement Units (e.g., pM, nM, μM, mM, M)
4. Measurement Relation (=, >, <, >=, <=, ~)
5. Measurement Value (floating point matching the regular expression:
   ``^[-+]?[0-9]*\.?[0-9]+([eE][-+]?[0-9]+)?$``)
6. Assay Type (see below)
7. Cell line, target organism, and/or species

In some cases, the measurement value may be reported as a range. In these
situations, use two complementary annotations for Measurement Range Lower
and Measurement Range Upper.

Assay Type (adapted from `ChEMBL <https://www.ebi.ac.uk/chembl/faq>`_)
**********************************************************************
- Binding (B) - Data measuring binding of compound to a molecular target,
  e.g. Ki, IC50, Kd.
- Functional (F) - Data measuring the biological effect of a compound,
  e.g. %cell death in a cell line, rat weight.
- ADMET (A) - ADME data e.g. t1/2, oral bioavailability.
- Toxicity (T) - Data measuring toxicity of a compound, e.g., cytotoxicity.
- Physicochemical (P) - Assays measuring physicochemical properties of
  the compounds in the absence of biological material e.g., chemical
  stability, solubility.
- Unclassified (U) - A small proportion of assays cannot be classified
  into one of the above categories e.g., ratio of binding vs efficacy.

After adding this metadata, we get:

.. code-block::

	SET AssayType = "B"
	SET MeasurementType = "IC50"
	SET MeasurementUnits = "nM"
	SET MeasurementRelation = "="
	SET MeasurementValue = "0.5"

	SET Species = "9606"
	SET Cell = "HEPG2"

	a(CHEMBL:CHEMBL1487) =| act(p(UNIPROT:P04035), ma(GO:0004420))

Provenance
~~~~~~~~~~
Using a valid citation that points to the original source of the information
is preferred to using a refernce to the database from which the relation
comes. Example: it's better to use `PMID:2153213 <https://www.ncbi.nlm.nih.gov/pubmed/2153213>`_
in these examples referring to its original publication rather than citing ChEMBL.

However, data often comes in a table, and won't have a real evidence text.
It's not *exactly* clear whether BEL requires evidences for each statement,
so for now a placeholder string saying "Retrieved from X" and an additional
annotation called ``Database`` set to ``X`` will allow forward-compatibility.
Use an identifiers.org namespace whenever possible for ``X``.

Finally, with both the assay metadata and provenance, we get:

.. code-block::

	SET Citation = {"PubMed", "2153213"}
	SET Evidence = "Retrieved from ChEMBL"
	SET Database = "chembl"

	SET AssayType = "B"
	SET MeasurementType = "IC50"
	SET MeasurementUnits = "nM"
	SET MeasurementRelation = "="
	SET MeasurementValue = "0.5"

	SET Species = "9606"
	SET Cell = "HEPG2"

	a(CHEMBL:CHEMBL1487) =| act(p(UNIPROT:P04035), ma(GO:0004420))

Receptor Binding
----------------
This example will focus on the binding of zolpidem (CHEMBL911) to the
GABA receptor alpha-5 subunit (CHEMBL5112, UniProt:A8K338, HGNC:GABRA5)

The binding of a chemical to a receptor is represented by the chemical
causing a complex with the protein. Binding is typically measured with
Ki.

.. code-block::

	SET AssayType = "B"
	SET MeasurementType = "Ki"
	SET MeasurementUnits = "nM"
	SET MeasurementRelation = ">"
	SET MeasurementValue = "15000"

	SET Species = "9606"

	a(CHEMBL:CHEMBL911) => complex(p(UNIPROT:A8K338), a(CHEMBL:CHEMBL911))

Zolipidem is not a very strong binder to the GABA receptor alpha-5 subunit,
so it is unlikely we'll find an annotation as to its binding type.

Binding Type
~~~~~~~~~~~~
- *Full agonist*s are able to activate the receptor and result in a strong
  biological response. The natural endogenous ligand with the greatest
  efficacy for a given receptor is by definition a full agonist (100% efficacy).
- *Partial agonist*s do not activate receptors with maximal efficacy, even
  with maximal binding, causing partial responses compared to those of full
  agonists (efficacy between 0 and 100%).
- *Antagonist*s bind to receptors but do not activate them. This results
  in a receptor blockade, inhibiting the binding of agonists and inverse
  agonists. Receptor antagonists can be competitive (or reversible), and
  compete with the agonist for the receptor, or they can be irreversible
  antagonists that form covalent bonds (or extremely high affinity
  non-covalent bonds) with the receptor and completely block it. The
  proton pump inhibitor omeprazole is an example of an irreversible
  antagonist. The effects of irreversible antagonism can only be reversed
  by synthesis of new receptors.
- *Inverse agonist*s reduce the activity of receptors by inhibiting their
  constitutive activity (negative efficacy).

.. todo:: add full agonist example
.. todo:: add partial agonist example
.. todo:: add antagonist example

Allostery
~~~~~~~~~
In general, if allostery is not set, then it is assumed to be None.

Allosteric modulators do not bind to the agonist-binding site of the receptor
but instead on specific allosteric binding sites, through which they modify
the effect of the agonist. For example, benzodiazepines (BZDs) bind to the
BZD site on the GABAA receptor and potentiate the effect of endogenous GABA.

	- Positive allosteric modulator
	- Negative allosteric modulator

Source: https://en.wikipedia.org/wiki/Receptor_(biochemistry)

When the binding type is set, we can also write a second statement with how
the binding affects the activity of the receptor.

Basmisanil (CHEMBL3681419) is an inverse agonist of the GABA receptor alpha-5
subunit (UNIPROT:A8K338).

.. code-block::

	SET Citation = {"Patent", "US-8846719-B2"}

	SET AssayType = "B"
	SET MeasurementType = "Ki"
	SET MeasurementUnits = "nM"
	SET MeasurementRelation = "="
	SET MeasurementValue = "445.47"

	SET BindingType = "Inverse agonist"
	SET Allostery = "Negative"

	SET Species = "9606"

 	# Basmisanil binds GABA receptor alpha-5
	a(CHEBML:CHEMBL3681419) => complex(p(UNIPROT:A8K338), a(CHEMBL:CHEMBL3681419))

  	# Binding of basmisanil decreases the activity of the receptor
	complex(p(UNIPROT:A8K338), a(CHEMBL:CHEMBL3681419)) =| act(p(UNIPROT:A8K338))
