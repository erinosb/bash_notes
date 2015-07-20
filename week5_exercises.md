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

## Array variables
+ write a script called **labMembers.sh**
+ within this script, assign values to an array variable that corresponds to the names of people in your lab. 
  labMembers=()
+ Have the script output the following information by accessing the value of each element numbered indices:

  "You have # in your lab. Members are ____, ____, ___."
  
  For example, mine would be: "You have 6 people in your lab. Members are Sheera, Max, Sophie, Adam, Matt, and Erin."
  
  The tricky part will be to figure out how you would have the script count the number of elements in your array? Google search this to find it out.

### Special variables

+ Open up labMembers.sh and comment out the line where you assigned your array variable labMembers (put a # sign in front of this line). Instead, feed the script the name of your lab members as arguments when you execute the script like so:

```
$ bash labMembers.sh Max Sheera Adam Sophie Matt Erin
```
+ Re-write the labMembers.sh script so that it continues to work as before, this time with the command line arguments.

### Quoting

+ Go back to your favoriteThings.sh script. This time, have your script print out the following output (filling in your personal values in the blanks:

```
The variable $name has the value _____.
The variable $favoriteFood has the value ____.
The variable $favoriteBook has the value ____.
The variable $favoriteMovie has the value ____.
The variable $favoriteEnzyme has the value ____.
```

## Homework exercise-5-1

+ Download the file microscopy.tar.gz from the [week5 wepage](http://onish.web.unc.edu/week5)
+ Unpackage the tarball and navigate into the directory.
+ This directory contains some pretend microscopy data. Microscopes often take z-stacked images of time course data and save each image as a file. The files typically have some name that includes the stack, the time, and the sample name. Inspect the names of these 'files'.
+ There is also a bash script included. Read the bash script and try to modify it as suggested in the last line of the script.
+ You'll need to read about [sub-string replacements](https://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#substring-replacement) to answer this question.

## Homework exercise-5-2
+ Imaginge you have a tab delimited file or a comma delimited file. These files typically contain spread-sheet like data. You can save a 'column' of information as an array by combining the 'cut' function with the notation:
    + array=($(<command>))
+ Can you save a column of information as an array? Make sure to test that you have captured the expected number of individual elements. Also test that ${array[1]} gives you what you expect. 
+ If you need a sample file, try Scerevisiae_TFs.csv from a previous homework exercise.



  



