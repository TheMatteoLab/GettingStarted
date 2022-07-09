# ToDo
- [x] add useful links
- [ ] add links to important papers
- [x] add info on how to connect to the cluster and jupyterlab
- [ ] directory structure
- [ ] expand useful file locations
- [ ] create tutorials (on a separate repository?)

# Useful links
- [CAST website](https://admixgenomics.ucsd.edu/)
- [UKBB user site](https://bbams.ndph.ox.ac.uk/ams/researcher_home.jsp)
- [AllOfUs researcher workbench](https://workbench.researchallofus.org/login)
- [AllOfUs data browser](https://databrowser.researchallofus.org/)

## Reading
Coming soon.

# Getting started

Initially you should have a user account on the Frazer Lab cluster. In order to access the cluster from your home terminal:
```
ssh username@flh1.ucsd.edu
```
You should typically not work on the head node. After you have logged in, to navigate elsewhere:
```
qlogin
```
To request more memory/cores:
```
qlogin -pe smp 4 -l h_vmem=4G # request 4 cores (4 Gb/core)
```

## Connect to jupyterlab:
[jupyterlab](https://flh1.ucsd.edu:9000/user/username/lab)

To delete jupyterlab jobs (via command line):

1. Run qstat to find the job ID 
```
qstat
```

```
{
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID
-----------------------------------------------------------------------------------------------------------------
8803323 0.55617 jupyterhub username1    r     06/06/2022 11:37:43 juphigh.q@fl-n-1-10               16
8803325 0.55617 jupyterhub username2    r     06/06/2022 14:08:13 juphigh.q@fl-n-1-3                16
}
```

2. qdel your job ID
```
qdel 8803323
```

# Install software

Add software to `~./bashrc`:
```
export PATH=/frazer01/software/bcftools-1.9/bin:$PATH
export PATH=/frazer01/software/bedtools-2.27.1/bin:$PATH
export PATH=/frazer01/software/samtools-1.9/bin:$PATH
export PATH=/frazer0l/software/tabix-0.2.6/bin:$PATH
```

## miniconda 

From [these instructions](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html). First you will need to install miniconda locally. If this is something you've never done before or have limited experience with, it might be useful to ask someone for more help with this issue. Otherwise proceed as follows.

Download the most recent version of miniconda (assuming you are installing this in your home directory):
```
cd ~
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```
Follow the prompts on the screen to finish the installation.

To make the changes take effect, close and then re-open your terminal window.

Test your installation. In your terminal window or Anaconda Prompt, run the command `conda list`. A list of installed packages appears if it has been installed correctly.


## Plink
For very obnoxious reasons both the original plink (1.9) and plink 2.0 are probably required. Installing them locally is an option, but it may just make an alias. Do this by adding the following two lines to your `~./bashrc` file:
```
alias plink2="/frazer01/software/plink-2.3/plink2_64"
alias plink="/frazer01/software/plink-1.90b3x/plink"
```


### Set up a python kernel for the jupyter lab
Coming soon.


# Running a qsub job
Run qsub:
```
qsub my_script.sh
```

You can include the following to the SH file to pass to `qsub` as:
```
#!/bin/bash

#$ -N job_name
#$ -pe smp 4      ### specify number of cores requested
#$ -l h_vmem=4G   ### specify amount of memory per core (default is 4Gb per core)
#$ -l short       ### specify queue ([short, week, long, opt], default is all)
#$ -V             ### export your current environment parameters to the job
#$ -cwd           ### change the working directory to where the script was submitted from
#$ -e ~/std.err   ### redirect stderr to this file
#$ -o ~/std.out   ### redirect stdout to this file
#$ -t 1-10        ### define array jobs (in this case will run 10 jobs), use $SGE_TASK_ID to get access to the array index
```

Always make sure that environment is activated in the SH file:
```
source /home/username/.bashrc
```

# Useful File Locations

- UKBB pgen files: `/frazer01/projects/CEGS/analysis/apoe_haplotypes/input/genotypes/ukbb`
- UKBB subjects by ethnicity: `/frazer01/projects/CEGS/analysis/ukbb_hla_type_gwas/pipeline/ethnicity/subjects_by_ethnicity/`

# Forking a Github repo branch

First, go on GitHub and click fork in the upper right hand side. This should add the repository to your user account homepage.

```
git clone <URL-of-repository>
```
Navigate into directory on your local machine or server.
```
git status
```
Should say "on branch master"
```
git branch
```
Should say "* master"
```
git pull upstream master
```

Should give error ‘upstream’ does not appear to be a git repo
```
git remote add upstream <URL>
git pull upstream master
```
should execute with no errors
```
git checkout -b desired-branch-name
git branch
```
Should say "* desired-branch-name". We are trying to see if this is executing the correct sequence of commands.
```
git add file1
git commit -m ‘Update file1’
git push origin desired-branch-name
```

Then go to the github website and go to PULL REQUESTS in the upper left corner. Click issue pull request and add any comments. Make sure you don’t click merge on the website until someone reviews your code!
