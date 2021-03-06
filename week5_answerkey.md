# Exercises for Week 5


## Variables

+ write a script called **favoriteThings.sh**
+ Within this script, assign values to the following variables that correspond to your favorite things:
    + $name
    + $favoriteFood
    + $favoriteBook
    + $favoriteMovie
    + $favoriteEnzyme
+ Now have the script output the following statements with your values filling in the blanks:


```
    My name is ____.
    My favorite food is ____.
    My favorite Book is ____.
    My favorite Movie is ____.
    My favorite Enzyme is _____.
```


## Variables -- ANSWER

```bash
#!/bin/bash

# A list of my favorite things

# assign values to the following variables that correspond to your favorite things
name="Erin Osborne Nishimura"
favoriteFood="guacamole"
favoriteBook="Jane Eyre"
favoriteMovie="Howard and Maude"
favoriteEnzyme="DNA Polymerase"

#Now have the script output the following statements with your values filling in the blanks:
echo -e "My name is $name."
echo -e "My favorite food is $favoriteFood."
echo -e "My favorite Book is $favoriteBook."
echo -e "My favorite Movie is $favoriteMovie."
echo -e "My favorite Enzyme is $favoriteEnzyme."

#Alternatively, this is also a good technique. The curly brackets explicitly put your variable names in parentheses and avoid confusion with any of the surrounding text.
echo -e "My name is ${name}."
echo -e "My favorite food is ${favoriteFood}."
echo -e "My favorite Book is ${favoriteBook}."
echo -e "My favorite Movie is ${favoriteMovie}."
echo -e "My favorite Enzyme is ${favoriteEnzyme}."
```

## Array variables
+ write a script called **labMembers.sh**
+ within this script, assign values to an array variable that corresponds to the names of people in your lab. 
  labMembers=()
+ Have the script output the following information by accessing the value of each element numbered indices:

  "You have # in your lab. Members are ____, ____, ___."
  
  For example, mine would be: "You have 6 people in your lab. Members are Sheera, Max, Sophie, Adam, Matt, and Erin."
  
  The tricky part will be to figure out how you would have the script count the number of elements in your array? Google search this to find it out.
  
## Array variables -- ANSWER

```bash
#!/bin/bash

#People in my lab

labMembers=(Sheera Max Matt Erin Adam Sophie)

echo -e "You have ${#labMembers} in your lab. Members are ${labMembers[@]}."
```

### Special variables

