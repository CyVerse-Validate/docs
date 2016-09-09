***********
GWAS Tools
***********


FastLMM
=======

The main genome wide association studies tool that we have used, FaST-LMM stands for Factored Spectrally Transformed Linear Mixed Models. It is a tool from Microsoft Research designed for analyses of very large data sets, and has been tested on data sets with over 120,000 individuals.

**Running the Program**

The easiest way to run fastlmm is through Agave, as it will interpret your json job file and compile the command for you. However, if you are interested in running fastlmm directly through SLURM, we provide documentation for that as well.

**Run through Agave**

To run fastlmm, you will need a phenotype file as well as a set of EITHER ped/map or bed/bim/fam data files. The example json below includes ped/map files from the syngenta data, and can be run as-is if you would like to test it before using your own data.

Here are all of the possible inputs that may be used in your job submission:
	* inputPHENO : (required) phenotype file corresponding to PLINK fileset
	* inputCOVAR : (optional) covariate file
* Choose one group of data inputs:	
	* inputTPED : TPED file for transposed PLINK set
	* inputTFAM : TFAM file for transposed PLINK set
	
	
	* inputPED : PED file for main PLINK set
	* inputMAP : MAP file for main PLINK set
	
	
	* inputBED : BED file for PLINK binary set
	* inputBIM : BIM file for PLINK binary set
	* inputFAM : FAM file for PLINK binary set
* Parameters:
	* output : (required) The name of the output file (without extension)
	* verboseOutput : (optional) Trigger for verbose mode, 1 if true, 0 if false
* Optional advanced parameters:
	* C : Trigger for whether covariate file is included (1 if true, 0 if false)
	* B : Set the binary PLINK fileset as the primary input (1 if true, 0 if false)
	* SimFileset : Specify the PLINK grouop used to calculate the genetic similarity matrix (PEDMAP, BEDBIMFAM, or TPEDTFAM)
	* mpheno : Proper column number for phenotype file (if multiple phenotypes are used)
	* T : Transposed PLINK fileset is the primary input (1 if true, 0 if false)
	
	
You can save this example json and modify it for your needs:

::

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

  
**Run directly through SLURM**

The program requires a minimum of three files to function: 1) A PEDMAP set of files, 2) a phenotype file corresponding to the PEDMAP set, and 3) a set of PLink formatted files to compute the genetic similarity matrix decomposition (does not need to be different from number 1).

The input flags you would use are as follows:

    * -file : Denotes the file name for the PLINK .ped/.map files
    * -bfile : Denotes the name for PLINK .bed/.bim/.fam files
    * -tfile : Denotes the name for PLINK .tped/.tfam files
    * -pheno : Denotes the name of the phenotype file (including extension)
    * -covar : Denotes the name of the covariate file (including file extension)
    * -out : The name of your final output file, which is placed into the same directory as your program and data unless otherwise specified

These are the bare minimum options needed to run FaST-LMM; however, some other options for considerations are:

    * -verboseOutput : use this flag to show more complex and detailed output; does not require a file to be named
    * -fileSim : The name of the PLINK set used for computing the genetic similarity matrix and its decomposition
    * -pValuePrintThreshold : Restricts the output file to only include SNPs with a p-value less than or equal to the specified threshold

An example of executing the FaST-LMM program might look like::

  fastlmmc -verboseOutput -bfile toydata -pheno toydata.phe.txt -covar toydata.covar.txt -out MyResults.csv
  

Puma
====

Puma (Penalized Unified Multiple-locus Association) "comprises a family of statistical methods designed to identify weak associations in genome-wide association studies that are not detectable by conventional analytical methods." Puma was developed by Jason Mezey at Cornell University, and we have installed it on Agave so that it is available for use.

Puma download (if you would like to install the software yourself rather than run through Agave) is available here: http://mezeylab.cb.bscb.cornell.edu/Software.aspx

Example data can be found here and uploaded to your data store for testing use with Agave:
https://github.com/CyVerse-Validate/Stampede-Files/tree/master/Puma/data

Here is an example JSON job file which you can save and modify for your own use:

::

  {
    "jobName": "puma-test-1",
    "softwareName": "Puma-1.0u1",
    "processorsPerNode": 16,
    "requestedTime": "01:00:00",
    "memoryPerNode": 32,
    "nodeCount": 1,
    "batchQueue": "serial",
    "archive": true,
    "archivePath": "",
    "inputs": {
        "tped": "agave://data.iplantcollaborative.org/PATHTODATA/DATA.tped",
        "tfam": "agave://data.iplantcollaborative.org/PATHTODATA/DATA.tfam"
    },
    "parameters":{
        "regression": "LINEAR",
        "penalty":"LASSO",
        "name":"try1"
    }
  }

These are all of the possible inputs you can specify for your job:

Inputs:
    * tped (required)          [genotype data in plink TPED format]
    * tfam  (required)         [phenotype (and sex) data in plink TFAM format]
    * sex            		   [if tfam is used, this includes sex as a covariate]
    * covariates     		   [file storing matrix with each column being a covariate]
    * regression (required)    [specify regression model as either LINEAR or LOGISTIC]
    * sma            		   [if set, performs only standard single marker analysis]
    * penalty (required)       [space delimited list of methods to run, select from:
							LASSO ALASSO LOG NEG MCP VBAY]
    * name (required)      	   [name to be appended to results files]

Advanced inputs:
    * screen_p_value [marginal p-values below which markers are passed to method]
		         (default = 0.01)
    * pML_restarts   [number of posterior modes explored]
		         (default = 100)
    * results        [specify folder where results are saved. Defaults to local folder]
    * nthreads       [number of threads used to run in parallel]
		         (default = machine default)
    * restrictedPathSearch [1 dimensional path search for non-convex penalties]

When you run the job, it will return a file of pvalues as well as an R results file. The best way to read this data is to use an R extraction program which will summarize the results for you:

* Download extract_puma_results.R and place a copy in the directory with your results file: https://github.com/CyVerse-Validate/Stampede-Files/blob/master/Puma/extract_puma_results.R)
* Modify the file with your results file name (example: "results_testjob_LASSO.R") in line 9: 
result = dget("FILENAME.R")
* Save extract_puma_results.R
* Start R and run these lines (where OUTPUTFILENAME is what you want your summarized results file to be called):

::

  sink('OUTPUTFILENAME.txt')
  print(source('extract_puma_results.R'))
  sink()

  
This will place the summarized results file in your working directory.
