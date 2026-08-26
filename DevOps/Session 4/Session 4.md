# Commands
#session4commands 

| **Command**                              | **Work**                                           |     |
| ---------------------------------------- | -------------------------------------------------- | --- |
| ***hostname***                           | *Hostname*                                         |     |
| ***bash -l***                            | *Reload bash*                                      |     |
| ***sudo -i<br>su - root***               | *User root*                                        |     |
| ***apt upgrade***                        | *All upgrade*                                      |     |
| ***apt update***                         | *Update list of apps*                              |     |
| ***apt -cache<br>policy app***           | *Getting versionof the app*                        |     |
| ***timedatectl list <br>-timezones***    | *get the time zoneof the city*                     |     |
| ***timedatectl set <br>-timezone city*** | *set the time of your city*                        |     |
| ***man -S 5 passwd***                    | *Choose the name in <br>what section*              |     |
| ***man -a name***                        | *Shows all the name <br>in every section*          |     |
| ***nl***                                 | *Number the lines without empty*                   |     |
| ***cat -n***                             | *Number the lines*                                 |     |
| ***wc***                                 | *Word count*                                       |     |
| ***watch "command"***                    | *Watch the command*                                |     |
| ***mkdir***                              | *Create a directory*                               |     |
| ***mkdir -p***                           | *Create a parental directory*                      |     |
| ***-v***                                 | *Verbose*                                          |     |
| ***cp Location***                        | *Copy*                                             |     |
| ***-f***                                 | *Force*                                            |     |
| ***-i***                                 | *ask question*                                     |     |
| ***-r***                                 | *for directory*                                    |     |
| ***crtl + r***                           | *Search in history*                                |     |
| ***mv***                                 | *Move a file*                                      |     |
| ***rm***                                 | *Remove a file*                                    |     |
| ***date > output***                      | *Redirect*                                         |     |
| ***ping -c -s -i***                      | *Count, Size, Every\Second*                        |     |
| ***echo $?***                            | *Exit Status Code For Last* <br>*Recently Command* |     |
| ***cut -d "\|" -f 1,3 file***            | *Cut the delimiter by index*                       |     |
| ***less***                               | *To page a file*                                   |     |
| ***head -num***                          | *First num lines*                                  |     |
| ***tail  -num***                         | *Last num lines*                                   |     |
| ***-f***                                 | *Follow realtime reading*                          |     |
| ***find***                               | *To find something in a directory*                 |     |
| ***stat***                               | *Details of the file*                              |     |

#### Find

| command         | Work                         |
| --------------- | ---------------------------- |
| ***-name " "*** | *Something you want to find* |
| ***-type d,f*** | *Type of the name*           |
| ***-size***     | *The size of the file*       |
| ***-mtime***    | *Day*                        |
| ***-mmin***     | *Minute*                     |
| ***-ls***       | *Shows like ls command*      |
| ***-user***     | *What user made it*          |
| ***!***         | *Not*                        |
| ***-o***        | *Or*                         |
| ***-a***        | *And*                        |



```
*.txt
*.????
[a,b,m]*.????
{Pattern, Pattern}
```

[[Commands]]

# Input Output Streams

- Redirect means transferring the output of commands to files devices and inputs of other commands.

- Redirect the output of commands to a file with >.

- Redirect the output of one command to the input of another command with the | sign (pipeline).


| ***#*** | **Name** | **Type**        | **Device** | **File**      |
| ------- | -------- | --------------- | ---------- | ------------- |
| **1**   | *stdin*  | *Input Stream*  | *Keyboard* | */dev/stdin*  |
| **2**   | *stdout* | *Output Stream* | *Terminal* | */dev/stdout* |
| **3**   | *stderr* | *Output Stream* | *Terminal* | */dev/stderr* |


Standard Input
......↓.......
|Program| ➜ Standard Error
......↓.......
Standard Output

>[!tip] If you redirect another command to a file that has data in it, the data will disappeared.So you can use >> to keep your previous data.


[[Session 3|Previous Session]]
[[Session 5|Next Session]]



