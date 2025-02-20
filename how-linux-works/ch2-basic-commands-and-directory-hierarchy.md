# 2 - Basic Commands and Directory Hierarchy

## 2.1 - The Bourne Shell: /bin/sh
* Shell - program that runs commands
* bash - Bourne again shell

## 2.2.1 - Shell Window
* Terminal - shell window
* Prompt - `<name>@<host>:<path>$`

## 2.2.2 - `cat`
* `cat <file1> <file2> ...` - print the contents of files
    * called `cat` because it performs concatenation when it prints more than 1 file
    * no arguments - `cat` defaults to standard input stream

## 2.2.3 - Standard Input and Standard Output
* Input stream - file, device, terminal window, or an output stream of another process
* `CTRL-D` - stops current standard input entry from terminal with an `EOF` message

## 2.3.1 - Basic Commands `ls`
* `ls` - lists contents of a directory
    * default - current directory
* Arguments - 
    * `-l` - long listing
    * `-F` - file type information

## 2.3.2 `cp`
* `cp file1 file2` - copy `file1` to `file2`
* `cp file dir` - copy `file` into `dir`
* `cp file1 file2 file3 dir` - copy files into `dir`

## 2.3.3 `mv`
* `mv file1 file2` - rename `file1` to `file2`

## 2.3.4 `touch`
* `touch file` - create empty file
    * modifies modification timestamp

## 2.3.5 `rm`
* `rm file` - deletes file

## 2.3.6 `echo`
* `echo <args>` - prints arguments to the standard output

## 2.4 Navigating Directories
* root directory - `/`
* absolute path - starts with `/`
* parent directory - `..`
* current directory - `.`
* relative path - does not start with `/`

## 2.4.1 - 2.4.3 Directory Commands
* `cd` - changes shell's working directory
    * ommitting a directory return shell to the home directory, abbreviated as ~
    * shell built in - child process is not normally allowed to change the working directory of a parent process
* `mkdir` - creates new directory
* `rmdir` - removes directory
    * `rm -r dir` - deletes directory and all its contents

## 2.4.4 - Shell Globbing
* Globbing - shell matching simple patterns to file and directory names
* Expansion - shell matches then substitues the filenames for those arguments and runs the revised commands
    * `at*` - expands to all filenames that start with at
    * `*at` - expands to all filenames tha end with at
    * `*at*` - expands to all filenames that contain at
* `?` - glob character that matches exactly one character
    * example, `b?at` matches to boat and brat

## 2.5.1 Intermediate Commands - `grep`
* `grep root /etc/passwd` - print the lines in the `/etc.passwd` file that contain `root`
    * prints filename in addition to the matching line
    * `-i` - case insensitive search
    * `-v` - print lines that do not match
* `egrep` or `grep -E` - regular expressions
    * `.*` matches any number of characters, including none
    * `.+` matches any one or more characters
    * `.` match exactly one arbitrary character

## 2.5.2 Intermediate Commands - `less`
* `less /usr/share/dict/words` - page through large file
    * `spacebar` - page forward
    * `b` - page backward
    * `q` - quit
    * example - `grep '*' ch2-basic-commands-and-directory-hierarchy.md | less`

## 2.5.3 Intermediate Commands - `pwd`
* print working directory

## 2.5.4 Intermediate Commands - `diff`
* see differences between two text files
    * example - `diff -u ch1-the-big-picture.md ch2-basic-commands-and-directory-hierarchy.md | less`

## 2.5.5 Intermediate Commands - `file`
* `file file` - get format of a file
    * example - ASCII text

## 2.5.6 Intermediate Commands - `find` and `locate`
* `find dir -name file -print` - find file in dir

## 2.5.7 Intermediate Commands - `head` and `tail`
* `head file` - show first 10 lines of file
* `tail file` - show last 10 lines of file
* `-n` - change number of lines
* `+n` - print lines starting at line n

## 2.5.8 Intermediate Commands - `sort`
* `sort file` - sorts lines of text file in alphanumeric order.
    * `-n` - sort in numeric order
    * `-r` - reverse order

## 2.6 - Changing Password and Shell

## 2.7 - Dot Files
* `.file` - hidden files not shown by `ls`, use `ls -a`
    * reduces clutter

## 2.8 - Evironment and Shell Variables
* Shell variables - temporary variables usable by the shell
    * Assignment - `STUFF=blah`
    * Access - `$STUFF`
* Environment variables - like shell variables but not specific to the shell
    * child processes inherit environment variables from their parent process
    * Assignment - `export STUFF`

## 2.9 - The Command Path
* `PATH` - special environment variable that contains the command path, list of system directories that the shell searches when trying to locate a command
    * if programs with the same name appear in several directories in the path, the shell runs the first matching program
    * path components separated by colons `:`
    * modify - `PATH=dir:$PATH` or `PATH=$PATH:dir`