+ Open up labMembers.sh and comment out the line where you assigned your array variable labMembers (put a # sign in front of this line). Instead, feed the script the name of your lab members as arguments when you execute the script like so:
+ Re-write the labMembers.sh script so that it continues to work as before, this time with the command line arguments.
+ 
```
$ bash labMembers.sh Max Sheera Adam Sophie Matt Erin
```

### Special variables -- ANSWER

```bash
#!/bin/bash

#People in my lab

labMembers=($@)

echo -e "You have ${#labMembers} in your lab. Members are ${labMembers[@]}."
```



### Quoting

+ Go back to your favoriteThings.sh script. This time, have your script print out the following output (filling in your personal values in the blanks:

```
The variable $name has the value _____.
The variable $favoriteFood has the value ____.
The variable $favoriteBook has the value ____.
The variable $favoriteMovie has the value ____.
The variable $favoriteEnzyme has the value ____.
```

### Quoting -- ANSWER

```bash
#!/bin/bash

# A list of my favorite things

# assign values to the following variables that correspond to your favorite things
name="Erin Osborne Nishimura"
favoriteFood="guacamole"
favoriteBook="Jane Eyre"
favoriteMovie="Howard and Maude"
favoriteEnzyme="DNA Polymerase"

#Now have the script output the following statements with your values filling in the blanks:
echo -e "The variable \$name is $name."
echo -e "The variable \$favoriteFood is $favoriteFood."
echo -e "The variable \$favoriteBook is $favoriteBook."
echo -e "The variable \$favoriteMovie is $favoriteMovie."
echo -e "The variable \$favoriteEnzyme is $favoriteEnzyme."
```

## Homework exercise-5-1

+ Download the file microscopy.tar.gz from the [week5 wepage](http://onish.web.unc.edu/week5)
+ Unpackage the tarball and navigate into the directory.

```
#On the command line:
$ mv microscopy.tar_.gz microscopy.tar.gz
$ tar -zxvf microscopy.tar.gz 
```

+ This directory contains some pretend microscopy data. Microscopes often take z-stacked images of time course data and save each image as a file. The files typically have some name that includes the stack, the time, and the sample name. Inspect the names of these 'files'.
+ There is also a bash script included. Read the bash script and try to modify it as suggested in the last line of the script.
+ You'll need to read about [sub-string replacements](https://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#substring-replacement) to answer this question.
+ 
```bash 

# This technique spits out a lot of errors but it gets the job done. We'll learn more elegant solutions next week.
# There are lots of possible ways to do this.

#!/bin/bash

#transform_names.sh
#Author:  Erin Osborne Nishimura
#Date:    July 17, 2015
#Purpose: My collaborator keeps sending me directories full of microscopy data with spaces in them! How infuriating. I want to write a script that will remove spaces from filenames and replace those spaces with underscores. This code will capture all .tif files in the working directory, search them for spaces, and replace those spaces with underscores.


#This sets the internal file separator to a newline. Don't worry about understanding this part at this point.
IFS=$'\n'

#This captures all the .tif files in the directory within an array called filesArray
filesArray=($(ls *.tif))


#Assignment: Can you hack this code to replace "glob-color1" with "GFP" and "glob-color2" with "mCherry"?
for file in ${filesArray[@]}
do
    #For each element of the array, the code below replaces any " " strings with "_"
    newfile=${file/glob-color1/GFP}
    
    #This tells the user what will be replaced
    echo "Renaming $file to $newfile"
    
    mv $file $newfile
    newfile=${file/glob-color2/mCherry}
    

    #This tells the user what will be replaced
    echo "Renaming $file to $newfile"
    
    #This renames the file to the new name
    mv $file $newfile
    
done
```

## Homework exercise-5-2
+ Write a script called **TxtToFastq.sh** that takes in an a text file (file1.txt) as an argument and prints to the screen the name **file1.fastq**.
+ This seems like it should be easy but it is a little tricky for one reason... bash gets confused about how to *echo* or *printf* things that have characters right next to the output with no spaces.
+ Try using the notation ${variable} instead of $variable when you *echo* or *prinf* and see whether this helps.

```bash
#!/bin/bash

#First method:
#take in file1.txt and print to screen file1.fastq

file=$1

newfile=${file/%.txt/.fastq}

echo $newfile



#Second method:
#take in file1.txt and print to screen file1.fastq

file=$1

rootfile=${file%%.txt}
echo -e "${rootfile}.fastq"
```

## Homework exercise-5-3
+ Imaginge you have a tab delimited file or a comma delimited file. These files typically contain spread-sheet like data. You can save a 'column' of information as an array by combining the 'cut' function with the notation:
    + array=($(\<command\>))
+ Can you save a column of information as an array? Make sure to test that you have captured the expected number of individual elements. Also test that ${array[1]} gives you what you expect. 
+ If you need a sample file, try Scerevisiae_TFs.csv from a previous homework exercise.

**getColumn.sh**

```bash
#!/bin/bash

#Get files
file=$1

#Get column
idarray=($(cut -d ',' -f 1 $file | tail -n +2 ))

echo -e "${#idarray[@]}"
echo -e "${idarray[0]}"
echo -e "${idarray[1]}"
```

  
**On the command line, this looks like**


```

$ head Scerevisiae_TFs.csv 
"ID","Name","Species","GeneID","Family","Evidence"
"T000176_1.01","ABF1","Saccharomyces_cerevisiae","YKL112W","ABF1","D"
"T000387_1.01","AFT1","Saccharomyces_cerevisiae","YGL071W","AFT","D"
"T000388_1.01","AFT2","Saccharomyces_cerevisiae","YPL202C","AFT","D"
"T005322_1.01","MBP1","Saccharomyces_cerevisiae","YDL056W","APSES","D"
"T005325_1.01","PHD1","Saccharomyces_cerevisiae","YKL043W","APSES","D"
"T005326_1.01","SOK2","Saccharomyces_cerevisiae","YMR016C","APSES","D"
"T005323_1.01","SWI4","Saccharomyces_cerevisiae","YER111C","APSES","D"
"T005324_1.01","XBP1","Saccharomyces_cerevisiae","YIL101C","APSES","D"
"T008770_1.01","SUM1","Saccharomyces_cerevisiae","YDR310C","AT hook","D"

$ wc Scerevisiae_TFs.csv 
  255   359 18872 Scerevisiae_TFs.csv
  
$ bash getColumn.sh Scerevisiae_TFs.csv 
254
"T000176_1.01"
"T000387_1.01"
```


