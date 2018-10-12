BEP8 - A style guide for BEL
============================
This document describes style guidelines for BEL. It was written with
inspiration by the pragmatism and existence of PEP8 guidelines.

Division of Content into Documents
----------------------------------
Each statement in BEL is an atomic piece of knowledge, and combine with
annotations and provenance information makes a nano-publication. This
header addresses the issue of how to organize that information into several
*.bel files.

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

Organization of Terminologies
-----------------------------
Terminologies with multiple parts, like MeSH and GO, should **NOT** be split into
multiple namespaces (e.g. MESHD, MESHCS, MESHC, GOBP, GOCC, GOMF).

Usage of Short vs. Long Form
----------------------------
All BEL functions (e.g., `proteinAbundance()`, `abundance()`, `pathology()`, etc.)
should be abbreviated to the short forms (e.g, `p()`, `a()`, `path()`, etc.).

All BEL transformations (i.e., `activity()`, `translocation()`, and `reaction()`),
as well as their specific arguments (i.e. `molecularActivity()`, `fromLocation()`, etc.)
should be abbreviated to the short forms (i.e. `act()`, `tloc()`, and `rxn()`).

All BEL relationships should be abbreviated with their short forms.

BEL is quite verbose - the theme is to always abbreviate when possible.

Proper Spacing
--------------
Ensure proper spacing. Without it, BEL is difficult to read and assess.

TODO: develop a linter for continuous integration checking!

Spacing in BEL Terms
********************
The following protein with a post-translational modification is difficult
to read because there is no space between the comma following the identifier
and the `pmod()` function:

.. code-block::

	p(HGNC:MAPT,pmod(Ph))

The same, with proper spacing applied:

.. code-block::

	p(HGNC:MAPT, pmod(Ph))

The same applies for all other variants (`sub()`, `frag()`, `loc()`, etc.)
and other functions in which commas are applied. The following is another
example in which the spacing between the comma following the identifier is
correct, but the contents of the `pmod()` are not:

.. code-block::

	p(HGNC:MAPT, pmod(Ph,Y,18))

The same, with proper spacing applied:

.. code-block::

	p(HGNC:MAPT, pmod(Ph, Y, 18))

Spacing in Annotations
**********************
The following single annotation is difficult to read because there are
no spaces between 1) the annotation and the equals sign and 2) the
equals sign and the value:

.. code-block::

	SET Disease="Alzheimer disease"

The same, with proper spacing applied:

.. code-block::

	SET Disease = "Alzheimer disease"

The following multiple annotation is is difficult to read, because there
no spaces between 1) the annotation and the equals, 2) the equals and the
open bracket, and 3) the entries within the brackets.

.. code-block::

	SET Citation={"PubMed","12345"}

The same, with proper spacing applied:

.. code-block::

	SET Citation = {"PubMed", "12345"}
