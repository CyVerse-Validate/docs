*****************
Prediction Tools
*****************

BayesR
======

**Speed Test Results**

Our BayesR speed test on a third of the syngenta data set on the Cyverse Data store completed successfully in 22 hours and 25 minutes, running 333 jobs on 64 nodes, two processes per node.


Running BayesR through Agave
-----------------------------

From your local machine, create a folder for the output and cd into it::

  mkdir outputfolder
  cd outputfolder

Download the BayesR job skeleton::

  wget https://github.com/CyVerse-Validate/Stampede-Files/raw/master/json/bayesR-job.json

Open this with a text editor and edit the following parameters:

a. For jobName, anything will work. For this example, I used testBayesR

b. For software name, enter “bayesR-2.00u1”

c. For requested time, enter “02:00:00”

d. For inputBED enter “agave://data.iplantcollaborative.org/username/folder/simdata.bed”, replacing
username and folder with your own. For instance, mine would be: “agave://data.iplantcollaborative.org/swb5075/BayesRData/simdata.bed” and
repeat this for the other two input files (BIM and FAM files)

e. For output, anything will work. I will use “BayesRTesting”. Save and close this
file.

Note: You can copy and paste this into a website like http://jsonlint.com/ to ensure that the JSON file is formatted correctly.

Using your local terminal, make sure you are in the same directory as the job.json file.

Enter::

  jobs-submit –F bayesR-job.json.

You should get a response: “Successfully submitted job . The sample data takes about twenty minutes to run but you can check this by entering: jobs-status with the same job ID as above. Once the job is complete, the response to this command will be “FINISHED”

We now want to download the output data. You can enter jobs-output-list to
see all of the included files. For instance I may enter::

  jobs-output-list 3895995830152073701-ee4acae9fffff7a7-0001-007

BayesR has six output files (.frq, .gv, .hyp, .log, .model, .param files) which begin with
the output parameter from the job json file. In my case, testresults.

In order to download, for example, the frequency file enter::

  jobs-output --download -- path testresults.frq 3895995830152073701-ee4acae9fffff7a7-0001-007

Here the --path parameter refers to which file you want to download and the long string
at the end is your job ID.

GenSel
======

Running GenSel through Agave
-----------------------------

**Estimated Time ~30min**

**Prerequisities:** Agave CLI, general knowledge of executing using Agave, Access to the Cyverse data store, and Stampede allocation (if you want)

**Helpful Documentation**

* Gensel (User Manual) http://www.biomedcentral.com/content/supplementary/1471-2105-12-186-s1.pdf

* Gensel (Cyverse page) https://pods.iplantcollaborative.org/wiki/display/DEapps/GenSel

**Locating the parameter/input files and running Gensel:**

To run the software you need one parameter file (.inp) and three input files (.gs, .newbin, .192).

* All of these files can be found in the Data Store following the path iplant/home/shared/iplantcollaborative/example_data/gensel/

* For more information on these inputs read the documentation listed above

1. Save the following as a JSON file (This can be save locally as long as you have the Agave CLI installed)

::

  {
    "jobName": "testGenSel",
    "softwareName": "GenSel-2.14",
    "nodeCount": 1,
    "batchQueue": "serial",
    "requestedTime": "02:00:00",
    "processorsPerNode": 16,
    "archive": false,
    "archivePath": "",
    "inputs":{
    "phenotypeFileName":"agave://http://datacommons.cyverse.org/browse/iplant/home/shared/iplantcollaborative/example_data/gensel/DMI.gs",
    "markerFileName":"agave://http://datacommons.cyverse.org/browse/iplant/home/shared/iplantcollaborative/example_data/gensel/gpegeno.newbin",
    "includeFileName":"agave://http://datacommons.cyverse.org/browse/iplant/home/shared/iplantcollaborative/example_data/gensel/DMIg.192"
    },
    "parameters":{
    "Parameter_File":"agave://http://datacommons.cyverse.org/browse/iplant/home/shared/iplantcollaborative/example_data/gensel/run.inp"
    }
  }

2. With the following command you can run Gensel (publicly available on Agave) This is assuming that you don't want to change any of the parameters/inputs listed in the sample json file.

::

  jobs-submit -F (your path the JSON file you just saved)

RidgePredict
======

Running RidgePredict through Agave
-----------------------------

**Estimated Time ~15min**

**Prerequisities:** Agave CLI, general knowledge of executing using Agave, Access to the Cyverse data store, and Stampede allocation (if you want)

**Helpful Documentation**

* The RidgePredict app uses Ridge Regression based on the SciKitLearn Ridge package: http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html

**Locating the parameter/input files and running RidgePredict:**

To run the software you need one .ped parameter file, for example: agave://http://datacommons.cyverse.org/browse/iplant/home/shared/syngenta_sim/Dong_Wang_sim/Analysis_Files/dongwang.ped
You only need one parameter, which will be the name you wish to have for your output.

1. Save the following as a JSON file and modify to your needs:

::

  {
    "jobName": "ridge-test-1",
    "softwareName": "RidgePredict-1.1",
    "processorsPerNode": 16,
    "requestedTime": "01:00:00",
    "memoryPerNode": 32,
    "nodeCount": 1,
    "batchQueue": "serial",
    "archive": false,
    "archivePath": "",
    "inputs": {
        "inputPed": "agave://http://datacommons.cyverse.org/browse/iplant/home/shared/syngenta_sim/Dong_Wang_sim/Analysis_Files/dongwang.ped"
    },
    "parameters":{
        "outputPed": "ridge-test-output.ped"
    }
  }

