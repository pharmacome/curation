Encoding of Genetic Information
===============================
`BEP6 <https://github.com/belbio/bep/pull/13>`_ introduces a proper syntax for representing
epigenetic modifications, such as methylation for BEL 2.0.0+. The syntax follows the same style
as the protein modification syntax, and can follow the identifier for a gene. A reference
implementation has been included in PyBEL.

Epigenetics
-----------
The gene modification function, ``gmod()``, as a syntax for encoding epigenetic
modifications. Its usage mirrors the ``pmod()`` function for proteins and includes
arguments for methylation.

The options for ``gmod()`` are currently:

- ``M``, ``Me``, and ``methylation`` all refer to methylation on the given gene
- ``A``, ``Ac``, and ``acetylation`` all refer to acetylation on the given gene

.. code-block::

    SET Citation = {"PubMed", "17948130"}
    SET Evidence = "the methylation of NDUFB6 was found to be negatively correlated
    with its expression in a study of insulin resistance and Type II diabetes"

    SET Disease = "Type II diabetes"

    g(HGNC:NDUFB6, gmod(Me)) negativeCorrelation r(HGNC:NDUFB6)

Single Nucleotide Polymorphisms (SNPs)
--------------------------------------
In general, a single nucleotide polymorphism (SNP) refers to a variant in a
genetic sequence. The *de facto* identifiers for these variations are the RS
numbers from dbSNP. A given identifier can point to two types of information:
intrageneic SNPs and intergenic SNPs.

Intragenic SNPs
~~~~~~~~~~~~~~~
A variation in the sequence of a protein-coding gene can have the consequence
of an amino acid substitution or differential expression of the gene. In these
cases, it's important to explicitly code a BEL statement linking a SNP to its
gene with the variation to which it refers. Since BEL 2.0, variants can be
encoded according to the HGVS nomenclature.

A variant can be named multiple ways depending on the "reference sequence"
used. While it is possible to refer to a variation by the amino acid sequence
or the chromosomal sequence, it is much easier to interpret biologically when
using the gene reference sequence. Given an ``RS`` identifier, dbSNP lists the
reference sequence identifier and the HGVS string based on many of these
sequences. More specifically, reference sequence identifiers starting with
``NM`` or ``XM`` refer to the genetic sequence (and should all have the same
HGVS string), while the ``NC`` identifiers refer to the chromosome sequence
and should be disregarded.

In the future, there might be a way to automate this procedure, but as a
curator wants to encode intragenic SNPs, they should also make this equivalence
explicit. These statements can be grouped together in a citation to dbSNP, the
evidence can be dummy text, and the confidence level can be set with
``SET Confidence = "Axiomatic"``.

First, dbSNP can be included using a regular expression definition of a namespace,
since there are potentially billions of enumerated SNPs. This is a BEL 2.0.0+ feature
that was proposed in `BEP5 <https://github.com/belbio/bep/pull/12>`_. Identifiers.org
lists the database information at https://www.ebi.ac.uk/miriam/main/datatypes/MIR:00000161,
and includes a regular expression that all accession numbers follow. This can be included as

.. code-block::

    DEFINE NAMESPACE DBSNP AS PATTERN "^rs\d+$"

The following is an example from https://www.ncbi.nlm.nih.gov/projects/SNP/snp_ref.cgi?rs=1235 that
uses the ``equivalentTo`` relationship proposed by `BEP4 <https://github.com/belbio/bep/pull/11>`_
for BEL 2.0.0+ to link a dbSNP entry to the HGVS nomenclature applied to a gene.

.. code-block::

    SET Citation = {"Other", "dbSNP", "https://www.ncbi.nlm.nih.gov/projects/SNP/"}
    SET Evidence = "Extracted from dbSNP"

    SET Confidence = "Axiomatic"

    g(HGNC:MDGA2, var("c.*1638C>A")) equivalentTo g(DBSNP:rs1235)

A reference implementation is provided by PyBEL, in which the hasVariant relationship
``g(HGNC:MDGA2) hasVariant g(dbSNP:rs1235)`` is automatically added by the compiler.

An example from a genome-wide association study:

.. code-block::

    SET Citation = {"PubMed", "27076484"}
    SET Evidence = "The "GG" genotype of rs9331888 was significantly more frequent in patients with LOAD.
    The "CC" genotype of the SNP was significantly more frequent in controls. The rs9331888 "GG" genotype in patients
    and the "CC" genotype in controls were significantly higher in non-∊4 allele carriers of APOE The haplotype
     analysis showed the CLU "GCG" haplotype was a risk haplotype. Our findings indicate the rs9331888 SNP of CLU is
     associated with LOAD independent of APOE."

    g(HGNC:CLU) hasVariant g(DBSNP:rs9331888)
    g(DBSNP:rs9331888) -- path(MESH:"Alzheimer Disease")

Intergenic SNPs
~~~~~~~~~~~~~~~
Some SNPs are not directly part of coding genes’ regions. For these SNPs, it is
not necessary to encode a relationship to a gene.

However, this also means that their functional consequences do not follow
directly from the causal relationships connected to a particular gene. It must
be kept in mind that these SNPs will need further qualifications to become
useful, such as associations from LD-Block analysis or other studies from eQTL,
etc.

LD-Block Information
~~~~~~~~~~~~~~~~~~~~
Linkage disequilibrium (LD) block analysis find SNPs that co-occur together. These
relationships can be inferred from data-driven approaches.

*TODO*

eQTL Information
~~~~~~~~~~~~~~~~
Expression quantitative trait loci (eQTLs) connect variants to gene expression
patterns.

*TODO*
