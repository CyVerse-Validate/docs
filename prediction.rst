*****************
Prediction Tools
*****************

BeyesR
======

Running BayesR through Agave
-----------------------------

From your local machine, create a folder for the output and cd into it::

  mkdir outputfolder
  cd outputfolder

Download the BayesR job skeleton::

  wget https://github.com/CyVerse-Validate/Stampede-Files/raw/master/json/bayesR-job.json

Open this with a text editor and edit the following parameters:

a. For jobName, anything will work. For this example, I used testBayesR

b. For software name, enter “bayesR-0.75”

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
