
# Basic Bash Scripting Cheatsheet


____

[**What is a bash script?**](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#what-is-a-bash-script)

[**Variables**](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#variables)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Array Variables](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#array-variables)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Special Variables](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#special-variables)

[**Quoting**](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#quoting)

[**Commands**](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#commands)

[**Input**](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#input)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Hard wiring](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#hard-wiring)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Arguments](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#arguments)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Reading Standard Input](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#reading-standard-input)

[**Output**](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#output)

[**Substring Replacement**](http://github.com/erinosb/bash_notes/blob/master/01_intro_bash_variables.md#substring-replacement)

____

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
    favoriteNumber=42
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
    42
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

### Capturing output as variables

You can capture the output of a command as a variable like so:

```bash
variable=$(date)
```

You can capture the output of a numerical operation as a variable with double parentheses like so:

```bash
variable=$((49 + 50))
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

Some variables are already made for you. Some of these, like environmental variables existed before you even started your script. These are variables like $PATH and other variables that printout when you type $ prinenv. Other variables are initiated when you execute your code. These special variables are useful for accessing any arguments that you supplied when you executed your script.

+ $0 - The name of the Bash script
+ $1 - $9 - The first 9 arguments to the Bash script
+ $# - How many arguments were passed to the Bash script
+ $@ - All the arguments supplied to the Bash script
+ $* - All the arguments supplied to the Bash script
+ $? - The exit status of the most recently run process

For example, if you executed your code like so...
```
$ bash testcode.sh file1.txt file2.txt file3.txt
```

Then, 

```bash
    echo $0         #outputs: testcode.sh
    echo $1         #outputs: file1.txt
    echo $2         #outputs: file2.txt
    echo $@         #outputs: file1.txt file2.txt file3.txt
    echo $*         #outputs: file1.txt file2.txt file3.txt
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



**Curly brackets**          **{**

OK, these aren't quite quotes, but they help when quoting. Say you have a variable called $file that has the value 150702\_analysis and you want to dereference that variable to make the output 150702\_analysis\_log.txt and 150702\_analysis\_matrix.xlsx you are going to confuse things. If you want to put the value right up next to some text, use the curly brackets to explicitly dereference the variable:

```bash
    file=150702_analysis
    echo -e "Will save output as ${file}_log.txt and ${file}_matrix.xlsx"
```
    
This will output:
```
Will save output as 150702_analysis_log.txt and 150702_analysis_matrix.xlsx"
```



## Commands

Any shell command you give on the command line should work inside of a bash script.
You can execute any command simply by listing it on its own line:

```bash
    ls                  #output: will list the contents of the current working directory
    date                #output: will spit out the date
    wc file1.txt        #output: will count the number of lines in file1.txt IF file1.txt is in your working directory.
```

In addition, you can **capture** the output of a command into a variable! Cool! To do so, use $().

```bash
    contents=$(ls)
    echo $contents      #output: will list the contents of the current working directory
```


## Input

Getting things into and out of a shell script is really important. There are many ways to get information into shell scripts. Mostly, the only information we give shell scripts are alphanumeric names of things. 

#### Hard wiring
One, maybe obvious, way we can get information into a script is simply by typing it in there. For example, if I want to tell a script to count the lines in a document called file1.txt, I can just write it that way, like so:

```bash
    wc file1.txt
```

That's easy. I just wrote file1.txt into the code. But what if I want to change the file to count without re-writing my code? I'll need a better, more interactive strategy. The most popular is taking arguments on the command line:

#### Arguments

Let's say we have a file called file2.txt which is 10 lines long. Let's say we want to write a script that will count the number of lines in this file. We can write a script called counter.sh that takes the file name as an argument. This is done like so...

> **$ bash** *\<scriptname.sh\>* *[firstArgument]* *[secondArgument]*

```
$ bash counter.sh file2.txt
```

If we look inside the counter.sh script, it will look like this:

```bash
    #!/bin/bash
    
    wc $1       #output: the word count of any file given as the first argument to the script
```

This works because $1 is a special character that stands in for the first argument given on the command line. Anything that comes after the script's name and a space, will be captured as $1 and sent into the script as $1.

#### Reading Standard Input

Standard input is anything the user types into the computer at the keyboard. You can prompt the user for standard input using a command called `read`.

You'll need to experiment with this a little bit, but the syntax is:

```bash
    echo "what is your favorite food?"
    read favoritefood
    echo "Ah! I also like $favoritefood."
```

## Output

There are a lot of ways to move information out of a bash script. Mostly, we've been usign echo or printf to do this. By using echo or printf we can print information to the screen. This screen is called STANDARD OUT also known as OUTPUT 1. In addition to printing to standard out, we can print to a file.

To print to a file for the first time, Use 1> the redirect symbol:

```bash
    echo -e "This is s a test" 1>outputfile.txt
```

This will create a file called outputfile.txt and write the test "This is a test" to it. "This is a test" will not appear on the screen. 

If you want to add more content to the end of outputfile.txt, use 1>> like so...

```bash
    echo -e "This is s a test" 1>outputfile.txt
    echo -e "More content" 1>>outputfile.txt
```

Both lines will now appear in the file outputfile.txt.

Sometimes you want things to print out to the screen and to the desired file. In this case, you can use a  chain of commands that looks like `| tee -a `:


```bash
    echo -e "still more to say"  | tee -a outputfile.txt
```

This will both print "still more to say" to the screen and append it to the output file.

## Substring replacement
A series of numbers, letters, special characters, and spaces is called a **string**. Variables often point to values that are strings. Sometimes we want to do operations on those strings. We can do this using sub-string operations on variables.

Some cool tricks:


>**Subset a string**   
>*\<newvarname\>***=${***\<oldvarname\>***:***\<n\>***}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make a new variable $newvar that corresponds to the $var string starting at nth letter.   
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: **newvar=${oldvar:3}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: If $oldvar is "California" $newvar is "ifornia"  
>  
>**Subset a string of specific length**   
>*\<newvarname\>***=${***\<oldvarname\>***:***\<n\>***:***\<length\>***}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make a new variable $newvar that corresponds to the $oldvar string starting at nth letter and going for "length" letters.  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: **newvar=${oldvar:3:4}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: If $oldvar is "California" $newvar is "ifor"  
>   
>**Replace a sub-string**   
>*\<newvarname\>***=${***\<oldvarname\>***/***\<pattern\>***/***\<replacement\>***}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make a new variable $newvar that replaces one instance of "pattern" in $oldvar with "replacement".  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: **newvar=${oldvar/nia/nian}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: If $oldvar is "California" $newvar is "Californian"  
>   
>**Globally replace a sub-string**   
>*\<newvarname\>***=${***\<oldvarname\>***//***\<pattern\>***/***\<replacement\>***}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make a new variable $newvar that replaces **ANY** instance of "pattern" in $oldvar with "replacement".  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: **newvar=${oldvar//a/A}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: If $oldvar is "California" $newvar is "CAliforniA"  
>   
>**Replace a prefix**   
>*\<newvarname\>***=${***\<oldvarname\>***/#***\<pattern\>***/***\<replacement\>***}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make a new variable $newvar that replaces "pattern" at the BEGINNING of the string $oldvar with "replacement".  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: **newvar=${oldvar/#To/So}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: If $oldvar is "To be or not to be" $newvar is "So be or not to be"  
>   
>**Replace a suffix**   
>*\<newvarname\>***=${***\<oldvarname\>***/%***\<pattern\>***/***\<replacement\>***}** 
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make a new variable $newvar that replaces "pattern" at the END of the string $oldvar with "replacement".  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: **newvar=${oldvar/%txt/fastq}**  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: If $oldvar is "file1.txt" $newvar is "file1.fastq"  
>
