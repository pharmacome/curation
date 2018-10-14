Style Guide for BEL
===================
This document describes style guidelines for BEL. It was written with
inspiration by the pragmatism and existence of
the `PEP8 <https://www.python.org/dev/peps/pep-0008/>`_ guidelines.

Division of Content into Documents
----------------------------------
Each statement in BEL is an atomic piece of knowledge, and combine with
annotations and provenance information makes a nano-publication. This
header addresses the issue of how to organize that information into several
.bel files.

Simply, each BEL document should represent the contents of one article.
There may be reasons to include multiple articles in a single BEL document
if there is crucial supporting information, but the task of assembling BEL
for analysis is not the task of the curator.

One example where curation intervention was helpful in defining criteria
was the use of the "Subgraph" annotation in NeuroMMSig, which sliced a
large knowledgebase related to Alzheimer's disease into several discrete
subgraphs corresponding to biological pathways/mechanisms.

As an added benefit, the one-to-one correspondence of BEL scripts to
citations makes the management of curators much easier since files will
generally not conflict. This also encourages the externalization of
list annotations for reuse.

Document Metadata
-----------------
Versioning
**********
BEL documents that are manually generated (as opposed to dumps of
databases such as DrugBank) should use version numbers following
`Semantic Versioning <https://semver.org/>`_. A correct example,
using the <MAJOR>.<MINOR>.<PATCH> format:

.. code-block::

   SET DOCUMENT Version = "1.0.0"

Authorship
**********
Authors should be set comma-separated in alphabetical order by last name using

.. code-block::

   SET DOCUMENT Authors = "Daniel Domingo-Fernández, Charles Tapley Hoyt, ..."

In the description, the contributions of each author can be listed. Some suggested
roles are "curation", "supervision", "quality control".

Contact Info
************
Consider that the authors of a BEL document and the responsible person for the
integrity and correctness of the document might not be the same person. For example,
this could be due to people moving to new projects. Only the person responsible
for a given BEL document should list their contact information in the
``SET DOCUMENT ContactInfo`` field.

Organization of Terminologies
-----------------------------
The term "terminologies" is used to refer to both BEL namespaces and BEL annotations
in this section.

Terminologies' keywords should use an uppercased version of their corresponding
entry in Identifiers.org, when possible. Dots and dashes in resource names are
removed for BEL, since they are not consider valid characters for use in keywords.
Example: ``ec-code`` becomes ``ECCODE``.

Namespaces should be listed first (interspersed URL and PATTERN definitions), then
annotations (interspersed URL and PATTERN definitions), then annotations defined by
lists. Within each group, all terminologies should be listed in alphabetical order by
the keyword used.

Terminologies with multiple parts, like MeSH and GO, should **NOT** be split into
multiple namespaces (e.g. MESHD, MESHCS, MESHC, GOBP, GOCC, GOMF). Update versions
of these namespaces can be found at https://github.com/pharmacome/terminology/tree/master/external
and versioned using the git commit hashes. The following namespaces are already available:

.. code-block::

   DEFINE NAMESPACE CHEBI    AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/chebi-names.belns"
   DEFINE NAMESPACE DRUGBANK AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/drugbank-names.belns"
   DEFINE NAMESPACE ECCODE   AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/ec-code.belns"
   DEFINE NAMESPACE FPLX     AS URL "https://raw.githubusercontent.com/sorgerlab/famplex/e8ae9926ff95266032cb74f77973c84939bffbeb/export/famplex.belns"
   DEFINE NAMESPACE GFAM     AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/hgnc.genefamily-names.belns"
   DEFINE NAMESPACE GO       AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/go-names.belns"
   DEFINE NAMESPACE HGNC     AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/hgnc-names.belns"
   DEFINE NAMESPACE MESH     AS URL "https://raw.githubusercontent.com/pharmacome/terminology/1b20f0637c395f8aa89c2e2e342d7b704062c242/external/mesh-names.belns"
   DEFINE NAMESPACE MIRBASE  AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/mirbase-names.belns"
   DEFINE NAMESPACE NCBIGENE AS URL "https://raw.githubusercontent.com/pharmacome/terminology/b46b65c3da259b6e86026514dfececab7c22a11b/external/entrez.belns"

Note, while ``GFAM`` is used for ``hgnc.genefamily`` for brevity, this isn't *really* recommended.

Usage of Short vs. Long Form
----------------------------
All BEL functions (e.g., ``proteinAbundance()``, ``abundance()``, ``pathology()``, etc.)
should be abbreviated to the short forms (e.g, ``p()``, ``a()``, ``path()``, etc.).

All BEL transformations (i.e., ``activity()``, ``translocation()``, and ``reaction()``),
as well as their specific arguments (i.e. ``molecularActivity()``, ``fromLocation()``, etc.)
should be abbreviated to the short forms (i.e. ``act()``, ``tloc()``, and ``rxn()``).

All BEL relationships should be abbreviated with their short forms.

BEL is quite verbose - the theme is to always abbreviate when possible.

Usage of ``SET STATEMENT_GROUP``
--------------------------------
``STATEMENT_GROUP`` is listed in the BEL specification as a privileged annotation - it does not need to
be defined, and it can be set to anything without semantic validation.

Because it neither has inherent meaning, nor community practices ascribed to it, it is explicitly discouraged
to use this annotation.

Some curators use the ``STATEMENT_GROUP`` to give information about who the curator was, or a certain "sprint"
of curation, but these should already be addressed by the earlier point on the organization of BEL documents.

Proper Spacing
--------------
Ensure proper spacing. Without it, BEL is difficult to read and assess.

*TODO* develop a linter for continuous integration checking!

Spacing in BEL Terms
********************
The following protein with a post-translational modification is difficult
to read because there is no space between the comma following the identifier
and the ``pmod()`` function:

.. code-block::

    # Wrong
    p(HGNC:MAPT,pmod(Ph))

The same, with proper spacing applied:

.. code-block::

    p(HGNC:MAPT, pmod(Ph))

The same applies for all other variants (``sub()``, ``frag()``, ``loc()``, etc.)
and other functions in which commas are applied. The following is another
example in which the spacing between the comma following the identifier is
correct, but the contents of the ``pmod()`` are not:

.. code-block::

    # Wrong
    p(HGNC:MAPT, pmod(Ph,Y,18))

The same, with proper spacing applied:

.. code-block::

    # Correct
    p(HGNC:MAPT, pmod(Ph, Y, 18))

Spacing in Annotations
**********************
The following single annotation is difficult to read because there are
no spaces between 1) the annotation and the equals sign and 2) the
equals sign and the value:

.. code-block::

    # Wrong
    SET Disease="Alzheimer disease"

The same, with proper spacing applied:

.. code-block::

    # Correct
    SET Disease = "Alzheimer disease"

The following multiple annotation is is difficult to read, because there
no spaces between 1) the annotation and the equals, 2) the equals and the
open bracket, and 3) the entries within the brackets.

.. code-block::

    # Wrong
    SET Citation={"PubMed","12345"}

The same, with proper spacing applied:

.. code-block::

    # Correct
    SET Citation = {"PubMed", "12345"}

Citation Information
********************
Citations should be written succinctly when referring to databases like PubMed, PubMed Central and DOI. The remaining
citation information can be looked up programatically after.

.. code-block::

    # Wrong
    SET Citation = {"PubMed", "Nat Rev Drug Discov. 2018 Sep;17(9):660-688. doi: 10.1038/nrd.2018.109. Epub 2018 Aug 17.", "30116051"}

The same, with proper terseness:

.. code-block::

    # Correct
    SET Citation = {"PubMed", "30116051"}
