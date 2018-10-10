Rational Enrichment
===================
This document describes an approach to enrich knowledge assemblies
based on topological novelty.

1. Assemble BEL from Relevant Sources
-------------------------------------
1. Assemble BEL from relevant sources
2. Re-curate content with questionable quality following the
   `re-curation procedure <https://github.com/pharmacome/curation/blob/master/recuration.rst>`_
3. *Optional*: choose annotations that are relevant and filter the resulting network.
   During the initial stages of the Human Brain Pharmacome project, we used the
   "Subgraph" annotation from NeuroMMSig to select our `ten highest priority candidate
   mechanisms <https://pharmacome.scai.fraunhofer.de/index.php/2018/08/04/our-priority-mechanisms/>`_
   of pathogenesis of Alzheimer's disease.

2. Identify Low-Information Nodes
---------------------------------
The information density of each node is assessed to provide an un-biased prioritization list of genes/proteins.

1. Chemicals and higher-order processes (e.g., biological processes, phenotypes, pathologies, clinical measurements,
   etc.) are filtered from the resulting network. From a molecular-biology point of view, these are the logical inputs
   and outputs to a biological system.
2. Proteins, mRNAs, miRNAs, and all variants are collapsed to their corresponding genes' nodes.
3. The information density of each node is defined as the *degree*: the sum of the in-degree and out-degree.

Nodes with a degree of 0 necessarily had links to chemicals or higher-order processes that were removed in Step 1. They
are interesting because there is not yet mechanistic information linking them to other genes and proteins that have
been curated in the context of the network. Nodes with a degree of 1 or more have an increasing amount of information,
and can be ranked such that the lowest degrees are prioritized for curation.

3. Filter Low-Information Nodes
-------------------------------
Some of the nodes with low information have already been quantified mechanistically, but just not in the given
knowledge assembly. In this step, several sources (Pathway Commons, Bio2BEL, etc.) are used to enrich these
nodes to determine if they have already been curated. Those that are found in other sources are also excluded
from curation.

4. Curation
-----------
Several steps can be taken to curate content after prioritizing genes.

1. `Curation with INDRA <https://github.com/pharmacome/curation/blob/master/indra.rst>`_
2. Manual search of literature for full-text. Eventually, storing the resulting PDFs in
   services like Mendeley will result in good automatic recommendations. Curation and
   `re-curation <https://github.com/pharmacome/curation/blob/master/recuration.rst>`_
   can be done on prioritized papers.
