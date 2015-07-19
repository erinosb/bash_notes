
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


Basically, a variable is just a name that is given to a value. Values are assigned to their variable names using the syntax

    varname="value"
    
And then the value can be accessed by calling the variable using a dollar sign in front of it like so:

    echo $varname
    
For example

```bash
    #!/bin/bash
    
    #this is a script name assignVariable.sh
    
    varname="value"
    echo $varname
```

If you were to execute this script, it would look like this:

    $ bash assignVariable.sh
    value

Values can be letters, numbers, symbols, spaces, special characters, returns, etc. Simple things can be assigned without quotes, but complex things (especially spaces) require quotes.

**Note! Don't put any spaces on either side of the = sign! This will result in an error and your variable will not be assigned the value you want.**

```bash
    homeDir="/nas02/home/e/r/erinosb"
    favoriteNumber=24
    favoriteLetter="X"
    favoriteQuote="Rich is the man whose needs are met and whose wants are few."
```


To access the varaible, use its symbol $variable

```bash
    echo $homeDir
    echo $favoriteNumber
    echo $favoriteLetter
    echo $favoriteQuote
```
    
Which outputs:

```
    /nas02/home/e/r/erinosb
    24
    X
    Rich is the man whose needs are met and whose wants are few.
```

Variables can be re-assigned with new values at any time. Because bash scripts are read from top to bottom, the variable will have the new value in any lines below the reassignment:

```bash
    favoriteBook="Jane Eyre"
    echo "my favorite book is $favoriteBook"
    
    favoriteBook="Midnight's Children"
    
    echo "my new favorite book is $favoriteBook"
    
```

This script outputs:

```
    my favorite book is Jane Eyre
    my new favorite book is Midnight's Children
```

### Array Variables

So far, we have seen one value be assigned to each varaible names. We can also assign multiple, ordered values to a single variable name. These create array varaibles. Arrays are zero-based: the first element is indexed with the number 0. There is no maximum limit to the size of an array, nor any requirement that member variables be indexed or assigned contiguously. 

To assign array variables, we use parentheses:

```
    arrayname=(value1 value2 value3 value4)
```

This array has four values, also called elements.
To see all elements, we use this syntax:

```
    echo ${arrayname[*]}    #outputs: value1 value2 value3 value4
```

Alternatively, you can populate an array using the 'index number'. Here is an array variable called "cities" with multiple values set to the names of local cities:

```
    cities[0]="Chapel Hill"
    cities[1]="Durham"
    cities[2]="Apex"
```

We can access this array, again using an echo statement and an * but you can also access any value using the index number as well...

```
    echo ${cities[*]}           #outputs:   Chapel Hill Durham Apex
    echo ${cities[0]}           #outputs:   Chapel Hill
    echo ${cities[2]}           #outputs:   Apex
```

**Tips on naming variables (arrays or regular)**
+ First character should be a character
+ Following characters can be characters or numerals
+ Avoid any special/weird characters
+ Avoid all caps
    + Environmental variables in bash are in all caps
    + To see environmental variables list:
    + $ printenv
    + $ echo $PATH




### Special Variables

Some variables are already made for you. Some of these, like environmental variables existed before you even started your script. These are variables like $PATH and other variables that printout when you type $ prinenv. Other variables are initiated when you execute your code. These special variables are useful for getting information into your script.

$0 - The name of the Bash script

$1 - $9 - The first 9 arguments to the Bash script

$# - How many arguments were passed to the Bash script

$@ - All the arguments supplied to the Bash script

$* - All the arguments supplied to the Bash script

$? - The exit status of the most recently run process

For example, if you executed your code like so...
```
    user:erin$ bash testcode.sh file1.txt file2.txt file3.txt
```

Then, 

```bash
    echo $0         #outputs: testcode.sh
    echo $1         #outputs: file1.txt
    echo $2         #outputs: file1.txt
    echo $@         #outputs: file1.txt file2.txt file3.txt
    echo $#         #outputs: 3
```


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

Enclosing characters in double quotes preserves the literal value of all characters within the quotes, with the exception of $, \`, \, and sometimes !. The characters $ and \` retain their special meaning within double quotes. The backslash retains its special meaning only when followed by one of the following characters: $, \`, ", \, or newline. Backslashes preceding characters without a special meaning are left unmodified. A double quote may be quoted within double quotes by preceding it with a backslash.

To illustrate the difference between single and double quotes, check this out:

```bash
    color=red
    favoritecolor=$color
    echo $favoritecolor         #outputs:   red
    
    favoritecolor='$color'
    echo $favoritecolor         #outputs:   $color
    
    favoritecolor="$color"
    echo $favoritecolor         #outputs:   red
```



## Loops

### for loop -- python style

### for loop -- C Style

### while loop

## Flow control

### If

### Elsif

### Else
