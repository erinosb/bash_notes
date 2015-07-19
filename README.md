
# Basic Bash Scripting Cheatsheet




## What is a bash script?
A bash script is an excecutable file that contains a list of commands. A bash script's name is typically appended with the file extension .sh. The script is typically started with a shebang. A shebang starts with #! and ends with the answer to the command line question 'which bash':

```bash
#!/bin/bash
```
    
With minor exceptions, anything you can run on the command line can run in a script.


## Variables

Variables are placeholders for information. The information can either stay constant throughout the script, change every time the script is initiated, or change multiple times within the script. Variables help us to keep track of information by assigning a nickname to things with long names, or by keeping track of something that may change value.


Variable names are how you call the value. You pick the variable name and you pick the value. You assign values to their variable names using the syntax:

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
    "/nas02/home/e/r/erinosb"
    24
    "X"
    "Rich is the man whose needs are met and whose wants are few."
```


### Array Variables

We have seen that Variables can be assigned one value but that is not all bash can do. Variables can also be assigned multiple ordered values. These are called arrays in other programming languages. An array is a variable containing multiple values. Any variable may be used as an array. There is no maximum limit to the size of an array, nor any requirement that member variables be indexed or assigned contiguously. Arrays are zero-based: the first element is indexed with the number 0.

Arrays are specified using parentheses.

```
    arrayname=(value1 value2 value3)
```

echo all the elements of an array using 

```
    ${arrayname[*]}
```
    --->    value1 value2 value3

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

Enclosing characters in double quotes preserves the literal value of all characters within the quotes, with the exception of $, \`, \, and sometimes !. The characters $ and \` retain their special meaning within double quotes. The backslash retains its special meaning only when followed by one of the following characters: $, \`, ", \, or newline. Backslashes preceding characters without a special meaning are left unmodified. A double quote may be quoted within double quotes by preceding it with a backslash.






### special variables

## Loops

### for loop -- python style

### for loop -- C Style

### while loop

## Flow control

### If

### Elsif

### Else
