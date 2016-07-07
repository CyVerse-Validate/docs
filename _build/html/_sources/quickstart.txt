*****************************
Getting Started with Validate
*****************************

It's helpful to think of Validate not as a single app (Winnow) but as a multi-stage workflow. A typical session will involve either generating a sample data set or importing your own from the CyVerse Data Store for analysis with your preferred GWAS or prediction tool. The corresponding outputs are then analyzed with Winnow, and rendered with Demonstrate. 

These quick start tutorials assume basic command-line knowledge. While the guides assume you have access to a Cyverse account and Stampede Allocation (`see here [accounts.rst]` for account setup information), these instructions should be easily adapted to run Validate on your own hardware. 

.. toctree::
    :maxdepth: 2
   
    Tutorial for running Validate with sample data set <syngenta_tut.rst>
    Generating a sample data set with Alphasim <alphasim.rst>
    SLURM/JSON job submission guide <json.rst>
    GWAS Tools <gwas.rst>
    Prediction <prediction.rst>
    

Resources
=========
    
Alphasim home page
Cyverse Agave CLI Guide

Getting Help
============

email stapletonlab@gmail.com
post on the Slack
