#session5commands 

|               Command               |                        Work                         |
| :---------------------------------: | :-------------------------------------------------: |
|      ***command && command***       |          *Start the commands step by step*          |
| ***find ... -exec cp {} loc \\;***  |                       *- - -*                       |
|        ***find -mindepth***         |              *Depth of the directory*               |
|        ***find -maxdepth***         |              *Depth of the directory*               |
|  ***tr "character" "character"***   |      *Translate or replace the chars together*      |
|  ***tr \[:upper:\] \[:lower:\]***   |     *Make the upper cases char to lower cases*      |
|      ***tr -d \[:isdigit:\]***      |              *Delete the taken value*               |
|        ***Today=\`date\`***         |    *Push the stdout of the command in variable*     |
|         ***Today=$(date)***         |    *Push the stdout of the command in variable*     |
|           ***tac file***            |            *Reverse of the cat command*             |
|  ***sed "s/Artin/Arash/g" file***   |     *Replace the first word to the second word*     |
| ***sed -i "s/Artin/Arash/g" file*** |     *After the replacement the file will Edit*      |
| ***sed "3,7s/Artin/Arash/g" file*** | *In the lines have gotten it will replace the word* |
|         ***sed -n "34p"***          |              *To see the wanted lines*              |
|     ***grep artin Names.txt***      |        *To fine the selected word in a file*        |
|       ***grep -i file name***       |            *Ignore the key sensitivity*             |
|       ***grep -n file name***       |                    *Line number*                    |
|            ***grep -H***            |        *Show the result with the file name*         |
|    ***grep "^root" file name***     |   *search the word of the beginning of the line*    |
|         ***grep "root$"***          |              *At the end of the line*               |
|        ***egrep "CBd#@&$"***        |      *Make the special characters to regular*       |
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
 The most popular tools for compression available in Linux:
 - Gzip
 - Bzip2
- zip
- 7zip

## Gzip
- Most popular compression algorithm in Linux.
- Keep all file parameters, such as : Ownership,  Timestamp, etc.
- Its file extension is : \[File Name].gz
- Gzip compresses the original file.
- The gzip compression rate is denoted by -n from 1 to 9.
### Commands

| Command gzip ... file |           Work            |
| :-------------------: | :-----------------------: |
|         ***-2***          |    *Compression rate*     |
|         ***-l***          | *List of the compression* |
|         ***-k***          | *Keep the original file*  |
|         ***-r***          |        *Directory*        |
|         ***-v***          |         *Verbose*         |

---
## XZ
- It has the same options as gzip and bzip2.
- Keep all file parameters, such as : Ownership, Timestamp, etc.
- Its file extension is : \[File Name].xz
- Xz compress the original file.
- The xz compression rate is denoted by -n from 1 to 9.

| Command xz ... file |           Work            |
| :-----------------: | :-----------------------: |
|      ***-9***       |    *Compression rate*     |
|      ***-l***       | *List of the compression* |
|      ***-k***       | *Keep the original file*  |
|      ***-r***       |        *Directory*        |
|      ***-v***       |         *Verbose*         |

----
```
zip archive_name File_1 File_2 ...
```
---
# Tar Archiving Tools
- Tar is the most widely used archiving tool in Linux.
- This tool is for backing up or archiving multiple file.


| Command |                 work                  |
| :-----: | :-----------------------------------: |
|   ***-c***    |          *Create a new file*          |
|   ***-x***    |  *Extracting contents of a tar file*  |
|   ***-t***    | *Listing contents without extracting* |
|   ***-f***    |   *Specifying name of the tar file*   |
|   ***-v***    |  *Print a nicely report about file*   |
|   ***-z***    |    *Using Gzip in archiving files*    |
|   ***-j***    |   *Using Bzip2 in archiving files*    |
|   ***-J***    |     *Using XZ in archiving files*     |
|   ***-r***    |      *Append a file to archive*       |

### Tar Structure
##### To Create An Archive File:
- $ tar -cfv archive_name File_1 File_2 File_3  
##### To Extract An Archive File:
- $ tar -xvf archive_1 

##### To Create A  Gzip Archive File:
- $ tar -zcfv archive_name.gz File_1 File_2 File_3  
##### To Extract A Gzip Archive File:
- $ tar -zxvf archive_1.gz

##### To Create A Bzip2 Archive File:
- $ tar -jcfv archive_name.bz File_1 File_2 File_3  
##### To Extract A Bzip2 Archive File:
- $ tar -jxvf archive_1.bz

##### To Create A XZ Archive File:
- $ tar -Jcfv archive_name.xz File_1 File_2 File_3  
##### To Extract A XZ Archive File:
- $ tar -Jxvf archive_1.xz 

[[Session 4|Previous Session]]
[[Session 6|Next Session]]