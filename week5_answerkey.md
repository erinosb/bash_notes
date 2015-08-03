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

### Special variables -- ANSWER

```bash
#!/bin/bash

#People in my lab

labMembers=($@)

echo -e "You have ${#labMembers} in your lab. Members are ${labMembers[@]}."
```

```
$ bash labMembers.sh Max Sheera Adam Sophie Matt Erin
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
+ This directory contains some pretend microscopy data. Microscopes often take z-stacked images of time course data and save each image as a file. The files typically have some name that includes the stack, the time, and the sample name. Inspect the names of these 'files'.
+ There is also a bash script included. Read the bash script and try to modify it as suggested in the last line of the script.
+ You'll need to read about [sub-string replacements](https://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#substring-replacement) to answer this question.

## Homework exercise-5-2
+ Write a script called **TxtToFastq.sh** that takes in an a text file (file1.txt) as an argument and prints to the screen the name **file1.fastq**.
+ This seems like it should be easy but it is a little tricky for one reason... bash gets confused about how to *echo* or *printf* things that have characters right next to the output with no spaces.
+ Try using the notation ${variable} instead of $variable when you *echo* or *prinf* and see whether this helps.

## Homework exercise-5-3
+ Imaginge you have a tab delimited file or a comma delimited file. These files typically contain spread-sheet like data. You can save a 'column' of information as an array by combining the 'cut' function with the notation:
    + array=($(\<command\>))
+ Can you save a column of information as an array? Make sure to test that you have captured the expected number of individual elements. Also test that ${array[1]} gives you what you expect. 
+ If you need a sample file, try Scerevisiae_TFs.csv from a previous homework exercise.



  



