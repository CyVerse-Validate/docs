****************************
Submitting jobs on Stampede
****************************

You have two alternatives for running your tools on Stampede. The Agave API allows you to :ref:`jobs` as outlined in our quickstart guide.

For further reference see:

- http://agaveapi.co/what-is-a-job2/
- http://agaveapi.co/documentation/tutorials/job-management-tutorial/

You can also use Stampede's parametric launcher to distribute your work across multiple nodes. For large jobs, this has tangible speed benefits & is in general a more secure & efficient computing practice. The TACC guide for the parametric launcher can be found at the link below, or scroll down for our quick-start tutorial.

- https://www.tacc.utexas.edu/research-development/tacc-software/the-launcher

Parametric Launcher
====================

Running multiple jobs through the launcher on Stampede
------------------------------------------------------

**Prerequisities:** Agave CLI, general knowledge of executing using Agave, Access to the Cyverse data store, and Stampede allocation

**Job Format:**

When you start a job using the parametric launcher, it will always look for a parameter file in your current working directory titled "paramlist". The first step is to put together this file and store it where you want to run your job from. Below is an example of a paramlist for the prediction app bayesR. You can see that it is simply a list of commands to run the bayesR application with the specified inputs and outputs.

::

/home1/04109/ksierrac/applications/bayesR-master/bin/bayesR -bfile /work/04109/ksierrac/bayes_speedtest/data/AlphaSim_1 -out /work/04109/ksierrac/bayes_speedtest/alpha_output/AlphaSim_1_out;
/home1/04109/ksierrac/applications/bayesR-master/bin/bayesR -bfile /work/04109/ksierrac/bayes_speedtest/data/AlphaSim_2 -out /work/04109/ksierrac/bayes_speedtest/alpha_output/AlphaSim_2_out;
/home1/04109/ksierrac/applications/bayesR-master/bin/bayesR -bfile /work/04109/ksierrac/bayes_speedtest/data/AlphaSim_3 -out /work/04109/ksierrac/bayes_speedtest/alpha_output/AlphaSim_3_out;
/home1/04109/ksierrac/applications/bayesR-master/bin/bayesR -bfile /work/04109/ksierrac/bayes_speedtest/data/AlphaSim_4 -out /work/04109/ksierrac/bayes_speedtest/alpha_output/AlphaSim_4_out;

The advantage of using the launcher in this situation is that all you have to do is to build the paramlist file. Once you submit, the launcher will automatically submit these multiple jobs for you.

**To run these jobs through parametric launcher**

* To run the above example, you would use this command:
    ::
    sbatch -N 64 -n 128 -t 48:00:00 $TACC_LAUNCHER_DIR/launcher.slurm

* The submit command is "sbatch", the same as submitting a single job to Stampede. Call the launcher by adding "$TACC_LAUNCHER_DIR/launcher.slurm" at the end of your command.

(Note: If you have not loaded the launcher module, first run the command "module load launcher" followed by "module save")

* -N specifies number of nodes, -n specifies number of processes running at once, and -t specifies the allowed time for the jobs to run. For a full list of possible flags, see this link: https://portal.tacc.utexas.edu/user-guides/stampede#tablesbatchoptions
