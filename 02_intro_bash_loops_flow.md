# Bash Scripting Cheatsheet

## Loops

Let's say we have an array of items called files specified like so:

```bash
    files=(file1.txt file2.txt file3.txt)
```

Files contains a list of files that are in our working directory. How would we do an operation on each file? One way to do this is to use a for loop.

Well, we could easily just do this:

```bash
    wc $files[0]
    wc $files[1]
    wc $files[2]
```

That is perfectly fine to do! However, if you have 100 files, it may get kind of old. And also, you might make a typing error somewhere. There are a few different ways to loop things, but the main ones are while loops and for loops. We will look at one kind of while loop and two kinds of for loops.

### 1) While Loop

A while loop uses the format:


>while [ \<some test\> ]
>do
>    \<commands\>
>done

Typically, we start with a numberic counter, set it to 0, then start the loop. At the end of each pass through the loop we add one to our counter. The loop will run until the counter gets to be a certain size and then it stops. The way this works is like so:

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


### C-style for loop

For loops come in two main flavors. The first is the C-style for loop. This is the way that C is written and people just kep doing it this way. It is similar to a while loop.

In a while loop, we actually did three things:
INITIALIZATION -- When we set counter=0, we initiated the counter.
CONDITION -- When we checked whether $counter -lt 2, we were testing for a conditional statement
AFTERTHOUGHT -- when we added 1 to $counter, this is called an afterthough.

Those three steps are used in a C-style for loop in a slightly different way, like so:

for (INITIALIZATION; CONDITION; AFTERTHOUGHT) 
do
    <commands>
done

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
    
The syntax is very special within the double parentheses because it is basically mimicing "C".
If this doesn't make sense, just skip it.


### PYTHON-STYLE FOR LOOP.

A python style for loop is MUCH easier! It takes the form:
```
for var in ${array[@]}
do
    <commands>
done
```

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

## Flow control

### If

### Elsif

### Else
