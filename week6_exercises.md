
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


### for loop -- python style loop
#### 3. Element Names: 
Write a python style loop that loops through this array and prints out the names of of each element:

```bash
examplearray=(gene1 gene2 gene3 gene4 gene5 gene6);

#Write a for loop to print out each element of the array
```

#### 4. TXT to FASTQ: 
Download the tarball htsf\_demo\_dataset.tar.gz. This contains a bunch of example deep sequencing files from the UNC Sequencing facility. Typically, UNC gives you your results as .txt.gz even though these are fastq files. If you are not familiar with fastq files (the standard deep sequencing output file) you can read about it [here](https://en.wikipedia.org/wiki/FASTQ_format).

Can you write a script called transformTxtToFastq.sh that does the following...
  1. unzips each .txt.gz file.
  2. renames each .txt file so that the new file extension is .fastq (example:  JM1357\_UNC9\_1.txt will become JM1357\_UNC9\_1.fastq)
  3. Re-zips the .fastq files to .fastq.gz


#### 5. FASTX_TOOLKIT
Load the module fastx_toolkit. Read about fastx_toolkit on  [the fastx_toolkit website](http://hannonlab.cshl.edu/fastx_toolkit/commandline.html#fastq_statistics_usage).

The fastx\_toolkit has a function called fastx\_to\_fasta. This utility has a lot of possible bells and whistles, but the code is quite simple once you strip it down. Simply execute the command:


>**$ fastq_to_fastq -i** *\<infile.fastq\>* **-o** *\<outfile.fa\>*


Write a script called fastqToFastq.sh that loops through all the fastq files in the directory htsf\_demo\_dataset.tar.gz and converts them to fastq files with the same root name but in a new folder:   
**JM1357\_UNC9\_1.fastq** will become **fasta\_files/JM1357\_UNC9\_1.fa**



#### 6 FASTX_TOOLKIT EXTRA CREDIT:

Follow the examples of how to produce two really pretty barplots using fastx\_toolkit in [its online manual] (http://hannonlab.cshl.edu/fastx_toolkit/commandline.html#fastq_info_example)

Write a script with a loop in it to produce the two plots for each of your .fastq files in the htsf\_demo\_dataset.




