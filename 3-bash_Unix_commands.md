
# UNIX commands used in bioinformatics
Autor: Luiz Carlos  
Data: 31/12/2021


Bash is a Unix shell and command language written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell.
First released in 1989, it has been used as the default login shell for most Linux distributions. A version is also available for Windows,
via the Windows Subsystem for Linux.[¹](https://en.wikipedia.org/wiki/Bash_(Unix_shell))

## Basic commands line used
```bash
sudo                # super user do
sudo apt update     # to update
sudo apt update && sudo apt upgrade
apt search 'app name'

pwd                 # Currently working directory
history             # list of command used. It's possible to use arrow down and up to show the last 100 comands.
clear               # clear command prompt
cat filename.ext    # to show or execute the file
```

## CHMOD

This command modify files permissions, controling who can access files, search directories, and run scripts.

### Usage:
chmod [mode] [operator] [permission] file.ext

### Mode ugoa

These letters "ugoa" in the command chmod definy which of the user will have ther permissions modified.

    u : Owner of the file (user);
    g : Members of the group the file belongs (Groups);
    o : any other user (others);
    a : all user of the system (all).

If none is passed to the command, the system will uses all as default.

### Operators

With the command chmod, has to be used with a operator, to specify the kind of permission which will be given.

    + : Grants the permission. The permission is added to the existing permissions;
    – : remove permissions specified;
    = : Set a permission and remove others.

### Values
    r : The read permission.
    w : The write permission.
    x : The execute permission.


### Setting And Modifying Permissions

Checking the permission
```bash
ls -l file.txt
```

output: I separated them to a better visualization:

    - rwx rw- r-- 1 luiz luiz 6kb Jan 12 14:38 file.txt
    d rwx rwx rw- 1 luiz luiz 6k Jan 12 14:38 data

where the first fild "-" means the file is not a directory, like in the seconda exemple, represented by "d".  

The seconda fild "rwx", represent the permissions for the user;  
The third fild "rw-", represents the permissions for others;  
And the forth fild "r--", represents the permissions to all.  

### Setting a permissions
```bash
# removing permission to write and execute to group and others
chmod go-wx file.txt

# set only permission to read and write to group and others
chmod go=rw file.txt

# Add permission to execute to group and others
chmod go+x file.txt
```


## Running scripts
```bash
# simple run
bash script.sh

# Run in second plan
bash script.sh &

# redirect both stdout and stderr to file.log.txt
bash script.sh >& script.log.txt

# to run the scrip withou hang up, redirect both stdout and stderr to file.log.txt and run in second plan
nohup sh script.sh >& script.log.txt &

```

### Running scripts with a conda env setup
This kind of running is required when we need to activate a conda env, where all the programs needed to run the script are.

### Exemple of script
I do recommend not use any kind of characters as (_ , - , /) in the script name.

At the top of the script, starts as follow:

    #!/usr/bin/env bash                # shabang sign - Tells the operating system which interpreter to use. 
    set -o errexit                     # This will exit, if any erro happens.
    conda activate genomics            # This will activate the env we need to execute the script, change for the one you have.
    
    command 1
    command 2
    command 3


Before run any command, let's ussume we have a env called genomics, and there are all the programs needed to execute the following script.
```bash
# Note: this script starts as showed above.

# running in interactive mode.
bash -i script2.sh

# redirect both stdout and stderr to file.log.txt
bash -i script2.sh >& script2.log.txt


# Now, let's assume we don't wrote in the script to activate genomics
# We can open the terminal and do as follow:
conda activate genomics
./script2.sh >& script2.log.txt    # This comand will run the script interacting if the current env.

```


## List the content of a directory
```bash
# list everything in pwd
ls

# list the content of a specific directory
ls dir_name

# ls command with flags
ls [flags] [directory]

ls -d */     # to list only directories
ls *         # to list the contents of the directory with it's subdirectories:
ls -R        # to list all files and directories with their corresponding subdirectories down to the last file:
ls -s        # to list files or directories with their sizes:
ls -l        # to list the contents of the directory in a table format
ls -lh       # to list the files or directories in a human readable table format
ls -a        # to list files or directories including hidden files or directories 
ls -t        # to list files or directories and sort by last modified date and time in descending order
ls -tr       # the same as above in reverse order
ls -S        # (the S is uppercase) command to list files or directories and sort by date or time in descending order (biggest to smallest).

```


## Create a directory

Create the DIRECTORY(ies), if they do not already exist.

Usage: 
```bash
mkdir [OPTION]... DIRECTORY Nane...
```

Mandatory arguments to long options are mandatory for short options too:

    -m, --mode=MODE   # set file mode (as in chmod), not a=rwx - umask
    -p, --parents     # no error if the diretory already exist, make parent directories as needed
    -v, --verbose     # print a message for each created directory


## Remove files and directories
```bash
rmdir dir_name # remove directory if its empty
rm -r dir_name # remove all directory and everything in it.
rm -l dir_name # remove but prompt which file should be removed 
rm -v dir_name # verbose what is going on
rm -i filename # this will ask if we sure we want to delete
```


## Change directory
```bash
cd          # move to home directory
cd /        # move root directory
cd dir_name # move a specified directory
cd -        # move one directory up
cd ..       # move one directory up
cd ../../   # move two directory up
```

## Copy Files and Directories

Common options used with the cp command, include:  

    -a – archive, never follow symbolic links, preserve links, copy directories recursively  
    -f – if an existing destination file cannot be opened, remove it and try again  
    -i – prompt before overwriting an existing file  
    -r – copy directories recursively  

```bash
# Copying a single file to a destination directory
cp data.txt /var/tmp/

# Copying multiple files to a destination directory
cp data.txt file.csv /var/tmp/

# Copying a directory (and it’s contents) recursively
cp -r /etc/ /var/tmp/backup/
```

## Move Files and Directories

The mv command will move or rename files or directories, or can move multiple sources (files and directories)
to a destination directory. 

The basic syntax of the mv command is:
```bash
mv [options] source destination
```

## To move multiple files/directories into a destination
```bash
mv [options] source1 source2 [...] destination
```

Common options used with the mv command: 

    -f – do not prompt before overwriting  
    -i – prompt before overwrite  
    -u – move only when the source file is newer than the destination file or when the destination file is missing  

Note 1: that if the destination exists, it will be overwritten unless the -i option is used.  

Note 2: If a file or directory is moved to a new name within the same directory, it is effectively renamed.   


## Rename a file
```bash
mv -i oldname newname
```


## Creating files
```bash
touch filename.ext #create empty files
touch /home/doc.txt # create a empty file in a specific directory
```

## Writting in files
```bash
echo msg to be written file.ext
```

## Redirect outputs from command into a file
```bash
# Overwriting the file or creating a new one
command > file.txt

# Appending into a file
command >> file.txt

# Showing output and overwritting a existing file using pipe (|) and tee
command | tee file.txt

# Showing output and append it to a existing file
command | tee -a file.txt

# Showing output and append it to a existing file
command | tee -a file.txt
```


## Search for files
```bash
find -name dir_or_filename
```

## Visualize files

### head and tail
```bash
head file_name.ext
tail file_name.ext

# With the option -n plus a number specifies the number of lines to be shown.
head -n10 file_name.ext
```

### more and less
Those are a *nix command line used to display the contents of a file in a console.   
The basic usage of more command is to run the command against a file as shown below:  
```bash
more filename.ext 

less filename.ext
```

Option for less and more:  

    -g               # highlight serch, lasta match  
    -G               # highlight serch  
    -s               # sqeeze long lines  
    -S               # chop-long-lines  
    q                # quit reading file  
    enter or ▼       # forward one line  
    ▲                # backward one line  
    space or f       # forward one window  
    b                # backward one window  
    /pattern         # search for a parttern forward  
    ?pattern         # search for a pattern backward  
    &pattern         # display only matching lines  

With the file opened with less or more, is possible to search for pattenrs or go to a specific line in it  
```bash
\>
5555g

# with nano 
ctrl + shift + - and choose the line number
```


## Uses of regular expression

    *       # Any kind of character one or more times
    ?       # Any kind of character one time
    [0-9]   # Any number character
    [a-z]   # Any alphabetic character
    {pattern1,pattern2,etc.}.png

```bash
ls *
ls *.png
ls [0-9]*.png           # find a match which have a number repeated mulpliple times. Such as 111.png, 90876.png etc.
ls [a-z]*.png           # The same as above, but now with alphabetical characteres.
ls ?mage.png            # Find a match which starts with any character only one time folowed by mage.png
ls {file1,file2}.png

```


## Compress and Uncompress files

### option:
    -c, --stdout    = compress but, write on standard output, keep original files unchanged  
    -k, --keep       = keep (don't delete) input files  
    -d, --decompress = decompress  
    -t, --test       = test compressed file integrity  
    -v, --verbose    = verbose mode  
    -l, --list       = list compressed file contents  


```bash
# To compress
gzip file_name
bzip file_name


# Uncompress files
gunzip -k file_name
gzip -d file_name

bunzip file_name

```


## Group and compress multiple files with TAR

Descrition:  
tar (Tape ARchiving) group/ungroup files.

Sintax:  
tar [opções] grouped_name.tar [files]  

Options command:  

    -c : creates a new tar file.  
    -t : list the content of tar file.  
    -x : extract the content of tar.  
    -v : "verbose" show mensagens of what is happening.  
    -f file : defines the name of the tar file.  
    -z ou −−gzip ou −−gunzip : compress/uncompress files using gzip/gunzip.  
    -j ou −−bzip2 : compress/uncompress using bzip2.
    -?, −−help : mostra as opções do comando.  


```bash
# To creates a file colection_txt with group all txt files in the pwd.
tar -cvf colection_txt.tar *.txt

# To verify the content of the archive colection_txt
tar -tvf colection_txt.tar

# to extract all the file from colection_txt
tar -xvf colection_txt.tar

# to extract a specific file from colection_txt 
tar -xvf colection_txt.tar filename.ext


### Creating file grouped and compressed:

# To compress the files grouped by tar, we can use gzip
tar -czvf colection.tar *.txt

# to compress using bzip2 with starts with test
tar -cjvf colection2.tar *.txt
```


## Disck space usage
```bash
df 
df -h .         # for human size readble
df -h -m .      # for human readble in megabyties
du -sh          # size of pwd
du -sh dir_name
```

## sort
```bash
# Defualt alphabetically
sort filename

# Sort by column 2
sort -k 2 filename

# sort by column numerically
sort -k 2n filename

# sort reversely and numerically 
sort -k 2rn filename

# sort bby multiple columns
sort -k 2 -k 3 filename

# sort uniquely
sort -u filename
```

## cut

cut is a command-line utility that allows you to cut parts of lines from specified files or piped data and print the result to standard output. 
It can be used to cut parts of a line by delimiter, byte position, and character.

Options:  

    -f (--fields = LIST)______ # Select by specifying a field, a set of fields, or a range of fields.  
    -d (--delimiter)__________ # Specify a delimiter that will be used instead of the default “TAB” delimiter..  
    -c (--characters = LIST)__ # Select by specifying a character, a set of characters, or a range of characters..  

The LIST argument passed to the -f, -b, and -c options can be an integer, multiple integers separated by commas, a range of integers
or multiple integer ranges separated by commas.

The syntax for the cut command:
```bash
# default delimiter tab
cut -f 1,7-10 featurecounts.txt > counts.txt

# specifying a new delimiter
cut -d ' ' -f 1,7-10 featurecounts.txt > counts.txt
```

## uniq
return unique lines, if consecutive occurances are found in sequence
```bash
uniq filename

# counts the consecutive occurences
uniq -c filename
```

## grep
```bash
grep pattern file.ext

# find a pattern in all files.txt
grep "pattern" *.txt

# return the line number of the pattern
grep -n "pattern" file.ext

# Counts the occurences of the pattern
grep -c "pattern" file.ext

# to grep all except the pattern
grep -v "pattern" filename

# to grep multiple patterns
grep -e "pattern1" -e "pattern2" file

grep "[I,D]"

egrep "pattern1|parttern2" file

```

## WC

Description:  
counts the number of lines, words and characteres of a file.

options: 

    -c : counts bytes.  
    -l : counts lines.  
    -L : show the lenght of longest line.
    -m : counts characteres.
    -w : counts words.

```bash
wc [option] [file]  
wc -l file
```

## sed

SED command in UNIX stands for stream editor and it can perform lots of functions on file like searching, find and replace, insertion or deletion.

Usage:

sed OPTIONS... [SCRIPT] [INPUTFILE...]

options:

    -i ------> change the file in place
    -e ------> print without changing the file
    -n ------> show just the result of the command
    s -------> replace a pattern for another
    p -------> p at the end, prints
    g -------> g at the end, change all accurrences


Sed command is mostly used to replace the text in a file. 
```bash
# Replacing or substituting string not in place: 
sed 's/strig_to_find/new_string/' file.txt

# Replacing or substituting string in place: 
sed -i 's/strig_to_find/new_string/' file.txt

# Replacing a string between lines 3 and 9: 
sed '3,9s/strig_to_find/new_string/' file.txt

# Delete all lines with the string specified
sed -i '/string/d' file.txt

# insert a string at the beginning of each line
sed 's/^/string/' file.txt

# replace all occurrences of the strings “marcos”, “luiz”, “karol” by “friends”
sed 's/marcos\|luiz\|karol/friends/g' file.txt

# Insert the string ‘#’ at the beggining of lines 1 to 8
sed -i '1,8s/^/#/' file.txt

# Substitute “foo” by “bar” onle at lines with “##”
sed '/##/s/foo/bar/g' arquivo.txt

# prints only the lines each starts with the string ‘http’
sed -n '/^http/p' file.txt

# print only the line 9
sed -n '9p' file.txt

# Print from line 6 to 9 
sed -n '6,9p' file.txt


```
[link for more exemples](https://terminalroot.com.br/2015/07/30-exemplos-do-comando-sed-com-regex.html)


## comm

Description:  
Compare sorted files FILE1 and FILE2 line by line.  

Syntax:  
comm [OPTION]... FILE1 FILE2

```bash
# With no options, produce three-column output:
# Column one contains lines unique to FILE1, 
# column two contains lines unique to FILE2, and 
# column three contains lines common to both files.
comm fileA.txt fileB.txt

# suppress column 1 (lines unique to FILE1) 
comm -1 fileA.txt fileB.txt

# suppress column 2 (lines unique to FILE2) 
comm -2 fileA.txt fileB.txt

# suppress column 3 (lines that appear in both files)  
comm -3 fileA.txt fileB.txt

# Print only lines present in both file1 and file2.
comm -12 fileA.txt fileB.txt


```

 

# For Loop in linux

## Loop over a string
```bash
sample="1 2 3 4"; for i in $sample; do echo "wellcome $i times"; done
```

## Over a array:
first declare an array of string with type.   
Then Iterate the string array using for loop.   
The doble quote around ${StringArray[@]}, force the whitespaced variable to be read as a simgle variable.  
```bash
StringArray=("Linux Mint" "Fedora" "Red Hat Linux" "Ubuntu" "Debian" ); for val in "${StringArray[@]}"; do echo $val; done
```


# Utilities for bioinformatics

## TREE

### Descrição:
Este utilitário lista o conteúdo de um diretório usando o formato de árvore. 
Ele tem a mesma função do comando ls. A diferença consiste na maneira como as informações são exibidas.

Installation:
```bash
sudo apt install tree
```

Algumas opções do comando:  

    -a : lista todos os arquivos, inclusive os arquivos ocultos.  
    -d : lista somente os subdiretórios.  
    -f : exibe o caminho completo dos arquivos.  
    -p : exibe as permissões dos arquivos.  
    −−help : exibe as opções do utilitário.  
    −−version : mostra informações sobre o utilitário.  


```bash
tree -d # lista os diretórios do pwd
tree -d dir_name # lista o diretório especificado
tree -a 
```

## wget

Wget is a command-line utility for downloading files from the web. With Wget, you can download files using HTTP, HTTPS, and FTP protocols. 
Wget provides a number of options allowing you to download multiple files, resume downloads, limit the bandwidth, recursive downloads, 
download in the background, mirror a website, and more.

Options:  

    -nv ------> non verbose
    -O -------> Saving the downloaded file under different name 
    -P -------> Download the file into a specific directory
    -c -------> Resuming a download from the previous one
    -b -------> Downloading in background
    -i -------> Downloading multiple files (this options need to be followed by the path to a local or external file containing a list of the 
    URLs to be downloaded. Each URL needs to be on a separate line).


Downloading files from internet
```bash
wget -o /mnt/c/file.txt 'link to download the file'
```

Download a fasta file from NCBI into the PC with (eutils):
```bash
wget "http://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=NC_045512.2&rettype=fasta" -O covid_genome.fa 
```

Download a list of fastq files:
```bash
wget -i urls_fastq_files.txt
```



# Shortcuts
```bash
ctrl + l         # clear cmd
ctrl + d         # quit()
ctrl + c         # interrupt
ctrl + z         # interrupt abruptly
ctrl + a         # move to the start of line
ctrl + e         # move to the end of line
ctrl + shift + c # copy
ctrl + shift + v # paste
right click of mouse to paste
jupyter notebook --no-browser
'dir name'      # use of '' to acess dir with spaces in the name
up and down arrows to show previewly command used
```



# Creating alias to open files in wsl

.bashrc is a login scripts which load a user's personal preferences. Upon creation of their account, a .bashrc file with default settings
is copied into a user's home directory. The user can then modify that file to customize their session. They can modify environment variables, 
load modules, create aliases and activate Python virtual environments. Users can also modify .bashrc to change aesthetic things like the terminal
color scheme and what their bash prompt displays. To edit your .bashrc file use a command line editor like vim or nano:

## Creating a alias "open" by writing it into the .bashrc file:
```bash
echo "alias open='wslview'" >> ~/.bashrc
```

WE can edit the .bashrc too from nano.
```bash
nano ~/.bashrc

# with the file opened:
"alias open='wslview'"
```

## Activating alias
```bash
source ~/.bashrc
```

## Removing alias:
```bash
unalias alias_name
```




