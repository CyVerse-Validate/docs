Dependency Trouble for Sphinx (GWAS tool)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The below diagram details the problem I encountered while downloading Sphinx on my Stampede allocation.

.. image:: depend.png
   :height: 100px
   :width: 200 px
   :scale: 50 %
   :alt: alternate text


As you see from the above picture, the white boxes were the original instructions in the README text for SPHINX. The dependency I could not get downloaded and installed was the PFunc_ library.

.. _PFunc: https://projects.coin-or.org/PFunc

To get the other 6 libraries loaded into your cuurent environment enter the following code:

::
   module load gcc/4.7.1
   module load gcc/4.9.1
   module load gcc/4.9.3
   module load intel/13.0.2.146
   module load referencelapack/3.5.0
   module load boost/1.55.0

Problems Running PFunc
++++++++++++++++++++++

The PFunc README says to create a folder called "pfunc-install" and after running through the directions, and the cmake command (which I think is the command that will be compiling the files into a binary) the folder is still empty.


::
   /work/03813/ddc/iPlant/src/PFunc-0.1.1
   /work/03813/ddc/iPlant/pfunc-install

Here is the installation guide written in the PFunc folder which has last been updated 7 years ago as of today.

::
   Basic Installation:
   -------------------
   For a clean installation process, we recommend an out-of-source build. However,
   the in-source build works just as well. Given below are the basic installation
   instructions for PFunc on Linux/OS X/AIX:

   a) Get a copy of PFunc. For the sake of this installation guide, let us 
      assume that PFunc's sources have been checked out in the directory
      "pfunc". Furthermore, let us assume that the absolute path is 
      "/home/anon/pfunc". 

      b) #cd /home/anon/ && mkdir pfunc-build
	 
	 At the end of this step, we have the following directories:
   i) "/home/anon/pfunc"
   ii) "/home/anon/pfunc-build"

       c) #cd /home/anon/pfunc-build

	  d) #cmake /home/anon/pfunc \
	     -DCMAKE_INSTALL_PREFIX=/home/anon/pfunc-install

	     
Step above says to specify in the make command a folder called "pfunc-install" but the above instructions only mentioned created a folder "pfunc-build", so after trying multiple times with the install, I used the second folder in the make command:::
::
  
  cmake /work/03813/ddc/iPlant/src/PFunc-0.1.1/pfunc -DCMAKE_INSTALL_PREFIX=/work/03813/ddc/iPlant/PFunc-0.1.1/pfunc-build

Going back to the installation guide:


::
	     At this step, we are configuring PFunc and have choosen to install the 
	     files in the local directory. Once configuration is done, the following 
	     targets are available to be built by the native build-system.
	     i) "pfunc" -> builds the static library "libpfunc.a"
		ii) "tutorial" -> builds the tutorial if BUILD_TUTORIAL was ON.
		    iii) "doc" -> build documentation if BUILD_DOCS was ON.
			 iv) "all" -> builds all the selected targets.
			     v) "clean" -> removes all the object files.
				vi) "install" -> installs the targets to the selected prefix.
				    vii) "uninstall" -> does the obvious.
					 viii) "examples" -> builds examples if BUILD_EXAMPLES was ON.

					       e) #make <target-name>
						  
						  At this stage, we can build any of the targets mentioned in (e).


First off, the directions cut off after this sentence into a new section. Secondly, there are no targets mentioned in this text, so I'm not sure what I'm tryinig to do with this step.						  
