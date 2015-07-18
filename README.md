
# Basic Bash Scripting Cheatsheet




## What is a bash script?
A bash script is an excecutable file that contains a list of commands. A bash script's name is typically appended with the file extension .sh. The script is typically started with a shebang that answers the command line question 'which bash' and looks like so:

```bash
#!/bin/bash
```
    
With minor exceptions, anything you can run normally on the command line can be put into a script and it will do exactly the same thing.
Similarly, anything you can put into a script can also be run normally on the command line.


## Variables

Variables are placeholders for information. The information can either stay constant throughout the script, change every time the script is initiated, or change multiple times within the script. Variables help us to keep track of information by giving long things short names (nicknames) or by keeping track of something even though it may change thoroughout the script.


Basically, a variable is just a name that is given to a value. Values are assigned to their variable names using the syntax:

```bash
    homeDir="/nas02/home/e/r/erinosb"
    favoriteNumber=24
    favoriteLetter="X"
    favoriteQuote="Rich is the man whose needs are met and whose wants are few."
```

**Note! Don't put any spaces on either side of the = sign! This will result in an error and your variable will not be assigned the value you want.**

To access the varaible, use its symbol $variable

```bash
    echo $homeDir
    echo $favoriteNumber
    echo $favoriteLetter
    echo $favoriteQuote
```
    
Which outputs:

```
    "/nas02/home/e/r/erinosb"
    24
    "X"
    "Rich is the man whose needs are met and whose wants are few."
```


### array variables

A variable is a data structure. It is a way we store information. Most programming languages have several well-defined types of data structures. They have scalars (a single string of alphanumeric characters), arrays (ordered lists of alphanumeric characters), hashes (unordered pairs of keys and values), and many other complex types of data structures. Bash is way more simplistic than that. There are really just straight up variables. However, these variables come in two flavors. Regular old singleton varaibles have one value for each variable name. Arrays, on the other hand, are an ordered list of values that are assigned to one variable name.



## Special Variables

$0 - The name of the Bash script

$1 - $9 - The first 9 arguments to the Bash script

$# - How many arguments were passed to the Bash script

$@ - All the arguments supplied to the Bash script

$* - All the arguments supplied to the Bash script

$? - The exit status of the most recently run process


## Quoting

**Escape Character**    	**\**


A non-quoted backslash \ is the Bash escape character. It preserves the literal value of the next character that follows.
Example:
    var=23
    echo "$var"
    echo "\$var"
    
```bash
var=23
echo "$var"   #outputs    23
echo "\$var"  #outputs    $var
```
    
**Single Quotes**          **'**

Enclosing characters in single quotes preserves the literal value of each character within the quotes.
A single quote may not occur between single quotes, even when preceded by a backslash.


**Double Quotes**           **"**

Enclosing characters in double quotes preserves the literal value of all characters within the quotes, with the exception of $, `, \, and sometimes !. The characters $ and ` retain their special meaning within double quotes. The backslash retains its special meaning only when followed by one of the following characters: $, `, ", \, or newline. Backslashes preceding characters without a special meaning are left unmodified. A double quote may be quoted within double quotes by preceding it with a backslash.






### special variables

## Loops

### for loop -- python style

### for loop -- C Style

### while loop

## Flow control

### If

### Elsif

### Else
