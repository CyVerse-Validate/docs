*****************************
Getting Started with Validate
*****************************

It's helpful to think of Validate not as a single app (Winnow) but as a multi-stage workflow. A typical session will involve either generating a sample data set or importing your own from the CyVerse Data Store for analysis with your preferred GWAS or prediction tool. The corresponding outputs are then analyzed with Winnow, and rendered with Demonstrate.

These quick start tutorials assume basic command-line knowledge (start with the Software Carpentry `tutorial <http://swcarpentry.github.io/shell-novice/>`_ if you're new, or refer to this `cheat sheet <http://linoxide.com/guide/linux-cheat-sheet.png>`_ for a quick reference). While the guides assume you have access to a Cyverse account and Stampede Allocation, these instructions should be easily adapted to run Validate on your own hardware.

.. toctree::
    :maxdepth: 2

    Setting up your accounts <accounts.rst>
    Tutorial for running Validate with sample data set <syngenta_tut.rst>
    Generating a sample data set with Alphasim <alphasim.rst>
    SLURM/JSON job submission guide <json.rst>
    Accessing the Discovery Environment <discover_guide.rst>
    GWAS Tools <gwas.rst>
    Prediction <prediction.rst>
