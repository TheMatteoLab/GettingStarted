# Links
- [CAST website](https://admixgenomics.ucsd.edu/)
- [UKBB user site](https://bbams.ndph.ox.ac.uk/ams/researcher_home.jsp)

# Getting Started

Initially you should have a user account on the Frazer Lab server. In order to access the server from your home terminal:
```
ssh username@flh1.ucsd.edu
```
You should typically not work on the head node. After you have logged in, to navigate elsewhere:
```
ssh n1
```

### Install miniconda 

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

### "Install" plink

For very obnoxious reasons both the original plink (1.9) and plink 2.0 are probably required. Installing them locally is an option, but it may just make an alias. Do this by adding the following two lines to your `~./bashrc` file:
```
alias plink2="/frazer01/software/plink-2.3/plink2_64"
alias plink="/frazer01/software/plink-1.90b3x/plink"
```
### Set up a python kernel for the jupyter lab
Coming soon.


# Running a qsub job

Coming soon.

# Useful File Locations

Coming soon.