## 2.10 - Special Characters
* `*` - RegEx, glob character
* `.` - current directory, file/hostname delimiter
* `!` - negation, command history
* `|` - pipe
* `/` - directory delimiter, search command
* `\` - literals, macros
* `$` - variables, end of line
* `'` - literal strings
* ``` ` ``` - command substitution
* `"` - semi literal strings
* `^` - negation, beginning of line
* `~` - negation, directory shortcut
* `#` - comments, preprocessor, substitutions
* `[ ]` - ranges
* `{ }` - statement blocks, ranges

## 2.11 - Command Line Editing
* `CTRL-B` - move cursor back
* `CTRL-F` - move cursor forward
* `CTRL-A` - move cursor to beginning of the line
* `CTRL-E` - move cursor to the end of the line
* `CTRL-W` - erase preceding word
* `CTRL-U` - erase from cursor to beginning of the line
* `CTRL-K` - erace from cursor to end of the line

## 2.12 - Text Editors

## 2.13 - Getting Online Help
* `man` - see manual page for a command
    * `-k` - search for a man page by keyword
    * Man page numbered sections:
        1. user commands
        2. kernel system calls
        3. high level Unix programming lib docs
        4. device interface and driver info
        5. file descriptions
        6. Games
        7. file formats, conventions, and encodings
        8. system commands and servers
* `--help` - look for option for a command
* `info <command>` - another avenue for documentation

## 2.14 - Shell Input and Output
* Redirection - 
    * `command > file` - shell overwrites file with output from command
    * `command >> file` - shell appends output of command to end fo file
    * pipe - `|` send command output to input of another command
    * `command < file` - channel file into program input
* Standard error - additional output stream for diagnostics and debugging
    * Redirect - `ls /fffffffff > f 2> e` sends stdin to file f and stderr to file e
* Stream ID -
    * stdout - 1
    * stderr - 2 `2>&1` redirects stderr to stdout

## 2.15 Understanding Error Messages
* Anatomy of a UNIX error message
    *  `ls: cannot access /blahblah: No such file or directory`
        * program_name: file: error
* Common errors:
    * `No such file or directory`
        * known as ENONET or "Error NO ENTity"
    * `File exists`
    * `Not a directory` - treating a file as a directory
    * `No space left on device` - out of disk space
    * `Permission denied`
    * `Operation not permitted` - usually happens when trying to kill a process that you do not own
    * `Segmentation fault, Bus error` - program tried to access a part of memory that it was not allowed to touch and the operating system killed it

## 2.16 - Listing and Manipulating Hardware
* PID - each process has a numeric process ID
* `ps` - quick listing of running processes
    * PID
    * TTY - terminal device where process is running
    * STAT - process status, what the process is doing and where the memory resides. S means sleeping, R means running
    * TIME - amount of CPU time in minutes and seconds that the process has used so far
    * COMMAND - command used to run the program
* `ps` options
    * `ps x` - show all your running processes
    * `ps ax` - show all processes on the system
    *  `ps u` - include more detailed information
    * `ps w` - show full command names
* Process Termination
    * signal - message to a process from kernel
    * `kill pid` - sends `TERM` (terminate) signal
    * `kill -STOP pid` - sends `STOP` signal
    * `kill -CONT pid` - sends `CONT` signal to continue process
    * `CTRL-C` - `INT` (interrupt) signal
    * `kill -KILL pid` - cannot be ignored
    * `kill -l` - map signal numbers to names
* Job control
    * allows you to suspend and switch between programs
    * send `TSTP` signal with `CTRL-Z` and resume with `fg` (bring to foreground) or `bg` (bring to background)
    * `jobs` - see if you have accidentally suspended a process
* Background Processes
    * `&` - detach process from shell and put it in the background
        * `gunzip file.gz &`
        * shell responds by printing the PID and returning the prompt

## 2.17 File Modes and Permissions
* `ls -l` - `drwxr-xr-x 4 ethan ethan 4096 Feb 13 23:02 projects`
    * Type - `d`, `d` means directory, `-` means regular text or binary file, `l` means symbolic link
    * User - `rwx`
    * Group - `r-x`
    * Other - `r-x`
* Permissions -
    * `r` means file is readable
    * `w` means file is writable
    * `x` means file is executable
    * `-` permission not granted
    * `s` - indicates the executable is setuid, meaning that when the program is executed it runs as though the file owner is the user instead of you
* Modifying Permissions
    * `chmod g+r file` - add read to group
    * `chmod go-rwx file` - remove all permissions from group and others
    * `chmod 644 file` - represents permission bits in octal form
* `umask 077` - set default permissions of files that you create, in this case hide everything from everybody but you
    * put in `.bashrc` file
* Symbolic Links - file that points to another file or directory, alias
    * `l` is the file type
    * create - `ln -s target linkname`

## 2.18 - Archiving and Compressing Files
