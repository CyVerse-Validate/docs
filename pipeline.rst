Setup Stampede2 and run PipelineAgavePy
=======================================

This tutorial assumes that you have set up accounts with TACC and Cyverse and be assigned to a project allocation.

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

Using the Validate Pipeline
---------------------------

+ Move to PipeDevel directory. Use the standard tools cd, pwd, and ls to navigate_ on Stampede from the command line. If you've just completed the previous steps, simply use:
::

  >$ cd PipeDevel

.. _navigate: http://www.westwind.com/reference/os-x/commandline/navigation.html


+ the command to initialize the pipeline requires several parameters. In addition to your Agave account infomation, you must specify if you want to run a simulation, what type of GWAS or GenSel tools to use, whether you need Winnow for further analysis, the type of data being used (PED, BED, TFAM), and where the data is located on the Discovery Environment.

+ A sample command line looks like this:
::

  - >$ -u *username* --password *password* -i \tp -f /dhbrand/My_Data -lmm True

This would instruct the script to run the TPED/TFAM files in the specified datastore directory through FaSt-LMM.

Full Parameters
---------------

.. csv-table:: Full Parameters
  :heaer: "Command", "Verbose," "Description"
  :widths: 15, 10, 30
  
  "-u", "--username *username*", "Username for Agave services"
  "-i", "--InFormat *\inputformat*", "Defines data input format. \tp for PED/MAP, \tb for BIM/BED/FAM, \tt for TPED/TFAM"
  "-f", "--folder *working_directory*", "Folder to be pipelined. This folder should contain all inputs as well as the known-truth file for the given dataset."
  "-l", "--fastlmm", "Run Fast-LMM"
  "-r", "--ridge", "Run Ridge"
  "-b", "--bayes", "Run BayesR"
  "-p", "--plink", "Run Plink"
  "-q", "--qxpak", "Run QxPak"
  "-g", "--gemma", "Run Gemma"

Modifying the wrapper
---------------------

Modifying pipeline.py
---------------------