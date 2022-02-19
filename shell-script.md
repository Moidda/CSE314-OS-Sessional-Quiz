# Hot
> [Variables](#variables) \
> [Command Line args](#command-line-arguments-and-if-else) \
> [If-else](#command-line-arguments-and-if-else) \
> [Loop](#for-loop) \
> [Function](#function)

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

# Command line arguments and if-else
- $* - command line arguments
- $# - number of arguments
- $n - nth argument 

Run the following **script.sh**: ```./script.sh hello world```
```bash
#!/bin/bash
if [[ $# -eq 1 ]];
then
    echo "No of arguments = 1"
    echo "arg1 = $1"
elif [[ $# -eq 2 ]];
then
    echo "No of arguments = 2"
    echo "arg1 = $1"
    echo "arg2 = $2"
else
    echo "Exiting program"
    exit
fi
```
Output:
```bash
No of arguments = 1
arg1 = hello
arg2 = world
```

# for loop
Recursively print all files and directories
```bash
#!/bin/bash

for i in `ls -R`
do
    echo $i
done
```

# Function
## Passing Parameters
- ```$#, $*``` are replaced by parameters inside function call
- After finishing function call, these are again replaced by command line arguments
- ```script.sh```:
    ```bash
    myfun() {
        echo "Parameter count = $#"
        i=0
        for param in $*
        do
            i=$(( $i + 1 ))
            echo "Param$i = $param"
        done
    }

    echo "Before function call"
    echo "Arg count = $#"
    i=0
    for arg in $*
    do
        i=$(( $i + 1 ))
        echo "Arg$i = $arg"
    done

    myfun func params

    echo "After function call"
    echo "Arg count = $#"
    i=0
    for arg in $*
    do
        i=$(( $i + 1 ))
        echo "Arg$i = $arg"
    done
    ```
- ```./script.sh Hello world``` 
- Output:
    ```
    Before function call
    Arg count = 2
    Arg1 = Hello
    Arg2 = World
    Parameter count = 2
    Param1 = func
    Param2 = params
    After function call
    Arg count = 2
    Arg1 = Hello
    Arg2 = World
    ```

## Return Values
script.sh:
```bash
my_function () {
  local func_result=43
  echo "$func_result"
}

func_result="$(my_function)"
echo $func_result

if [[ $(( $func_result - 3 )) -eq 40 ]];
then
    echo "returned true"
else
    echo "returned false"
fi
```
Output:
```
43
returned true
```
- ```func_result``` is locally defined
- ```echo``` to return the value
- Capture the return value ```"$(my_function)"```
