# Setting Up a Conda Enviroments For Bioinformatics

## Download miniconda
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.10.3-Linux-x86_64.sh
```

## install Miniconda
```bash
bash Miniconda3-py39_4.10.3-Linux-x86_64.sh
```

By default, miniconda will be installed at the home directoty.
To verify if every thing were installed and configured correctly, type the command:  
```bash
source ~/.bashrc

# or reinitiate the terminal.
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
This command will wright into the file .bashrc the path to activate the base.

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


# Create a conda Enviroment

## Creating a conda enviroment:
```bash
conda create -n myenv python=3.8

conda activate myenv

# Commands to list the envs available
conda info --envs

conda env list
```

# Removing Enviroments

```bash
conda env remove -n myenv

conda remove --name myenv --all
```


# Instaling Packages

### Install SRA Toolskit:
The RSA Toolskit is a collection of tools and libraries for using data in the INSDC Sequence Read Archives.
```bash
conda install -c bioconda sra-tools

# versão mais recente
conda install -c bioconda/label/cf201901 sra-tools 
```

### Install biopython:
```bash
conda install -c conda-forge biopython
conda update -c conda-forge biopython

# the recomendations is to install all packages with the same package manager, but if it not available, do:
pip install biopython
```

## install fasqc
```bash
conda install fastqc
conda install -c bioconda fastqc
conda update fastqc
```

## Install MultiQC
```bash
conda install multiqc
```

## Install hisat2
```bash
conda install -c bioconda hisat2
conda install -c bioconda/label/cf201901 hisat2
```

### Install samtools

```bash
# -- version 1.13 - stable. but not available any more
conda install samtools   

# Lastest version1.7 ***com problemas
$ conda install -c bioconda/label/cf201901 samtools

# work around - install samtools 1.7 and then, update it to the latest build: tested 23/12/2021
$ conda install -c bioconda samtools=1.9 --force-reinstall
```

### installing featureCounts
featureCounsts is a subpackage of subread

```bash
conda install -c bioconda subread
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
