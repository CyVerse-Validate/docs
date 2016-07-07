**********************************************
Running Validate on Syngenta_heldback data set
**********************************************
--------------------------
Install Cyverse CLI tools
--------------------------

Accessing Validate through the Agave API hugely streamlines the task of managing your data and accessing applications through the Cyverse Data Store with a variety of command-line tools. For a comprehensive overview please see the full documentation `here <https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk>`_.

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
configure job submission
------------------------


download fastLMM job skeleton::

    wget https://www.dropbox.com/s/ij43c5qwsk6hakf/fastlmm-job.json

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
    

These parameters should be fairly self-explanatory and are defined in detail `on this page <https://agaveapi.co/documentation/tutorials/job-management-tutorial>`_

jobName is up to you

softwareName must be a valid Agave app

requestedTime is up to you

inputs must be specified based on the app you're running-- ensure the file format is correct! Refer to individual app's documentation for more information. In this tutorial we are accessing PED, MAP and phenotype files from the public syngenta_sim dataset.

To access your own data from the Discovery Environment, change the url to replace "/shared/" with the path to your user account; ie::
    
    "agave://data.iplantcollaborative.org/yourusername/results/yourdata.ped",

----------
submit job
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
Send output files to Winnow
----------------------------

The required files for winnow are the Known Truth file and the output from a GWAS tool (FastLMM in our case)

Once you download the fastlmm output, upload it to a new location in your DE::

    files-upload -S data.iplantcollaborative.org -F *fastlmm output which should now be local* yourusername/yourdatafolder

Download the winnow example skeleton::

    wget https://www.dropbox.com/s/pnhebgvx18mh6f5/winnow-job.json

You can edit and submit this file using the same process described above.
