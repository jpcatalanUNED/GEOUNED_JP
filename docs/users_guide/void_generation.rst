Void Generation
===============

Two innovative automatic void generation capabilities are included in GEOUNED: enclosures and envelopes. These capabilities are detailed in the next points.

1. User defined enclosures

Enclosures are CAD defined solids that are used as base to generate the void for the region covered by them instead 
of the usual bound box that cover the region of interest. 
The use of user defined enclosures allows to generate separated void regions inside the same model. 
This is useful to assign different materials to the void (e.g. different air composition between rooms) 
and for later user modifications of the geometry. 
In addition, enclosures can be nested making easy to give a hierarchical structure to the void. 
In summary, the use of user defined enclosures is a very useful capability to generate clean and structured voids.

Enclosures are defined directly in the CAD model with the component name enclosureX_Y_ where X is the number ID for 
the enclosure and Y is the enclosure on which the enclosure X depends (in the lowest level Y is 0). 
For example, enclosure1_0_ is enclosure 1 that has not any enclosure above him and enclosure2_1_ is enclosure 
number 2 that is under enclosure 1. 
There are no restrictions on the level of dependence on enclosures. 
Also, each enclosure should be completely inscribed inside the upper enclosure (part of one enclosure cannot be outside
 the upper enclosure). 

.. image:: /images/CADTreeEnclosures.png
   :alt: Example of a CAD tree with enclosures and envelopes with dedicated tags highlighted in red.
   :align: center
   :width: 50%

Enclosure solids can be defined anywhere in the CAD model tree. By default, the void cells corresponding to each enclosure are written in the MCNP output file after all the solid definition independently of their position in the CAD model tree. The order of enclosures in the output file is the same order (top to bottom) they appear in the CAD model tree. The last void cells to be written in the output file are the level 0 voids, that means outside of any enclosure.

If the parameters option sortEnclosure is True, then the voids of the enclosures will be written in the output file in between the solid cell definition. They will be written in the same order they appear in the CAD model tree independently if there are solid cells defined before or after the enclosure solid.    

2. Envelopes

In some cases, the extraction of a region from void generation can be useful to generate more optimized MCNP models. For example, if a region of the space is full of other components, an envelope solid covering this region (frequently simpler than the components that it covers) can be defined in the CAD model. This envelope will be used during the void generation to ignore all the components inside itself (only components completely inside the envelope will be avoided in the void generation process). This should produce a simpler void definition. In counterpart, the user should be sure that the region covered by the envelope is clean (i.e. no lost particles) and full.  
Envelopes follow the same nomenclature that enclosures with ‘envelope’ text instead of ‘enclosure’. Dependency has no sense in this case as the higher level is the one to be used in the void generation process.
