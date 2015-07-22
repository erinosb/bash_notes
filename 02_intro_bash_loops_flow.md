# Bash Scripting Cheatsheet




## Loops

Let's say we have an array of items called files specified like so:

```bash
    files=(file1.txt file2.txt file3.txt)
```

Files contains a list of files that are in our working directory. How would we do an operation on each file?  Well, we could easily just do this:

```bash
    wc $files[0]
    wc $files[1]
    wc $files[2]
```

That is perfectly fine to do. However, if you have 100 files, it may get kind of old. Also, you might make a typing error somewhere. A better way would be to use a loop. There are a few different kinds of loops but the main ones are **while loops** and **for loops**. We will look at one kind of while loop and two kinds of for loops.

### 1) While Loop

A while loop uses the format:


>**while [** *\<some test\>* **]**   
>**do**   
>    *\<commands\>*   
>**done**

Typically, start with a numberic counter, set it to 0, then start the loop. At the end of each pass through the loop increment the counter by one. The loop will run until the counter gets to be a certain size that fails the test and then it stops. The way this works is like so:

```bash
    files=(file1.txt file2.txt file3.txt)
    counter=0                   # Start a counter
    
    while [ $counter -le 2 ]    # Start a while loop that will go AS LONG AS $counter is Less than or Equal to 2
    do                          
        echo $counter           # Print what $counter is set to
        echo ${files[$counter]} # Print the element of files associated with the $counter value
        wc ${files[$counter]}   # Count the number of words in that file
        echo -e "\n"
        (($counter++))          # Add one to the counter
    done            
```


This loop outputs the following:
```
0
file1.txt
      15      13      47 file1.txt


1
file2.txt
       5       5      36 file2.txt


2
file3.txt
       4       3      24 file3.txt
```
For each pass through the loop, it prints what $counter represents, it prints the element within the files array that corresponds to the number that $counter represents, and it counts the words within that file.

### 2) C-style for loop

For loops come in two main flavors. The first is the C-style for loop. This is the way that C is written and people just kept doing it this way. It is similar to a while loop. I personally, don't use C-style loops very often, but they are useful to illustrate that while loops and for loops do the same thing.

In a while loop, we actually did three things:
+ INITIALIZATION -- When we set counter=0, we initiated the counter.
+ CONDITION -- When we checked whether $counter -lt 2, we were testing for a conditional statement
+ AFTERTHOUGHT -- when we added 1 to $counter, this is called an afterthough.

Those three steps are used in a C-style for loop in a slightly different way, like so:

>**for ((** *\<INITIALIZATION\>; \<CONDITION\>; \<AFTERTHOUGHT\>* **))**   
>**do**   
>     *\<commands\>*   
>**done**

Here is an example of the same loop in a C-style:

```bash

    files=(file1.txt file2.txt file3.txt)

    for (( counter=0; counter <= 2; counter++ ))
    do
        echo $counter
        echo ${files[$counter]}
        wc ${files[$counter]}
        echo -e "\n"
    done
```
    
The syntax within the double parentheses is very special because it is basically mimicking "C". Don't worry if it seems to look weird.
If this doesn't make sense, just skip it and move on to Python-style loops. You can totally live without C-style loops.


### 3) Python-style loop

A python style for loop is MUCH easier! It takes the form:

>**for** *\<var\>* **in $\{***\<array\>***[@]\}**  
>**do**   
>    *\<commands\>*   
>**done**   


In this type of loop "for" is a command that is typed literally. "in" is also a command that is typed literally. "var" is a variable name you choose. <array> is an array variable you have probably already defined. "do" and "done" are also command words that are typed literally.

An example of a python style C loop is:

```bash
    files=(file1.txt file2.txt file3.txt)

    for singleFile in ${files[@]}
    do
        echo $singleFile
        wc $singleFile
        echo -e "\n"
    done
```

This gives the following output. Notice we get to skip the counter altogether:

```
file1.txt
      15      13      47 file1.txt


file2.txt
       5       5      36 file2.txt


file3.txt
       4       3      24 file3.txt
```

The python-style for loop is probably the most common loop you'll end up using. However, there are times when having a counter can come in useful. So it is not ideal for all tasks.

## A word about tests

Before we get deep into flow control, we're going to need to learn about **tests**. Tests are statements we can give to the bash program to ask it whether something is true or false. Tests in bash typically happen between square brackets **[ and  ]**. We have seen one example of this already. In the **while** loop, there is a square bracket test we performed that looked like this...

```bash
    while [ $counter -le 2 ]    # Start a while loop that will go AS LONG AS $counter is Less than or Equal to 2
    do                          
        echo $counter           # Print what $counter is set to
        (($counter++))          # Add one to the counter
    done   
    
```

In that exampel `[$counter -le 2]` is a test. If $counter points to a value less than or equal to 2, the test is **TRUE** and the loop continues. If it is greater than 2, the test is **FALSE** and the while loop beraks.

When we start doing *if* and *else* statements, we'll do more tests. Here are some tests that can go between square brackets:

! *\<EXPRESSION\>*              # The EXPRESSION is false.   
-n *\<STRING\>*                 # The length of STRING is greater than zero.   
-z *\<STRING\>*	                # The lengh of STRING is zero (ie it is empty).   
*\<STRING1\>* = *\<STRING2\>*	# STRING1 is equal to STRING2   
*\<STRING1\>* != *\<STRING2\>*            # STRING1 is not equal to STRING2   
*\<INTEGER1\>* -eq *\<INTEGER2\>*	# INTEGER1 is numerically equal to INTEGER2   
*\<INTEGER1\>* -gt *\<INTEGER2\>*	# INTEGER1 is numerically greater than INTEGER2   
*\<INTEGER1\>* -lt *\<INTEGER2\>*	# INTEGER1 is numerically less than INTEGER2   
*\<INTEGER1\>* -ge *\<INTEGER2\>*	# INTEGER1 is numerically greater than or equal to INTEGER2   
*\<INTEGER1\>* -le *\<INTEGER2\>*	# INTEGER1 is numerically less than or equal to INTEGER2   
-e *\<FILE\>*	                            # FILE exists.    
-s *\<FILE\>*               # FILE exists and it's size is greater than zero (ie. it is not empty).   


## Flow control

Imagine the way that your commands are executed through a bash script. The script starts at the top and executes commands going down the script to the bottom. In the "loops" section, we learned how a script can start at the top, flow down to a loop, spin around in a loop, and then continue on to the bottom of a script.

There are other ways to optimize the path command execution takes through a script. Flow control involves skipping over different sections. In flow control, we can conditionally execute blocks of code or ignore them entirely. 

### 1) If

### 2) Elsif

### 3) Else
