#!/bin/bash

# Student ID: 100499009

# For full reproducibility this workshop has a full public github repository with a README.md file. 
# Please view the repo here: https://github.com/AnonymousUEAStudent/Workshop1

# The following is a break down of the material covered in workshop 1. It consists of a combination of simple command line navigation and file creation techniques followed
# by more complicated file manipulation to find out bioinformatic information when dealing with gff3 files. 
# Commentary includes descriptions of the commands used, their inteded purpose, as well as the output of the commands.
# Questions 1-2 are simple command line navigation and file creation techniques.
# Question 3 covers more complicated file manipulation to find out bioinformatic information when dealing with gff3 files.

# Learning command line commands: The following lists some of the most common commands used in Linux, and their intended purpose.
# pwd                       states current directory location (print working directory)
# cd                        change current directory
# cd ..                     go up one level from current directory
# mkdir                     create new directory folder
# ls                        list current files/folders in current directory location
# man                       manual/help information for program
# --help                    alternative help option as argument for program

# cat                       concatenate the content of files, either to terminal or pipe it to other commands (can also be used to create new files with the use of > )
# head                      show the first n number of lines from a files (10 default)
# tail                      show the end n number of lines from a files (10 default)
# wc                        word count of file (-l option gives new line count)
# less                      alternative way of viewing file content
# nano                      text editor allows you to alter file content
# mv                        moving files to different locations
# cp                        duplicate file and add it to new location
# grep                      search tool for finding strings within file use of regular expressions is common
# sed 's/term/new/g'        string replacement command
# cut -f colnum file        prints a single column to the standard output. Can print multiple columns if a range is supplied (e.g. -f2-5)

# awk <...>                                                     a language supplied with Linux to manipulate text-based files. Extremely powerful and robust. 
# awk ‘$<col_num> == <value>’ [file_name]                       prints all lines from file where a specified column which equal a value
# awk ‘$<col_num> > <value>’ [file_name]                        prints all lines from a file where a specified column which are greater than a value
# awk ‘$<col_num> == <value> {print $5 -$4}’ [file_name]        selects all lines from a file where a specified column which equal a value, 
#                                                               then prints the product of a subtraction of the entry of the 4th column from the 5th 
# Piping
# <program> | <program>         pipe – passes the standard output of one program to the standard input of another. Used to construct basic pipelines
# <program> > <new_file_name>	redirect – passes the standard output of a program to a location. Can be used to make a new file with the standard output if a new file name is specified            

# Prior to running the commands in this script, the files and folders generated in the exercises are deleted here, to ensure reproducibility when re-running the script
echo "Deleting any previous files to ensure reproducibility"
rm -f c13genes.txt
rm -f ENSG00000139618.gff3
rm -f exon_lenths.txt
rm -f exon_sequences.gff3
rm -f Homo_sapiens.GRCh38.113.chromosome.13.gff3
rm -f longest.txt
rm -f research2.txt
rm -f test1.txt # These two lines ensure there is an empty test1.txt file present
touch test1.txt
rm -f research.txt # These two lines ensure there is a research.txt file present with the correct content
echo "Project Title: Influence of biochar and antibiotics on the soil microbiome
Project Description: How does adding biochar antibiotics change the soil  microbiome
Project Keywords: Biochar, Antibiotics, Metagenome, Soil
Project Dates: 01/10/24-01/09/25
Previous Research: Biochemistry BSc" > research.txt

echo "Setup complete"

# Exercise 1
# 1a) Look at the man for ls, work out what the flag -lrth does to the output:

# Both of the following give the required documentation. Commented out to prevent large output when running the script. 
# man ls
# ls --help 
# h: human readable, r: reverse sort direction, l: long-format, t: sort by time newest first

# 1b) Use the command mkdir to make a file structure which you can understand. 
# You need to have a directory for input data, and some for the outputs of sessions 1-3. 
# Remember the naming conventions in Linux – do not use spaces in your directory or file names

# Example folder creation:
mkdir bioinformatics
mkdir bioinformatics/test_subfolder
mkdir bioinformatics/test_subfolder/further_subfolder

# 1c) Use the cat command to look some of the files used in the last session, 
# then compare how useful this is compared to looking at them with less. Remember that you exit less by pressing q.

# Example cat usage: These commands are commented out to allow the script to run uninterrupted
# cat > test1.txt     # create new file and add text by typing, end input with ctrl + d
# cat test1.txt       # read file contents
# less test1.txt      # alternative file reading

