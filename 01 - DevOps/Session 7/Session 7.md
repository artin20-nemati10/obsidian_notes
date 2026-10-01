
# Hard Links
- Each hard linked file has the same physical file location.
- hard links remain linked even if original files are moved.
- links have actual file contents.
- Removing any link doesn't affect other links.
- We cannot create a hard link for a directory to avoid recursive loops.
- The size of any of the hard link files same as original file.
- The disadvantage of the hard link is that it cannot be crated for files on different file systems and it cannot be created for special files or directories.
``` 
ln file_1 Hard_Link_1
ln file_2 hard_link_2
```
---
# What is Inod
 - An inod is a file data structure that stores information about files except name and data.
 - Data is sorted on disk in the form of fixed-size blocks If file exceeds a standard block, Linux will find next available segment to store the rest of your file from nodes.
 - Inods don't contain actual data it stores the files metadata including all storage blocks on which the files data cam be found
#### Data in Inodes:
1. File Size
2. Device on which the file sorted.
3. User and groups IDs associated with the file.
4. Permission needed to access the file 
5. Creation, read and write timestamps
6. Location of the data(though not the file path)
```
$ find / -inum [Inode]
$ find / -samefile [File]
$ find -h   --Human_Readable
$ find -i   --Inode
```
---
#### Inode Structure
![[Screenshot from 2026-09-16 10-32-28.png]]

---

# Symbolic Links 
 - A soft link is similar to shortcut feature in Windows.
 - Soft linked file has separate inode that points to original.
 - It can be linked across different file systems.
 - If original file deleted or moved, soft linked file will not work.
 - Soft Link contains the path for original file and not the contents.
 - A soft link can link to a directory.
 - The size of the soft link is equal to the length of the path of the original file we gave.
```
$ ln -s [Absolute_pass] [Soft-_link]
```

# Manage Processes of system
###### View the list of running processes with the ps command:
```
$ ps -f 
$ ps -ef or ps -aux
$ top
```
###### Output fields of the ps -f command:

| Word  |                    Meaning                     |
|:-----:|:----------------------------------------------:|
|  UID  |                  Owning user                   |
|  PID  |               Unique Process ID                |
| PPID  |               Parent Process Id                |
| STIME |             When the task started              |
| TIME  |       How ling the task has been active        |
|  CMD  | The actual command line used to start the task |

---
# Linux Boot Process
1. BIOS(firmware) : Boot order, HW clock, cpu unit,...
2. MBR(Master Boot Record) : Boot Loader, Partition table.
3. GRUB(Boot loader) : Load Kernel into RAm
4. Kernel: Executes /sbin/init
5. Init Process : Executes runlevel programs 
6. Runlevel:

|  0  |                 Shutdown                  |
|:---:|:-----------------------------------------:|
|  1  | Single user without network , Single user |
|  2  |  Multi user without network, Multi user   |
|  3  |       Multi user target, Multi user       |
|  4  |                  Reserve                  |
|  5  |       Graphical target, Multi user        |
|  6  |                  Reboot                   |
# Linux kill signals
- Signals are used to manage processes in Linux.
- Software must also have a number of signal handlers designed to communicate with Linux signals.
- Signals are sent to processes using the kill command.
###### See the full list of signals for kill command
```
$ kill -l
```

###### Ways to stop a process or task in linux:
- Use Ctrl+C to Cancel it.
- Use the kill command and its Process ID
---
# Job control in Linux
- Every command that runs on linux is called a job.
- Jobs can be executed in both foreground and background.
- Only one job can be executed in foreground at any one time.
- By running jobs in background, you can run multiple jobs at the same time in one terminal.
```
$ bzip2 bigfile &
   [1] 1493
$ jobs
[1]+ running        bzip2 bigfile &
```

>[!tip] You can Control the Jobs :
> for Foreground:
> ```
> fg %[ID]
>```
>for Background:
>```
>bg %[ID]
>```
>kill it:
>```
>kill %[ID]
>```

## Job control in Linux
- If you return a job t foreground, it can be stopped with the following actions:
1. Ctrl + C : Kills the process
2. Ctrl + Z : Suspend job and place it to background as a stopped job.
- Suspend job is a job that has gone to background and temporarily stopped.
- On a suspended job, following 3 actions can be applied:
1. Terminate it with kill %\[ID]
2. Send it to Foreground with fg %\[ID] and enable it.
3. Reactivate it with bg %\[ID] in the same background.

## Nohup (No Hang-Up) Signal
- By closing a session, SIGHUP is sent and all its jobs will be closed!
- Background jobs are protected against SIGHUP with the nohup tool.
- The output of executed command by nohup store in nohup.out file in the current path.
```
$ nohup ping 8.8.8.8 &
```
