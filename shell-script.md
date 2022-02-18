# Shebang
- ```#!```
- ```#!/bin/bash```
- Run the bash interpreter
-  If a script is named with the path ```path/to/script```, and it starts with the following line, ```#!/bin/sh```, then the program loader is instructed to run the program ```/bin/sh```, passing ```path/to/script``` as the first argument

# Variables
- All variables are stored as string, even numbers
- Double parantheses indicate a mathematical expression
- ```$x``` roughly translates to **value of x**
- Use ```$``` before double paranthese to evaluate mathematical expressions
```bash
#!/bin/bash

x=1+1
echo $x          # 1+1

x=$(( 1 + 1 ))  
echo $x         # 2

x=$(( $x + 5 ))
echo $x         # 7

echo -n "Input: "  # Input: myinput
read str          
echo str = $str    # str = myinput       
str="Dynamic use $str of string"
echo $str          # Dynamic use myinput of string 
```

# Command line arguments
- $* - command line arguments
- $# - number of arguments
- $n - nth argument

# for loop
Recursively print all files and directories
```bash
#!/bin/bash

for i in `ls -R`
do
    echo $i
done
```
