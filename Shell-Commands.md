# Hot
> [Shell Commands](#shell-commands) \
> [ls](#ls-option-file) \
> [pushd/popd](#pushd) \
> [View File](#view-file) \
> [File Permissions](#file-permissions) 


# Shell Commands
- Clear Screen with ```ctrl+L```
- Check file type ```file```
- ```!x``` to run command that has number x in ```history```
- Brace Expansion, **no whitespaces inside braces**
    ```bash
    $ echo hello {world,dunia} end
    hello world dunia end
    
    $ echo hello {2..10} end
    hello 2 3 4 5 6 7 8 9 10 end
    
    $ echo hello {2..10..3} end
    hello 2 5 8 end

    $ echo hello {10..2..3} end
    hello 10 7 4 end
    ```

## ls [OPTION] [FILE]
```
-a include hidden files 
-l include details
-R recursive
-S sort by size
-t time, latest first
-r reverse order
```
**Example**: Show files with details including hidden files in reverse order
```bash
$ ls -lar
```

## mkdir [OPTION] \<dir_1> ... \<dir_n>
```
-p Overwrite directory if exist
-v Show verbose description  
```

## cp SOURCE_1 SOURCE_2.. DEST
```
-r recursive
-i interactive
```

## rm [OPTION] FILE..
```
-f ignore non-existent file (don't prompt)
-i interactive, prompt before deleting
-r recursive
-v verbose
```

## mv SOURCE.. DIRECTORY

## pushd
- Changes directory just like ```cd```
- Also adds directory to stack
- View stack with ```pushd +0``` or ```dirs```
- ```dirs -v``` for verbose
- Current directory is entry 0 i.e. topmost element 
    ```bash
    $ pushd dir

    ~dir$ dirs -v
    0 ~dir

    ~dir$ pushd subdir

    ~dir/subdir$ dirs -v
    0 ~dir/subdir
    1 ~dir

    ~dir/subdir$ pushd subsubdir

    ~dir/subdir/subsubdir$ dirs -v
    0 ~dir/subdir/subsubdir
    1 ~dir/subdir
    2 ~dir
    ```

- ```pushd +x``` changes directory to x-th element in stack and prints the updated stack
    ```bash
    ~dir/subdir/subsubdir$ pushd +2
    0 ~dir
    1 ~dir/subdir/subsubdir
    2 ~dir/subdir

    ~dir$ pwd
    dir
    ```

- ```popd``` works similarly

# View File
### more less
- Views content of a file one pageful at a time
- ```less``` comes with more features than ```more```
### wc
- prints line, word, byte count of file
### head [OPTION] [FILENAME]
- Reads file from the beginning
- By default reads first 10 lines
    ```bash
    $ head -n x file  # read x lines of file
    $ head -c x file  # read x bytes/characters of file
    ```
- ```tail``` works similarly, reading from the end of file

# File Permissions
- 10 character long
- First character implies directory or file
- 9 characters, grouped by 3, represents permissions for user, group and other
>                -rwxrw-r-- 
> Is a file which has
> - read, write, execute permissions for user 
> - read, write permissions for groups
> - read permissions for others 

![](https://cdn.discordapp.com/attachments/932687336523833347/944227570021433374/linux-permissions-chart.png "Linux Permissions")


## chmod
- adds read and write permission to groups and others 
    ```bash
    chmod go+rw filename
    ```
- removes read and write permission from groups and others 
    ```bash
    chmod go-rw filename
    ```
- Can use octal notation
    ```bash
    $ chmod 755 filename

    > 7 => 111 
    > 5 => 101 
    > 755 => rwxr-xr-x 
    ```
- Can also use
    ```bash
    chmod u=rwx,g=rx,o=r filename
    ```
