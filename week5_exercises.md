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





  



