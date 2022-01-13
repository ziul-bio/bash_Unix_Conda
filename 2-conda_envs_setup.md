# Setting Up a Conda Enviroments For Bioinformatics
Autor: Luiz Carlos  
Data: 31/12/2021  

## Conda 

Conda is an open source package management system and environment management system that runs on Windows, macOS and Linux. 
Conda quickly installs, runs and updates packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python programs, but it can package and distribute software for any language.

Conda is also included in Anaconda Enterprise, which provides on-site enterprise package and environment management for Python, R, Node.js, Java and other application stacks. [¹](https://docs.conda.io/en/latest/)


#### Why???

An environment consists of a certain Python version and some packages. 

In bioinformatics, most of the packages used are mantained by studants in Universities, and some of them evolve and update slowly than versions of python.   

Then, we can end up needing to use some of the outdate bioinfo packages that are not supported by newer version of python.  

Conda allow us to create a enviroment with the version of python requeried for programs to work propetly.  

## Download miniconda
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.10.3-Linux-x86_64.sh
```

## Install Miniconda
```bash
bash Miniconda3-py39_4.10.3-Linux-x86_64.sh
```

By default, miniconda will be installed at the home directoty.
To verify if every thing were installed and configured correctly, type the command:  
```bash
source ~/.bashrc     # or reinitiate the terminal.
```
This command will activate the conda enviroment(Base) into the terminal, showing base at the left most side of the line.
Then, if everything goes correctly, there will be no need to type this command for future use.

## After instalation of miniconda,
if conda base enviroment is not set by default, its possible to set the conda base enviroment to activate automaticly or not.
```bash
# command to auto activate base
conda config --set auto_activate_base true 

# command to not auto activate base
conda config --set auto_activate_base false 
```


#
 
*In case of the env base wasn't automatic activate, will be necessary edit the .basrc file 
in the user's home directory.
For this, type the follow command: where "user_name" = the name of your linux user*.

```bash
echo 'PATH=/home/nome_do_usuário/miniconda3/bin:$PATH' >> ~/.bashrc
```
This command will write into the file .bashrc the path to activate the base.

#


# Config the channels

By definition, conda channels are the same across conda environments.

Channels are from where conda will download the packages.
Conda channel priority is ordered by which channel appears first (highest) in \~/.condarc

Doing this conda will seach first at default channels, after bioconda an then conda-forge:
```bash
conda config --add channels defaults
conda config --append channels bioconda
conda config --append channels conda-forge
```
This will avoid channel collisions.


# Use of conda

Remenbering, conda is a tool for manage environments and packages.

### Usage:

	conda command --help -----> This will show help for the specific command

### Usefull commands:

    create       Create a new conda environment from a list of specified packages.
    help         Displays a list of available conda commands and their help strings.
    info         Display information about current conda install.
    install      Installs a list of packages into a specified conda environment.
    list         List linked packages in a conda environment.
    remove       Remove a list of packages from a specified conda environment.
    search       Search for packages and display associated information. The input is a MatchSpec, a query language for conda packages.
    update       Updates conda packages to the latest compatible version.

### Options:

	-h, --help                         = Show this help message and exit.
	-all                               = Apply the command to all package in the env.
	-n ENVIRONMENT, --name ENVIRONMENT = Name of environment.
	-c CHANNEL, --channel CHANNEL      = Additional channel to search for packages.
	-y, --yes                          = Do not ask for confirmation.
	--force-reinstall                  = Ensure that any user-requested package for the current operation is uninstalled and reinstalled, even if that package already      exists in the environment.


## Creating a conda enviroment:
```bash
conda create -n myenv python=3.8

conda activate myenv
```


## List the envs available
```bash
conda info --envs

conda env list

# to list the package intalled in the enviroment
conda list -n myenv
```


## Removing Enviroments

```bash
conda remove --name myenv --all

conda env remove -n myenv
```


# Instaling Packages

## Search gor a package
```bash
conda search fastqc
```

output:

	Loading channels: done
	# Name                       Version           Build  Channel
	fastqc                        0.10.1               0  bioconda
	fastqc                        0.10.1               1  bioconda
	 ...                           ...                      ...
	fastqc                        0.11.8               0  bioconda
	fastqc                        0.11.8               1  bioconda
	fastqc                        0.11.8               2  bioconda
	fastqc                        0.11.9               0  bioconda
	fastqc                        0.11.9      hdfd78af_1  bioconda


## Installing packages

### Install fasqc
```bash
# Conda search in the available channels, previewlly seted up.
conda install fastqc

# This command, conda will search for the package at the bioconda channel
conda install -c bioconda fastqc
```

### Install MultiQC
```bash
conda install multiqc

# to install a specific package in an specific env
conda install -n myenv multiqc
```


### Install samtools
```bash
# This command will install the last version
conda install samtools   

# -- version 1.13 - stable and working with python 3.8

# If we face any problem, install samtools 1.9, downgrade it to the latest stable build: tested 23/12/2021
conda install -c bioconda samtools=1.9 --force-reinstall
```


### Install hisat2

In the site of Anaconda.org [at packages](https://anaconda.org/bioconda/hisat2/labels) is possible to choose from diferent labels.

	label       Version
	cf201901	2.1.0
	main	    2.2.1


```bash
# Installing main version
conda install -c bioconda hisat2

# Installing labeled version nº cf201901
conda install -c bioconda/label/cf201901 hisat2
```


### Install biopython:
```bash
conda install -c conda-forge biopython

# the recomendations is to install all packages with the same package manager, but if it not available, do:
pip install biopython
```


# Update an package (biopython)
```bash
conda update package_name

conda update -c conda-forge biopython
```


# Removing a package

To remove a packages such as samtools or any other in the current environment:
```bash
conda remove samtools
```

To remove a packages such as samtools or any other in other environment:
```bash
conda remove -n env_name samtools
```


# Uninstalling Anaconda or Miniconda

IN the terminal. Remove the entire Miniconda install directory with:
```bash
rm -rf ~/miniconda
```

## OPTIONAL: Remove the following hidden file and folders that may have been created in the home directory:

.condarc file
.conda directory
.continuum directory

By running:
```bash
$ rm -rf ~/.condarc ~/.conda ~/.continuum
```
