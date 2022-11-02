# Bash scripting - reusing your code

This is obviously too deep of a conversation for a single markdown file, but I'm going to throw in a cheat-sheet-style list here of things that I find interesting or otherwise didn't know as I go along, I have previous scripting experience so the level of detail you require my vary, but addition resources are available online, and just a google away. 

Bash is unlike other programming languages in that you are scripting at the Operating System level, so you are then possibly going to run into multiple languages being used in a single script, for instance, with the awk command.

# Defining functions
simply naming the function, followed by () and the code for your function in {} to define a function

Example:
```bash
# Defines the usage() function
usage () {
    echo "usage: $0 <case number>"
    echo "Simple script to create case folder and start listeners"
    exit 1
}
```

# Arguments
Arguments are found in the environment variables indexed by their position starting with the file name located at $0, so argument 1 will be accessible through $1

Example:
```bash
#output the file name
echo $0

#output the first argument
echo $1

#find the number of arguments given 
echo $#

# Use that to validate an argument was given
# spacing is important to bash
if [ $# -lt 1 ] ; then
    usage
else
    echo "Starting case $1"
# signifies the end of an if statement
fi
```

# Checking for a directory
Example:

```bash
# ! is the NOT operator, -d checks for directories, and $1 matches it to the argument passed to the script
# So if the directory matching the argument passed to the script doesn't exist, it will create it
if [ ! -d $1 ] ; then
    mkdir $1
fi
```

# Other conditional expressions
```-f``` checks if the file exists and it’s a regular file.

```-d``` checks if the argument provided was a directory.

```-h``` checks if the argument provided was a symbolic link.

```-s``` checks if the file exists and is not empty.

```-r``` check if the file is readable.

```-w``` check if the file is writable.

```-x``` check if the file is executable.