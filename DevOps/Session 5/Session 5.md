
| Command                             | Work                                                |
| ----------------------------------- | --------------------------------------------------- |
| ***command && command***            | *Start the commands step by step*                   |
| ***find ... -exec cp {} loc \\;***  | *- - -*                                             |
| ***find -mindepth***                | *Depth of the directory*                            |
| ***find -maxdepth***                | *Depth of the directory*                            |
| ***tr "character" "character"***    | *Translate or replace the chars together*           |
| ***tr \[:upper:\] \[:lower:\]***    | *Make the upper cases char to lower cases*          |
| ***tr -d \[:isdigit:\]***           | *Delete the taken value*                            |
| ***Today=\`date\`***                | *Push the stdout of the command in variable*        |
| ***Today=$(date)***                 | *Push the stdout of the command in variable*        |
| ***tac file***                      | *Reverse of the cat command*                        |
| ***sed "s/Artin/Arash/g" file***    | *Replace the first word to the second word*         |
| ***sed -i "s/Artin/Arash/g" file*** | *After the replacement the file will Edit*          |
| ***sed "3,7s/Artin/Arash/g" file*** | *In the lines have gotten it will replace the word* |
| ***sed -n "34p"***                  | *To see the wanted lines*                           |
| ***grep artin Names.txt***          | *To fine the selected word in a file*               |
| ***grep -i file name***             | *Ignore the key sensitivity*                        |
| ***grep -n file name***             | *Line number*                                       |
| ***grep -H***                       | *Show the result with the file name*                |
| ***grep "^root" file name***        | *search the word of the beginning of the line*      |
| ***grep "root$"***                  | *At the end of the line*                            |
| ***egrep "CBd#@&$"***               | *Make the special characters to regular*            |
|                                     |                                                     |
>[!tip] you can use some unique characters that is not in your text as a delimiter of sed

# Introduction to VI/VIM Text Editor
- VI editor was created in 1976 on Unix systems.
- An improved version of it called CIM was realized in 1991.
- It can be installed and used on all versions of Unix and Linux.
- It can also be installed and used on Windows, Dos and Mac.

To Use VIM Text Editor type ```vim file```

---
: = Command

---
i - a - o = Insert

---
v = Visual
Shift + v = Visual Line Mode
Crtl + v = Visual Block Mode
Shift + i = Switch to Insert with the selection

## Vim Commands

| Space   | Command            | Work                                                |
| ------- | ------------------ | --------------------------------------------------- |
| Insert  | Text               | ---                                                 |
| Command | :w                 | Save                                                |
| Command | :q!                | Quit <br>without saving                             |
| Command | :wq!               | Quit And Save                                       |
| Normal  | u                  | Undo                                                |
| Normal  | R                  | Redo                                                |
| Normal  | dd                 | Cut                                                 |
| Normal  | p                  | Paste                                               |
| Normal  | y                  | Copy                                                |
| Command | :s/first/second/g  | To replace the words in line<br>same as sed command |
| Command | :%s/first/second/g | To replace the word<br>in whole file                |
| Normal  | x                  | Delete                                              |
| Visual  | d                  | Cut                                                 |
| Visual  | y                  | Copy                                                |
| Visual  | p                  | Paste                                               |
| Normal  | /                  | Search                                              |
| Command | :w Name            | Save as                                             |
| Command | :new File_Name     | New window                                          |
| Normal  | Crtl + ww          | Next Window                                         |
| Command | :vsplit File_Name  | Vertical Window                                     |
| Command | :tabnew File_Name  | New Tab                                             |
| Command | :set nu            | Number                                              |
| Command | :tabnext           | Next tab                                            |
| Normal  | Shift + g          | Last Line                                           |
| Normal  | gg                 | First Line                                          |
``` 
vimdiff file1 file2
```

| Command  |
| -------- |
| :diffput |
| :diffget |
# Compression Tools
- Compressing file is a solution to reduce space occupied by a file on disk.
- Also it is a solution to reduce amount of data shared network.
 The most popular tools foe compression available in Linux:
 - Gzip
 - Bzip2
- zipx
- 7zip

	