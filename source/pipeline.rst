********************
Running the pipeline
********************

The Validate Pipeline represents our latest efforts to to simplify high-speed GWAS computing in the XSEDE cloud. While advanced users may wish to refer to the workflow overview for running custom applications, the pipeline includes scripts and wrappers for several common tools you can get started with right away.

A typical remote session on Stampede consists of several steps:
-Set up Agave CLI tools on Stampede
-create JSON files for job submission
-submit jobs
-retrieve results
-repeat to analyze outputs in other GWAS tools, validation, or visualization

The Validate Pipeline handles job submission and data management for you, automatically submitting jobs, monitoring their progress, and moving the results into your datastore. Automation of these steps makes it feasible to run multiple iterations of your analysis through multi-step workflows with considerably less user input. Researchers will enjoy fewer hours spent watching job queues, and users with extensive data requirements may be able to run customized workflows that would be unfeasible for a single user to submit and manage “by hand.”

What you’ll need:
-Accounts w/ Cyverse & TACC
-SSH client application
-Stampede allocation
-Data to be tested uploaded to the Data Store
-Validate Pipeline directory available on github

=======================================
Setup Stampede2 and run PipelineAgavePy
=======================================

This tutorial assumes that you have set up accounts with TACC and Cyverse and be assigned to a project allocation.

--------------------
Install Validate 1.2
--------------------

**(initial step: SSH into Stampede2 with your client of choice)**

+ Your Stampede2 home directory supports up to 10GB of data, while your work directory allows for up to 1TB. Use the alias command "cdw" and "cdh" to switch been your work and home directories, respctively::

  >$ cdw

+ Create a virtual environment to install the agavepy package with pip. See virtualenv_ for more information. **is this necessary or just good practice?**
  ::

  >$ virtualenv Validate1.2

.. _virtualenv: http://docs.python-guide.org/en/latest/dev/virtualenvs/

+ Change to new environment directory.
  ::

  >$ cd Validate1.2

+ We need to use our new environment.
  ::

  >$ source bin/activate

+ Next we need to install the packages required to run the Pipeline.
  ::

  >$ pip install agavepy numpy pandas statsmodels scipy

+ Finally we need to clone the repo from Github that contains the Pipeline.
  ::

  >$ git clone https://github.com/CyVerse-Validate/Validate.git

You now should be setup to run the pipeline.

+ Move to PipeDevel directory. Use the standard tools cd, pwd, and ls to navigate_ on Stampede from the command line. If you've just completed the previous steps, simply use:
  ::

  >$ cd PipeDevel

.. _navigate: http://www.westwind.com/reference/os-x/commandline/navigation.html


+ the command to initialize the pipeline requires several parameters. In addition to your Agave account infomation, you must specify if you want to run a simulation, what type of GWAS or GenSel tools to use, whether you need Winnow for further analysis, the type of data being used (PED, BED, TFAM), and where the data is located on the Discovery Environment.

+ A sample command line looks like this:
  ::

  - >$ python PipelineAgavePy.py -u *username* --password *password* -i \tp -f /username/My_Data -lmm True

This would instruct the script to run the TPED/TFAM files in the specified datastore directory through FaSt-LMM.

---------------
Full Meta-Parameters
---------------

.. csv-table:: Full Meta-Parameters
  :header: "Command", "Verbose," "Description"
  :widths: 15, 10, 30

  "-u", "--username *username*", "Username for Agave services."
  "", "--password", "Password used for Agave services."
  "-i", "--InFormat *inputformat*", "Defines data input format. p for PED/MAP, b for BIM/BED/FAM, t for TPED/TFAM."
  "-f", "--Folder *working_directory*", "Folder to be pipelined. This folder should contain all inputs as well as the known-truth file for the given dataset."
  "-pno", "--pheno *filename*", "Name (including extension) for the covariate file for the given dataset."
  "-lmm", "--fastlmm", "Run Fast-LMM"
  "-rdg", "--ridge", "Run Ridge."
  "-bay", "--bayes", "Run BayesR."
  "-plk", "--plink", "Run Plink."
  "-qxp", "--qxpak", "Run QxPak."
  "-gma", "--gemma", "Run Gemma."
  "-pma", "--puma", "Run Puma."


---------------------
Modifying JSON Parameters
---------------------

While the default settings should be adequate for most tasks, you may need to edit the python script with custom JSON settings if your jobs require additional processing or are timing out. This is handled in Validate/JsonBuilder.py. By editing this python file, you can easily alter the requested time for each app in the workflow. Simply change the value for “requestedTime” to a value that meets your needs.

---------------
Data Management
---------------
