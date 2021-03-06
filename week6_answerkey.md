
# Week 6 exercises


### While Loop
#### 1. Blast Off: 
Write a while loop that prints out the following...
```
10
9
8
7
6
5
4
3
2
1
blast off!
```

#### While Loop -- ANSWER

```bash

#!/bin/bash

# type out blastoff

counter=10

while [ $counter -gt 0 ]
do
    echo $counter
    counter=$((counter-1))
done

echo "blast off!!!"
```

**OR, this also works***

```bash
#!/bin/bash

# type out blastoff

counter=10

while [ $counter -ge 1 ]
do
    echo $counter
    counter=$((counter-1))
done

echo "blast off!!!"
```

#### 2. Argument reporting: 
You can find the length of an array using the notation: 
```bash
array=(file1.txt file2.txt file3.txt)

${#array[@]}
```
Knowing this, write a shell script called **printArgs.sh** that uses a while loop to print out all the arguments ($@) given on the command line. Examples of how printArgs.sh should work are:

```
$ bash printArgs.sh file1.txt file2.txt file3.txt
Your arguments are:
  $1 file1.txt
  $2 file2.txt
  $3 file3.txt
$ bash printArgs.sh gene exon start_site stop_site CDS ncRNA
Your arguments are:
  $1 gene
  $2 exon
  $3 start_site
  $4 stop_site
  $5 CDS
  $6 ncRNA
```

#### Argument reporting -- answer

```bash
#!/bin/bash

#Capture arguments in an array
arguments=($@)

#Initiate a counter
counter=0

#Start a while loop that runs for the number of elements in the arguments array
while [ $counter -lt ${#arguments[@]} ]
do
    echo "${arguments[$counter]}"
    ((counter++))  #Note, my notes previously had a bug and this was written $((counter++)) which will not work. counter=$((counter+1)) will work, however.
done
```


### for loop -- python style loop
#### 3. Element Names: 
Write a python style loop that loops through this array and prints out the names of of each element:

```bash
examplearray=(gene1 gene2 gene3 gene4 gene5 gene6);

#Write a for loop to print out each element of the array
```
#### Element Names -- ANSWER

```bash
#!/bin/bash

examplearray=(gene1 gene2 gene3 gene4 gene5 gene6);

#Write a for loop to print out each element of the array
for n in ${examplearray[@]}
do
    echo $n
done
```


