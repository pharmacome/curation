Cookbook
========
Post-Translational Modifications
--------------------------------
The control of post-translational modifications can be represented in two ways in BEL:

.. code-block::

	# mechanistic representation with a reaction
	p(X) -> reaction(reactants(p(Y)), products(p(Y, pmod(Ph))))

	# qualitative representation
	p(X) -> p(Y, pmod(Ph))

The qualitative representation is preferred, also with other modifications like truncations and fragmentations.
