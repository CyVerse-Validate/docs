******************
Useful Terms
******************


Depending on your specialty coming into the lab, you may not need all of the terms on this page. You may not need any! Either way feel free to skip to the relevant section for whatever information you may be lacking: Biology Terms, Statistics Terms, Computer Science Terms, next page.

Organizations
-------------

* Stampede: One of the most powerful supercomputers in the world, dedicated primarily for scientific computation.

* Cyverse: National life science consortium (previously known as iPlant). This organiztion has many functions and purposes but primarily seems to allow for ease of collaboration.

* TACC: Texas Advanced Computer Center (TACC). "The center's mission is to enable discoveries that advance science and society through the application of advanced computing technologies."

* Xsede: "Xsede is a single virtual system that scientists can use to interactively share computing resources, data and expertise."

* Agave: "Agave is an open source, platform-as-a-service solution for hybrid cloud computing. It provides a full suite of services covering everything from standards-based authentication and authorization to computational, data, and collaborative services."

Biology Terms
-------------

* Genotype: The set of genes an organism possesses.
* Phenotype: The physical characteristic of an organism. Though normally biologists refer to a collection of physical characteristics in defining phenotype, our typical studies limit the phenotype definition strictly to quantitative traits such as height or weight. Most tools only use one of these quantitative characteristics for analysis for the sake of consistency and for statistical accuracy, though other options for phenotype are entirely possible (e.g. binary options like disease/no disease).
* GWAS: Stands for _G_enome _W_ide _A_ssociation _S_tudies. Genome wide association studies examine variations in gene structure (genotypes) to see if these variations can be associated with certain physical traits or phenotypes. Because these studies involve entire genetic sequences, large sample sizes with a high number of individuals are required for success. The Stapleton Lab is focused largely on this area of research.
* SNP: Stands for _S_ingle _N_ucleotide _P_olymorphism.
* QTL: Stands for _Q_uantitative _T_rait _L_oci analysis.
* GxE: Stands for _G_enotype _E_nvironment interaction.

Statistics Terms
----------------

* Variable: As the name implies, a variable varies from object to object. To be specific, a variable is a symbol representing potentially any characteristic or object that can be either measured or counted. Some basic examples of variables (when dealing with people) might include eye color, height, or the number of pets one owns.
* Quantitative vs. Qualitative: A quantitative variable is a value that can be quantified, or measured and represented numerically. Height or weight are good examples of quantitative traits. Quantitative variables can be either discrete-only taking on a set number of values-or continuous-able to take on any value within a certain numerical range.
* Distribution: The description of the underlying observed or theoretical frequency of certain values occurring for a given variable. These frequencies, like the variables they describe, may be either discrete or continuous. Some well known discrete distributions include binomial and geometric. Continuous distributions include the normal distribution (AKA the "bell curve") and the gamma distribution.
* Hypothesis Testing: A statistical method for testing the probability of a given hypothesis being true. A hypothesis test deals with both a null hypothesis (the hypothesis being tested, generally says that findings are produced by chance) and an alternative hypothesis(a possible trend or hypothesis explaining the data formation, typically says that findings are the results of some difference or trend in data). The five steps of a hypothesis test are: 1) State hypotheses 2) Determine significance level to compare p-value against (usually 0.05) 3) Calculate test statistic (standardized value of your sample's attribute assuming the null hypothesis is true) 4) Calculate p-value 5) State the conclusion
* P-value: The value one refers to when making a final conclusion on certain statistical tests, particularly hypothesis tests. To be specific, a p-value is the probability of obtaining a certain sample (i.e. the sample chosen for the test) under the assumption that the null hypothesis is true. Since a p-value is a probability, it will always lie between 0 and 1. If a p-value is small, the probability of your findings being produced under the null hypothesis is small, meaning that the null hypothesis probably isn't true. Thus, if a p-value is below a specified significance level, the null hypothesis of your test may be rejected.
* Statistical Significance: Typically used when describing a hypothesis test for differences in samples,
* Correlation: The measurement of the strength and direction of a linear relationship between two quantitative variables. Correlation is typically indicated by the correlation coefficient statistic r, and this statistic can take any value from -1 to 1. A positive correlation (r value between 0 and 1) indicates that as one variable increases, the other tends to increase also. In contrast, a negative correlation (between -1 and 0) indicates that as one variable increases, the other tends to decrease. Note the keyword "tends" in the previous explanations. Correlations guarantee nothing with respect to increase or decrease of variable values. Furthermore, and this is an important point, correlation does not equal causation! Meaning that just because two variables are related does not mean that one necessarily causes another to increase or decrease.

Computer Science Terms
-----------------------

* Quality Control: The process of making sure software is working correctly. Quality Control typically includes a series of tests to measure software performance and/or ease of use. Developers and tester may have a certain set of standards that the tester may want the software to adhere to, or a list of criteria that the program must satisfy.
* Documentation: The necessary documents explaining how to use the software. Typically, documentation includes instructions for using each of the functions included and perhaps a tutorial for going through some of the main features of a given program.

*   Permissions: The authorization to read, write, or execute a program. Certain programs or files may not require access by everyone, so developers may set up permissions on their code such that only a certain group of people may use it freely. While certain permission barriers may be bypassed (e.g. through the "sudo" command on Linux or "Run as administrator" on Windows), permissions are usually set up for a reason, so it's best to just contact the developer if you need access to something blocked off.

* Github: A version-control website frequently used for collaboration on software design. Github allows for both public and private access to project repositories and keeps a history of different updates that users make to their programs. Anyone can make contributions to a public repository on Github. It also allows for you to set up webpages based on a project or organization and allows transfer of software permissions to other users or organizations.

* CLI: _c_ommand _l_ine _i_nterface (CLI). This is a way for a user to interact with a computer/application/etc. by way of the command line. (ex. old dos commands)

* GUI: _g_raphic _u_ser _i_nterface (GUI). This is a way for a user to interact with a computer/application/etc. by way of a graphic (ex. using microsoft word)

* API: _a_pplication _p_rogramming _i_nterface (API). A set of tools, resources, or routines which make developing applications on a given system easier. Following the logic from the two precedding definitions, API could be exaplined as the way in which interfacing happens when programming applications. For example, iPlant's Agave API allows for easier development of scientific apps on the Stampede supercomputer.

* Terminal: A portal for interacting with and recieving data from a computer.

* Auth-tokens: Authentication tokens are used as a kind of digital key which allow other computers to determine and verify user's identities.

* Node: (Within the context of the Stampede super computer) These are the speficic compute nodes which jobs are sent to.

* Allocation: (Within the context of this workflow) This a set amount of space that is given to you to run jobs on the stampede supercomputer

* iRODS: "The Integrated Rule-Oriented Data System (iRODS) is open source data management software for storing, searching, organizing, and sharing files and datasets that are large, important, and complex." Generally this is used so users can interact with the cyverse data store from their home computers.

* iCommands: A collection of commands to be used within IRODS for submitting or retrieving data from the data store.