#### 4. TXT to FASTQ: 
Download the tarball htsf\_demo\_dataset.tar.gz. This contains a bunch of example deep sequencing files from the UNC Sequencing facility. Typically, UNC gives you your results as .txt.gz even though these are fastq files. If you are not familiar with fastq files (the standard deep sequencing output file) you can read about it [here](https://en.wikipedia.org/wiki/FASTQ_format).

Can you write a script called transformTxtToFastq.sh that does the following...
  1. unzips each .txt.gz file.
  2. renames each .txt file so that the new file extension is .fastq (example:  Gm10847\_R1\_red\_head.txt will become Gm10847\_R1\_red\_head.fastq)
  3. prints out the first 8 lines of the file.
  3. counts the total lines in the file.
  3. Re-zips the .fastq files to .fastq.gz.

#### TXT to FASTQ -- ANSWER

```bash
#/bin/bash

#Can you write a script called transformTxtToFastq.sh that does the following...
#
#unzips each .txt.gz file.
#renames each .txt file so that the new file extension is .fastq (example: Gm10847_R1_red_head.txt will become Gm10847_R1_red_head.fastq)
#prints out the first 8 lines of the file.
#counts the total lines in the file.
#Re-zips the .fastq files to .fastq.gz.

files=($@)

echo "${#files[@]}"

for txtgzfile in ${files[@]}
do
    
    echo -e "$txtgzfile."
    
    #unzips each .txt.gz file.
        echo -e "\t\tUnzipping $txtgzfile."
        gunzip $txtgzfile
    
    #renames each .txt file so that the new file extension is .fastq (example: Gm10847_R1_red_head.txt will become Gm10847_R1_red_head.fastq)
        txtfile=${txtgzfile/.gz/}
        #echo -e "\t\ttext file is $txtfile"
        fastqfile=${txtfile/%.txt/.fastq}
        #echo -e "\t\fastqfile file is $fastqfile"
    
        echo -e "\t\tRenaming $txtfile as $fastqfile."
        mv $txtfile $fastqfile
        
    #prints out the first 8 lines of the file.
        echo -e "\t\tThe first lines of $fastqfile are:"
        head -n 8 $fastqfile
        
    #counts the total lines in the file.
        numlines=$(wc -l $fastqfile)
        echo -e "\t\tThe file $fastqfile contains $numlines lines."
        
    #Re-zips the .fastq files to .fastq.gz.
        echo -e "\t\tCompressing $fastqfile to ${fastqfile}.gz."
        gzip $fastqfile
    
        
        
done

```

#### 5. FASTX_TOOLKIT
Load the module fastx_toolkit. Read about fastx_toolkit on  [the fastx_toolkit website](http://hannonlab.cshl.edu/fastx_toolkit/commandline.html#fastq_statistics_usage).

The fastx\_toolkit has a function called fastx\_to\_fasta. This utility has a lot of possible bells and whistles, but the code is quite simple once you strip it down. Simply execute the command:

```bash
$ module load fastx_toolkit/0.0.13.2 
$ fastq_to_fasta -h
```

>**$ fastq_to_fasta -i** *\<infile.fastq\>* **-o** *\<outfile.fa\>* #Note, there was a bug here before. It was previously misspelled as fastq_to_fastq.


Write a script called fastqToFasta.sh that loops through all the fastq files in the directory htsf\_demo\_dataset and converts the fastq files to fasta files with the same root name but in a new folder:   
**Gm10847\_R1\_red\_head.fastq** will become **fasta_files/Gm10847\_R1\_red\_head.fa**

NOTE: Test this to make sure how it works. Make sure to retain a copy of the .fastq files for the extra credit exercise below.

#### FASTX TOOLKIT -- ANSWER

OK, this was a little trickier than I envisioned. Hopefully some googling will help the process along!

There are many ways to do this. Here is what I landed on...

```
# Write the program 
$ pwd 
/<myhomedirectory/06_week6/

$ ls -lh
-rw-r--r-- 1 erinosb employee 1.6K Aug  3 13:41 fastqToFasta.sh
drwxr-xr-x 2 erinosb employee 4.0K Aug  3 13:36 htsf_demo_dataset

# Call the function fastqToFasta.sh like so...

$ bsub -q week -n 1 -o %J.log "bash fastqToFasta.sh Gm10847_R1_red_head.fastq.gz Gm12753_R2_red_head.fastq.gz Gm12832_R1_red_head.fastq.gz Gm10847_R2_red_head.fastq.gz Gm12801_R1_red_head.fastq.gz Gm12832_R2_red_head.fastq.gz Gm10851_R1_red_head.fastq.gz Gm12801_R2_red_head.fastq.gz Gm12864_R1_red_head.fastq.gz Gm10851_R2_red_head.fastq.gz Gm12802_R1_red_head.fastq.gz Gm12864_R2_red_head.fastq.gz Gm12752_R1_red_head.fastq.gz Gm12802_R2_red_head.fastq.gz Gm12877_R1_red_head.fastq.gz Gm12752_R2_red_head.fastq.gz Gm12818_R1_red_head.fastq.gz Gm12877_R2_red_head.fastq.gz Gm12753_R1_red_head.fastq.gz Gm12818_R2_red_head.fastq.gz"


#There are other ways to do this. You could hard code the filenames into the code. You could read them from a separate file. or your could use *.fastq.gz or $ ls htsf_demo_dataset to get the list
```

Here is the code I came up with:

```bash
#!/bin/bash

#Write a script called fastqToFasta.sh that loops through all the fastq files in the directory htsf_demo_dataset and converts the fastq files to fasta files with the same root name but in a new folder:
#Gm10847_R1_red_head.fastq will become fasta_files/Gm10847_R1_red_head.fa


### USAGE   ####
#bsub -q week -n 1 -o %J.log "bash fastqToFasta.sh Gm10847_R1_red_head.fastq.gz Gm12753_R2_red_head.fastq.gz Gm12832_R1_red_head.fastq.gz Gm10847_R2_red_head.fastq.gz Gm12801_R1_red_head.fastq.gz Gm12832_R2_red_head.fastq.gz Gm10851_R1_red_head.fastq.gz Gm12801_R2_red_head.fastq.gz Gm12864_R1_red_head.fastq.gz Gm10851_R2_red_head.fastq.gz Gm12802_R1_red_head.fastq.gz Gm12864_R2_red_head.fastq.gz Gm12752_R1_red_head.fastq.gz Gm12802_R2_red_head.fastq.gz Gm12877_R1_red_head.fastq.gz Gm12752_R2_red_head.fastq.gz Gm12818_R1_red_head.fastq.gz Gm12877_R2_red_head.fastq.gz Gm12753_R1_red_head.fastq.gz Gm12818_R2_red_head.fastq.gz"


#Get the files to process
filenames=($@)

#Make a new directory
mkdir fasta_files

for fastqFile in ${filenames[@]}
do
    #Report the fastq file to process:
    echo -e "$fastqFile"
    
    #Make a backup file:
    bkpFile=${fastqFile}.bkp
    echo -e "\t\tbackup file is $bkpFile"
    cp htsf_demo_dataset/${fastqFile} htsf_demo_dataset/$bkpFile
    
    #Decompress the gzipped fastq file:
    unzipFastqFile=${fastqFile/.gz/}
    echo -e "\t\tUnzipped file is $unzipFastqFile"
    gunzip htsf_demo_dataset/$fastqFile
    
    #Make a fasta file:
    faFile=${unzipFastqFile/%.fastq/.fa}
    echo -e "\t\tfaFile is $faFile"
    
    #Convert the file from fastq to fasta using the fastx_toolkit utility
    fastq_to_fasta -Q33 -i htsf_demo_dataset/$unzipFastqFile -o fasta_files/$faFile
    
done

```

**NOTE** There is no mention of the -Q33 argument on the fastq_to_fasta manual page ($ fastq_to_fasta -h). So when I ran the original code without the -Q33 argument, i got this error message:

```
fastq_to_fasta: Invalid quality score value (char ')' ord 41 quality value -23) 
```

When I copied that sentence and google searched it, I got the following webpage which describes the -Q33 argument. This type of run-around, sadly, is typical.

[http://seqanswers.com/forums/showthread.php?t=7596](http://seqanswers.com/forums/showthread.php?t=7596)




#### 6 FASTX_TOOLKIT EXTRA CREDIT:

Follow the examples of how to produce two really pretty barplots using fastx\_toolkit in [its online manual] (http://hannonlab.cshl.edu/fastx_toolkit/commandline.html#fastq_info_example)

Write a script with a loop in it to produce the two plots for each of your .fastq files in the htsf\_demo\_dataset.


### Flow control

#### Usage statements.
Usage statements are typically paragraphs of information that are spit out when you try to execute a script with no arguments. 
For example, load the module bedtools and then look at what happens when you just execute:

```
$ bedtools 
#OR
$ bedtools getfasta
```

Begin a script called generateFactorFastas.sh. If no arguments are supplied to generateFactorFastas.sh, have it spit out a usage statement based on what you know about how this script should run in the [instructions for the group project](http://github.com/erinosb/bash_workshop_project/blob/master/instructions.md)

