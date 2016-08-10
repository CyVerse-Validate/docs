****************************************
Generating Simulation Data with Alphasim
****************************************

Running Alphasim through Agave
------------------------------

** Estimated Time ~30min **

**Prerequisites:** Agave CLI, general knowledge of executing using Agave, Access to Cyverse data store, and Stampede allocation (if you want).

**Helpful Documentation**

* Alphasim: http://www.alphagenes.roslin.ed.ac.uk/wp-content/uploads/AlphaSimManual/AlphaSim.html

* Alphasim parameter file: https://github.com/CyVerse-Validate/Stampede-Files/blob/master/AlphaSim-1.04/AlphaSimInputInformation.txt

**Locate / Open parameter file**

* You can download a sample parameter files from `our repository <https://raw.githubusercontent.com/CyVerse-Validate/Stampede-Files/master/AlphaSim-1.04/AlphaSimSpec.txt>`_. The parameter file allows you to pass commands into the AlphaSim software.

*  Once you have access the parameter file upload it to your Data Store. The default parameter file has specifications for running multiple generations for corn genetics.

* Save the following as a JSON file (This can be save locally as long as you have the Agave CLI installed) with usename replaced with your CyVerse username And the path to the file to the parameter file within your Data Store.

::

  {
    "jobName": "testAlphaSim",
    "softwareName": "AlphaSim-1.04",
    "requestedTime": "05:00:00",
    "archive": true,
    "inputs":{
      "specificationFile": "agave://data.iplantcollaborative.org/USERNAME/ALPHASIM_SPEC_PATH"
            }
      }

* With the following command you can run AlphaSim (publicly available on Agave). This is assuming that you don't want to change any of the parameters::

  jobs-submit -F (path to json file)

* After submiting your job there will be a returned message which will list your job-id - This is helpful for looking up status and downloading output later

* The command::

  job-status [withyourjobid]

will allow you to see when your job will be done

* Once this finishes this will save onto your Data Store, if Archive is set to true, under Archive/Jobs in your personal DE folder.

* If you are okay with these outputs they are now useable, you can also option to convert to pedmap (which is a more standard format) using the merger application found in https://github.com/CyVerse-Validate/Validate/tree/master/CurrentReleaseStable/Util_1/Merger

* You can download your outputs from jobs with the general command::

  jobs-output --download --path [FilePath in the Data Store] [JOBID]

* You will download your outputs to your local computer from the Data Store with the following commands::

  jobs-output --download --path AlphaSim/Selection/SelectionFolder1/SnpSolutions.txt [yourjobid]
  jobs-output --download --path AlphaSim/SimulatedData/Gender.txt [yourjobid]
  jobs-output --download --path AlphaSim/SimulatedData/PedigreeTbvTdvTpv.txt [yourjobid]
  jobs-output --download --path AlphaSim/SimulatedData/AllIndividualSnpChips/Chip1Genotype.txt [yourjobid]
  jobs-output --download --path AlphaSim/Chromosomes/Chromosome1/Chip1SnpInformation.txt [yourjobid]

* Download the merger.py from the github repository here https://github.com/CyVerse-Validate/Validate/tree/master/CurrentReleaseStable/Util_1/Merger

* Then you can run the merger with the AlphaSim outputs with the following commands (this will convert your outputs to PED/MAP::

  python Merge.py --output ASimExampleOutputPrefix alphasim --snp Chip1SnpInformation.txt --pedigree PedigreeTbvTdvTpv.txt --gender Gender.txt --geno Chip1Genotype.txt --sol SnpSolutions.txt

This will yield ASimExampleOutputPrefix.ped and ASimExampleOutputPrefix.map in the directory specified in your above output flag.
