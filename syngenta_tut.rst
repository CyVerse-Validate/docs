**********************************************
Running Validate on Syngenta_heldback data set
**********************************************
--------------------------
Install Cyverse CLI tools
--------------------------

Accessing Validate through the Agave API hugely streamlines the task of managing your data and accessing applications through the Cyverse Data Store with a variety of command-line tools. For a comprehensive overview please see the `full documentation  <https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk>`_.

Download Agave API::

    git clone https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk.git

Change directory into the downloaded repository and unpack the cli tools::

    cd cyverse-sdk
    tar xf cyverse-cli.tgz

Add the cli tools to your home directory and bash profile::

    mv cyverse-cli $HOME
    echo "PATH=\$PATH:\$HOME/cyverse-cli/bin" >> ~/.bashrc
    source ~/.bashrc

(note that on a Macintosh system your default profile may be .bash_profile)

Initialise the CLI tools::

    tenants-init -t iplantc.org

Create an OAAuth client application with API keys::

    clients-create -S -v -N my_client -D "Client used for app development"

Where -S saves the keys for future use, -D provides a brief description, and -N is your application name.

You will be asked to enter your CyVerse account information::

    auth-tokens-create -S

At this point::

    apps-list

should return a list of all publicly-available apps.


------------------------
Configure Job Submission
------------------------


download fastLMM job skeleton::

  wget https://github.com/CyVerse-Validate/Stampede-Files/json/fastlmm-job.json

(you may need to install wget if using a mac)


You can open fastlmm-job.json in your text editor of choice to go over your options::

    {
    "jobName": "FLMMDongWangFull",
    "softwareName": "FaST-LMM-hpc-2.07u1",
    "requestedTime": "02:00:00",
    "archive": true,
    "inputs":{
                "inputPED": "agave://data.iplantcollaborative.org/shared/syngenta_sim/Dong_Wang_sim/Analysis_Files/dongwang.ped",
                "inputMAP": "agave://data.iplantcollaborative.org/shared/syngenta_sim/Dong_Wang_sim/Analysis_Files/dongwang.map",
                "inputPHENO": "agave://data.iplantcollaborative.org/shared/syngenta_sim/Dong_Wang_sim/Analysis_Files/dongwangpheno.txt"
             },
    "parameters":{
        "output": "full_results"
                    }
    }


These parameters should be fairly self-explanatory but are defined in detail `on this page <https://agaveapi.co/documentation/tutorials/job-management-tutorial>`_

Inputs must be specified based on the app you're running-- ensure the file format is correct! Refer to individual app's documentation for more information. In this tutorial we are accessing PED, MAP and phenotype files from the public syngenta_sim dataset.

To access your own data from the Discovery Environment, change the url to replace "/shared/" with the path to your user account; ie::

    "agave://data.iplantcollaborative.org/yourusername/results/yourdata.ped",

----------
Submit Job
----------

from the working directory where the .json file is located, type::

    jobs-submit -F fastlmm-job.json

If successful you should soon see::

    Job [job_id] successfully submitted

Copy down the job_id. You'll use it to check the status of your job with::

    jobs-status *jobid*

Once your job is complete, you can view the outputs with::

    jobs-output *jobid*

And download selected outputs with::

    jobs-output --download --path *filename* *jobid*


----------------------------
Send Output Files to Winnow
----------------------------

For full inputs & outputs see `here <https://github.com/gpcarpen/Quickstart-guide/blob/master/docs/Winnow.md>`_

The required files for winnow are the Known Truth file and the output from a GWAS tool (FastLMM in our case)

Once you download the fastlmm output, upload it to a new location in your DE::

    files-upload -S data.iplantcollaborative.org -F *fastlmm output which should now be local* yourusername/yourdatafolder

Download the winnow example skeleton::

  wget https://github.com/CyVerse-Validate/Stampede-Files/json/winnow-job.json

You can edit and submit this file using the same process described above.

----------------------------------
Visualize Results with Demonstrate
----------------------------------


Demonstrate is the final step in the Validate known-truth pipeline for iPlant Collaborative. Using output from Winnow, it produces a set of graphics showing differences in a GWAS/QTL applications performance under varying heritability and population structure. Demonstrate also functions without the need for heritability or population structure, but different graphics will be produced in that case.

The function you will want to use depends on what type of data you have:

Data with Heritability and Population Structure Specified
---------------------------------------------------------

If you want to visualize differences in your data based on heritability or population structure, you'll want to use the original function Demonstrate. To run Demonstrate, type R on your terminal or command line to open the R console. From there use::

  library(Demonstrate)

If nothing happens, then you did it correctly! Now the Demonstrate package is loaded. Here are the options to run the function::

  Demonstrate(dir, make.AUC.plot=TRUE, AUC.plot.title="Mean AUC By Population Structure and Heritability", make.MAE.plot=TRUE, MAE.plot.title="Mean MAE By Population Structure and Heritability",herit.strings=list("_03_","_04_","_06_") ,herit.values=list(0.3,0.4,0.6),struct.strings=list("PheHasStruct","PheNPStruct"),struct.values=list(TRUE,FALSE))

In this function, dir represents the directory where all Winnow output is stored. These default values are based on the sample data found within this repository. Once run, the function will create two graphs on the mean absolute error (MAE) and area under the receiver operator curve (AUC) across varying levels of heritability and/or population structure. The graphs are in pdf format.

Other data from Winnow
-----------------------

For other types of data, or if you're more interested in comparing GWAS tools than comparing data, you will want to use the Demonstrate2 function. Before running it though, you will need to include the function in your global environment::

  source("<path to>/Demonstrate2.R")

Then run the function::

  Demonstrate2(dir, make.pos.plot=TRUE, pos.plot.title="True Positives by False Positives", make.error.plot=TRUE, error.plot.title="Plot of AUC by MAE", extra.plots=TRUE, AUC.axis.min=0, AUC.axis.max=1.0, MAE.axis.min=0, MAE.axis.max=2.0)

Assuming all outputs are kept, Demonstrate2 will output five files in total. First, two frequency histograms illustrating the distribution of both true and false positives (if multiple Winnow files were in the original directory, the pdf files will have multiple pages). Second, a .csv file detailing the average sensitivity, specificity, and precision of each
file. Finally, two plots based on true vs. false positives and mean absolute error vs. area under the curve will be produced. Demonstrate2 will color the points based on the file they came from, so you can compare multiple GWAS analysis results on the same plot.
