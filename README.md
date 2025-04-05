# Data Science & Bioinformatics Workshop 1: Linux Excercises
This repo includes all the required files to fully answer the questions set in this workshop, and ensuring reproducibility.
Each file is listed here with its intended purpose:

## Files:
BIO7051B_2025_Excercises.docx: Exercise instructions for the workshop 
## Exercise 1 files
test1.txt: An empty txt file created to show how to move and copy files 
## Exercise 2 files
research.txt: A basic text file containing the contents of previous research.

### Exercise 3 files
The following files are all generated when running the commandlines in exercise 3.

c13genes.txt: 348 lines decribing the genes from the gff3 file for Human chromosome 13

ENSG00000139618.gff3: A file containing the line associated with the Ensembl i.d ENSG00000139618

exon_lenths.txt: A file containing the lengths of the exons for the transcript ENST00000470094

exon_sequences.gff3: A file containing the lines for the exons of the transcript ENST00000470094

Homo_sapiens.GRCh38.113.chromosome.13.gff3: Downloaded gff3 file for Human chromosome 13

longest.txt: A file listing the lengths of the longest genes which are greater than 10000nt. A sanity check to ensure only values greater than 9999nt are included.

## Reproducing the exercise:
Clone the repo and use cd to navigate into the repo folder created.

Ensure that both test1.txt and research.txt are present in your current working directory (use ls on the commandline)
Run the bash script file using: bash script.sh.
The script includes a few setup lines to ensure the script is reproducible when running multiple times.
This includes the deletion of files and folders generated during the script.
Running the script will produce the output described in the workshop_1.sh.txt file.

A summary of what the script achieves is listed below:
First the local directory is reset to only include an empty test1.txt file and a research.txt with some content.
Creates new subdirectories within the current directory, a requirement for the questions in exercise 1.
Moves and copies an empty test1.txt file into the new subdirectories created.
Investigates the research.txt file with some grep commands.
Uses sed to do some text replacement using research.txt, creating a new research2.txt file with the changes.

Follows the exercise 3 bioinformatic questions to generate some files and answer the posed questions.