# 1d) Use the head command to look at top lines of the documents, and use -n flag to change the number of lines you look at. 
# Think about how this may be useful when working with many different file types, or custom-built files with no standard format.

# # Example head usage: These commands are commented out to allow the script to run uninterrupted     
# head test1.txt      # default output of 10 lines
# head -n 2 test1.txt # Specify just the first 2 lines for output

#1e) Using cp or mv, to put the files generated in the last session into the file structure you have created.

# Example mv/cp usage:
mv test1.txt bioinformatics/test1.txt                  # Move file from current directory to the newly made bioinformatics folder
cp test1.txt bioinformatics/test_subfolder/test1.txt   # Copy file from current folder and duplicate it in bioinformatics/test_subfolder

# 1f) Use nano to create a file (with a name you define yourself, ending with the extension ‘.txt’) with the following headers in it. 
# For each line copy the header and then complete the line. Use Ctrl + o to save the file and Ctrl + x to exit nano.

# Project Title: <most recent research project title>
# Project Description: <1 sentence describing your project>
# Project Keywords: <at least 3 keywords related to your project> 
# Project Dates: <Start + end date of your project>

# Example Nano usage:        
# nano research.txt      # Create new empty file, add text exit with ctrl + x, save with y on confirmation or with ctrl + o beforehand.

# For reproducibility the contents of research.txt created in nano is the following, omitting the comment formatting (# at the start of the line):
# Project Title: Influence of biochar and antibiotics on the soil microbiome
# Project Description: How does adding biochar antibiotics change the soil  microbiome
# Project Keywords: Biochar, Antibiotics, Metagenome, Soil
# Project Dates: 01/10/24-01/09/25
# Previous Research: Biochemistry BSc

# Exercise 2
# Using the .txt file that you wrote in the first session describing your research, go the following:

#2a) Edit the file to add a line detailing what your undergraduate degree was. Use the header ‘Previous Research: ’

# nano research.txt # Add required text ctrl + o, then ctrl + x
# nano research.txt # Reopens the file allowing for the addition new text

#2b) Find the number of lines in the file:      
wc -l research.txt  
# Output: 5 research.txt (5 Lines)

#2c) Search for the line which describes your Project
grep 'Project Description' research.txt # Prints the line which has includes 'Project Description'
# Output: Project Description: How does adding biochar antibiotics change the soil  microbiome

#2d) Count the number of lines containing the word ‘the’ in the description, and the term ‘Project’.   
grep -c 'the' research.txt                     # Prints all lines which include 'the'
# Output: 2

grep -c 'Project' research.txt                 # Prints all lines which include 'the'
# Output: 4

# 2e) Without using a text editor, change the colon at the ends of your headers to an equals sign
# Replace colons with =:     
sed 's/: /=/g' research.txt > research2.txt # Replaces all instances of : with = and writes to a new file to ensure the original file is not lost

# Alternatively you could use the -i flag to update the file in place, but this is not recommended for reproducibility
sed -i 's/: /=/g' research2.txt # Replaces all instances of : with = and updates the file in place 
# The above changes nothing in this example, as the change was made in the previous sed line which generates research2.txt


# Question 3's results should be reproducible, and give the same results as the commentary suggests.
# Running all commands will produde the following files:
# c13genes.txt: 348 lines decribing the genes from the gff3 file for Human chromosome 13
# ENSG00000139618.gff3: A file containing the line associated with the Ensembl i.d ENSG00000139618
# exon_lenths.txt: A file containing the lengths of the exons for the transcript ENST00000470094
# exon_sequences.gff3: A file containing the lines for the exons of the transcript ENST00000470094
# Homo_sapiens.GRCh38.113.chromosome.13.gff3: Downloaded gff3 file for Human chromosome 13
# longest.txt: A file listing the lengths of the longest genes which are greater than 10000nt. A sanity check to ensure only values greater than 9999nt are included.

# Exercise 3
# Using the annotation file for Human chromosome 13, use the tools introduced today to:
# First download the .gff3 annotation for the Human chromosome 13. Use the two lines below to do this, but make sure you are in the correct place in your file structure to do it. 

# Pasted commands to download external file
wget https://ftp.ensembl.org/pub/current_gff3/homo_sapiens/Homo_sapiens.GRCh38.113.chromosome.13.gff3.gz
gunzip Homo_sapiens.GRCh38.113.chromosome.13.gff3.gz

# 3a) Find out how many genes are found on chromosome 13:                                        
grep -P -c '\tgene\t' Homo_sapiens.GRCh38.113.chromosome.13.gff3 
# Output 348
# Grep using -P to allow for tab characters in regex. Select only gene lines 
# The -c argument then counts the number of lines.

