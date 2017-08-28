Documentation Notes & Discussion
--------------------------------

Some suggestions for the documentation:
=======================================

+ Some overview of the workflow is needed. E.g. where the jobs are run, where the output is put, and then why you need to download it, and then upload it again to run winnow.

*With the pipeline this will no longer be a problem. Users will give their Cyverse login info at the beginning and the pipeline will automatically access the users Discovery Environment. Jobs are run on Stampede2 using Agave. The output from the job is stored on the users DE. There will be an option to run Winnow in the initial command. Winnow output will be created and placed in a different directory in the user's DE.*

+ Under “Configure Job Submission” it would be useful to have some general background, for example what the job is going to do. What is FastLMM and what kinds of inputs does it need? It isn’t clear from the json how to direct the results from a job to a particular place or folder. Some details on where the output is going would be informative. In the past I’ve only written submission scripts with command line arguments - could you add an example of a command line argument and how it would look in the json?

+ Under “Submit Job” is there a way to access your current or previous job ids?
*All of the jobs that are submitted are tied to the user's Agave login (i.e. Cyverse login) information. The default JSON's from Validation 1.0 were using the directory "archive" on the DE to store all the job and it was listed by Job ID. Michael is working on each job going into a directory based on the type of analysis submitted (i.e. all simulations in one directory, all GWAS in another directory, GenSel another, Winnow another, etc.) and then each of those jobs will have a dated name. So if a user needed to go looked at a job they could access the information through the DE. An alternative would be to use the Agave ToGo website as it also*

+ “Run more GWAS / Prediction Apps for comparision” (note “comparision” is spelled wrong). It would be good to have some json examples that work for each of these programs. It would also be good to have links to the publications and webpages to each of the programs.

+ “Send Output Files to Winnow” Some background is needed on Winnow and what it does. The link is also not very helpful. What format should the “known truth” file be in? What are the fit statistics that it calculates and how are they calculated? What does Results.txt look like? Some people, like me, probably won’t use Winnow because we have some other stats and analysis that we’d like to run. It might be worth stating that this is optional.

+ “Demonstrate” section - It seems like this package requires a very specific type of input directory. It would be good to have some more information/examples on the inputs, and some examples of the outputs. How are multiple programs visualized and compared?
[8:55] (Note that answers to some of my questions are found in other places in the docs, but links and more info just need to be added to the quickstart guide)