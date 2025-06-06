---
title: Command Line Basics
parent: Computational resources
---

# Command Line Basics

The command line interface (also known as terminal, shell, or CLI) is a text-based interface for interacting with your computer. This guide provides basic instructions for using the CLI, intended for users who occasionally need to execute programs or interact with files through the terminal.

## Basic Commands

### Navigation
- `pwd` - Shows your current directory (Print Working Directory)
- `ls` - Lists files and folders in the current directory
- `cd [directory]` - Changes to the specified directory
  - `cd ..` - Moves up one directory level
  - `cd ~` - Returns to your home directory

### File Operations
- `cp [source] [destination]` - Copies a file
- `mv [source] [destination]` - Moves or renames a file
- `rm [file]` - Removes a file (use with caution!)
- `mkdir [name]` - Creates a new directory

### Running Programs
- `./program_name` - Runs an executable in the current directory
- `python script.py` - Runs a Python script (this assumes you have python installed on the machine)

## Tips for Beginners

1. **Use Tab Completion**: Press the Tab key to auto-complete file and directory names
2. **Check Your Current Directory**: Always know where you are using `pwd` before running commands
3. **Be Careful with `rm`**: The shell will not ask twice. Deleted files cannot be recovered from the trash
4. **Use `ls` Often**: Check what files are in your directory before making changes

## Common Issues and Solutions

- **"Command not found"**: The program you're trying to run isn't in your PATH or isn't installed
- **"Permission denied"**: You don't have the right permissions to execute the file. You may need to ask the program creator to run `chmod`, or contact the system adminstrators for access to certain files.
- **"No such file or directory"**: Check your spelling and current directory

## Further Reading

- [Command Line Crash Course](https://learnpythonthehardway.org/book/appendixa.html)
- [Linux Command Line Basics](https://ubuntu.com/tutorials/command-line-for-beginners)
- [Mac Terminal Guide](https://macpaw.com/how-to/use-terminal-on-mac) 