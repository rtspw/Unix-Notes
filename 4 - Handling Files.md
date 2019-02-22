# 4 - Handling Files

<br>

### $ ls Patterns

When searching with ls, you can use advanced patterns to search:

- **?** for one character
- **\*** for many characters
- **[]** for sets
  For example: [a-z] or [1-4] or [!a] (! means not)
  
```bash
ls test[1-7]
```
will match test4, test5, etc.
  
<br>

## Creating and Manipulating Files:

|  Command | Useful Flags | Action |
|---|---|---|
| `touch [filename]` | |Create file |
| `cp [source] [dest]`| -i (Ask to overwrite) | Copy source to new destination file |
| `mv [old name] [new name]`| | Renames a file |
| `rm [filename]`| -i (Asks to delete)  <br> -r (delete files inside dir) <br> -rf (delete dir and files)| Permanently delete file |
| `mkdir [dir name]` | | Create new directory |
| `rmdir` | | Removes an **empty** directory |
| `tree [dir]`| | Displays directory tree visual |

<br>

#### Symbolic Links

A **symbolic link** is a file which *points* to somewhere else in the virtual directory. In a way, the link will then represent the other file in memory.

To create a link, we use:
```bash
ln -s [existing file] [link name]
```

<br>

## Viewing File Contents

|  Command | Useful Flags | Action |
|---|---|---|
| `file [filename]` | | See what kind of file it is (ASCII text, bin, etc) |
| `cat [filename]` | -n (Line numbers) <br> -b (ignore empty lines) <br> -T (ignore tabs) | Displays entire file contents |
| `more [filename]` | | Opens pager utility (same as MAN page) to display file |
| `less [filename]` | | More advanced version of `more` with a larger command set | 
| `tail [filename]` | -n [number] (number of lines) | Views last n (default 10) number of lines) |
| `head [filename]` | -n [number] (number of lines) | Views first n (default 10) number of lines) |