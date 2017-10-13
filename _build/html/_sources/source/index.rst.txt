**Validation is an evolving process and the documentation should reflect the experiences of users as they discover new and useful bits of information.**
:ref:`updating` is easy, and you can share comments and questions `at this forum <https://github.com/cyverse-validate/docs/issues>`_.

Validate 1.2
============

Validation is the positive control for your experimental data
analysis. You have control over how long data analysis
takes. Completing your positive controls first allows you to be ready
for your data when you get it. Why validate a particular data
analysis?

- Trust but verify: check that a widely used method will work for your data.
- Have analysis pipeline optimized; the moment you've collected all
  your data you can start the analysis (saving weeks or months to
  complete afterwards)
- Fewer requests from reviewers for changes to your data analysis
  methods
- Be confident you are doing the best possible data analysis

The CyVerse Validate workflow is versatile enough to handle you
importing your GWAS tools, functions, or simulation methods to use in
conjunction with the existing software. Speaking of imports, Validate
is capable of handling a range of file formats, and each piece of
software is very customizable. You have multiple options for adjusting
your output each step of the way.

Finally, since the analysis are run on the NSF-supported national
XSEDE computer systems, scalability of simulations is a non-issue; the
computational demand for your simulations will scale up as your needs
increase. All of your necessary files may be uploaded and accessed
from the CyVerse Data Store.

Version 1.2 Features
--------------------

- Added python scripts to streamline common tasks and open new options for scaling and automation.

Version 1.0 Features
---------------------

Version 1.0 features include:

- The ability to test prediction
- Incorporate the following prediction applications: GenSel, BayesR,
  BLR/BATools, ridge regression
- Updated Demonstrate to handle prediction graphics
- Managing GWAS and prediction applications in parallel
- Incorporate D. Hand's H-measure to the current performance metrics
- Additional documentation to onboard new developers and statisticians

Documentation
-------------

.. toctree::
   :maxdepth: 3

    Useful Terms <terms.rst>
    Quickstart Guide <quickstart.rst>
    Citations & Resources <citations.rst>
    Further Development & Getting help <develop.rst>
    Setting up the Validate Pipeineline <pipeline.rst>
    Comments & Discussion <notes.rst>