#3b) Create a new file containing only the full lines describing genes:     
grep -P '\tgene\t' Homo_sapiens.GRCh38.113.chromosome.13.gff3 > c13genes.txt
# Grep using -P to allow for tab characters in regex. Select only gene lines and includes all of the line.

#3c) Find out how many genes have a gene space > 10,000nt                   
awk '$3 == "gene" {print $5 - $4}' Homo_sapiens.GRCh38.113.chromosome.13.gff3 | grep -c '.\{5\}'
# Find all lengths of genes by taking column 4 from 5. Then pipe the result to grep.
# Then find any line with at least 5 characters, this will be > 9,999.
# Output 270

# Sanity checked by running the following and checking all values are above 10000
awk '$3 == "gene" {print $5 - $4}' Homo_sapiens.GRCh38.113.chromosome.13.gff3 | grep '.\{5\}' > longest.txt

#3d) Find what gene is associated with the Ensembl i.d. ENSG00000139618     
grep -w 'ID=gene:ENSG00000139618' Homo_sapiens.GRCh38.113.chromosome.13.gff3 > ENSG00000139618.gff3 
# BRCA2 DNA repair associated gene
# https://www.ensembl.org/Homo_sapiens/Gene/Summary?g=ENSG00000139618;r=13:32315086-32400268

#3e) For the gene which is the answer to C, work out the length of the
# transcript (exons only) for one of the three isoforms (different transcripts)

# Choose one of the transcript IDs and grep for it:   
grep ENST00000470094 Homo_sapiens.GRCh38.113.chromosome.13.gff3 | awk '$3 == "exon"' > exon_sequences.gff3
# Get the lines specifically for the transcript, and filter to those that are exons. Save that to a file
awk '{print $5 - $4}'  exon_sequences.gff3 > exon_lenths.txt
# Get the lengths of each exon sequence and print to file
awk '{ sum += $1 } END { print sum }' exon_lenths.txt
# Sum all the lengths in the file. Output: 12049
# Very similar to the value shown for that transcript in
# https://www.ensembl.org/Homo_sapiens/Gene/Summary?g=ENSG00000139618;r=13:32315086-32400268


# If you have not visited the repo as stated at the start of the file, the README.md is included below:
# Available here: https://github.com/AnonymousUEAStudent/Workshop1

# # Data Science & Bioinformatics Workshop 1: Linux Excercises
# This repo includes all the required files to fully answer the questions set in this workshop, and ensuring reproducibility.
# Each file is listed here with its intended purpose:

# ## Files:
# BIO7051B_2025_Excercises.docx: Exercise instructions for the workshop 
# ## Exercise 1 files
# test1.txt: An empty txt file created to show how to move and copy files 
# ## Exercise 2 files
# research.txt: A basic text file containing the contents of previous research.

# ### Exercise 3 files
# The following files are all generated when running the commandlines in exercise 3.

# c13genes.txt: 348 lines decribing the genes from the gff3 file for Human chromosome 13
# ENSG00000139618.gff3: A file containing the line associated with the Ensembl i.d ENSG00000139618
# exon_lenths.txt: A file containing the lengths of the exons for the transcript ENST00000470094
# exon_sequences.gff3: A file containing the lines for the exons of the transcript ENST00000470094
# Homo_sapiens.GRCh38.113.chromosome.13.gff3: Downloaded gff3 file for Human chromosome 13
# longest.txt: A file listing the lengths of the longest genes which are greater than 10000nt. A sanity check to ensure only values greater than 9999nt are included.

# ## Reproducing the exercise:
# Clone the repo and use cd to navigate into the repo folder created.

# The script includes a few setup lines to ensure the script is reproducible when running multiple times.
# This includes the deletion of files and folders generated during the script and generating two .txt files.
# Running the script will produce the output described in the workshop_1.sh.txt file.

# Run the bash script file using: bash workshop1.sh. (Remove the .txt extension if required).

# A summary of what the script achieves is listed below:
# First the local directory is reset to include an empty test1.txt file and a research.txt with some content.
# Creates new subdirectories within the current directory, a requirement for the questions in exercise 1.
# Moves and copies an empty test1.txt file into the new subdirectories created.
# Investigates the research.txt file with some grep commands.
# Uses sed to do some text replacement using research.txt, creating a new research2.txt file with the changes.

# Follows the exercise 3 bioinformatic questions to generate some files and answer the posed questions.