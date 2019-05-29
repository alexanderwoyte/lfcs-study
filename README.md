# lfcs-study

## Basic Commands

### Files and Directories
#### du
    du file && du folder && du *
The 'du' command outputs the disk space occupied by files and folders.
    du -h file
The '-h' option makes the output human readable.
#### ls
    ls && ls directory
The 'ls' command outputs the content of a folder.

    $ ls -l
    total 2097256
    drwxr-xr-x   2 root root       4096 May 11 08:39 bin
    drwxr-xr-x   4 root root       4096 May 11 08:41 boot
    drwxr-xr-x   2 root root       4096 Jan 20 21:07 cdrom
    drwxr-xr-x  21 root root       4780 May 14 14:27 dev
    drwxr-xr-x 150 root root      12288 May 11 08:43 etc
    drwxr-xr-x   3 root root       4096 Jan 20 21:11 home
    . . .
The '-l' option requests output in long form.
#### tree
    tree
From the man page:
> "Tree is a recursive directory listing program that produces a depth indented listing of files..."
#### pwd
    pwd
From the man page:
> "Print the full filename of the current working directory."
#### touch
    touch -a foo
Updates the modification time of a file, creating it if it doesn't already exist.
#### mkdir
    mkdir foo
Creates the new directory 'foo'.
#### rmdir
    rmdir foo
Removes the empty directory, 'foo'. For a directory that isn't empty, use 'rm -r foo'.
#### mv
    mv foo ../bar/foo
Moves the file or folder, 'foo', a directory back and into the folder 'bar'.

    mv foo bar
Renames the file or folder, 'foo', to 'bar'.
#### cp
    cp foo bar
Creates a copy of the file or folder, 'foo', naming it 'bar'.
#### rm
    rm foo
Removes the file 'foo'.

    rm -r foo
Recursively removes the folder 'foo'. Used primarily for non-empty directories. For empty directories, use 'rmdir foo'.
 
### Standard File Permissions
#### Octal
Consists of a three digit number sequence describing the read, write and execute permissions that a group has on a file/folder.
Each digit is the sum of the following:
 - 1: Exec
 - 2: Write
 - 4: Read

The first digit notes the privileges for the owner, the second for the group and the third is for everyone else. Therefore, `chmod 764 foo` would alter permissions of foo so that the owner has all privileges, group has read and write, and everyone else can just read.

#### Absolute


#### Relative
#### Advanced Permissions

### Locate Files & Patterns
#### find
Recursive by default.
Examples:
 - `find /var/log -name '*.log'` searches for files with the '.log' suffix in /var/log.
 - `find /var/log -iname '*.log'` is the same but ignores case.
 - `find ~ -perm 777 -exec rm {} \;` searches files with 777 permissions and executes `rm {file}`. The 'exec' command must lie between '-exec' and the terminating '\\;'.
 - `find /etc -size -100k` searches for files in /etc that are smaller than 100 kilobytes. Likewise, `+100k` could be substituted to look for files greater than 100 kilobytes or `100k` for files exactly that size.
 - `find . -type f -size +2M -maxdepth 2` searches for only files greater than 2 megabytes at a maximum depth of 2 directory levels.
 - `find . \! -user owner` looks for files that are not owned by `'owner'`. The `'!'` operator negates and `'\'` escapes so that it can be interpreted by  the shell.
 - `find . -perm -222` finds files with at least write permissions for all. For example, this will return files with `222` and `777` but not `644` or `700`.
#### grep
Search for the pattern in a file or all files in a directory. Examples:
 - `grep -Rl` : Recursively (include symbolic links) list all files.
 - `grep -rl` : Recursively (do not include symbolic links) list all files.
 - `grep -RHn` : Search recursively (including symbolic links) for the word (output including path to file, line number and matching line)
 
### Compare & Manipulating Text
#### cmp
#### comm
#### diff
#### uniq
#### sort
#### sed
#### cut
#### tr
#### vi, vim

### Displaying Text
#### cat
#### less
#### more
#### head
#### tail
 
### Hard & Soft Links
#### ln, ln -s
 
### Regular Expressions
#### File Globbing
#### Regex
| Character |                Definition                |  Example   |        Result         |
| :-------: | :--------------------------------------: | :--------: | :-------------------: |
|     ^     |            Start of a string             |    ^abc    |    abc, abcd, abc1    |
|     $     |             End of a string              |    abc$    |  abc, rasabc, 2aabc   |
|     .     |       Any character except newline       |    a.c     |     abc, acc, a1c     |
|           |                                          | Alteration |           a           |
|   {...}   | Explicit quantity of preceding character |   ab{2}c   |         abbc          |
|   [...]   |   Explicit set of characters to match    |   a[bB]c   |        abc,aBc        |
| [a-z0-9]  |   One lower case characters or number    | a[a-z0-9]c |        aac,a1c        |
|   (...)   |           Group of characters            |  (abc){2}  |        abcabc         |
|     *     | Null or more of the preceding characters |    a*bc    | bc, abc, aabc, aaaabc |
|     +     |  One or more of the preceding character  |    a+bc    |       abc, aabc       |
|     ?     |  Null or one of the preceding character  |    a?bc    |        bc, abc        |
|    ^$     |               Empty string               |            |                       |

* Not all regular expressions are supported by `grep`. As alternative can be used `egrep`
#### Sed
 
### Redirection
#### < : redirect stdin
#### \> and >> : redirect stdout
#### 2> : redirect stderr
#### | : the stdout is transformed in stdin
#### |& : stderr to stdin
#### 2>&1 : redirect stderr to same place of stdout
 
### Users, Groups and Their Privileges
For privileges relating specifically to files, see
#### adduser
`adduser alex`
#### deluser
`deluser alex`
#### passwd
`passwd alex`
#### groups
`groups alex`
#### groupadd
`groupadd sudoadmins`
#### usermod
`usermod -aG sudoadmins alex`
#### groupdel
`groupdel sudoadmins`
#### visudo

## Service Configuration
