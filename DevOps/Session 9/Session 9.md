
# Basics of Shell Scripting

## Defining a Function in Linux
###### Defin e functions in Linux for analysing and processing variables:
---
```
$ FUNCTION_NAME()
{
[ACTION1]
[ACTION2]
}
```
---
## Shebang ( #! )
- Shebang should always be the first line of a script.
- Shebang basically represents the programming languagein which the script is written.
- File extentions are just a label and type of language specified by shebang.
---
```
$ vim script1/sh

#!/bin/bash

. . .
```
---
## Variables
###### In the Shell environmet, a variable can be find as VARIABLE="value".
###### In a script, you can define and use a variable in the same way.
---
```
$ vim script2.sh

#!/bin/bash
MYNAME="Artin"
```
---
## Command Substitution
- To use the result of one statement in another statement or as a variable, the command must be used inside  a $(COMMAND) or \`COMMAND\` (Backtick).
- Using the Tee command, a stdout can be displayed bot in screen and redirect in a file.
---
```
$ date | tee output.txt
- - - - - - -
```
## Performing Math
###### Using expr or $\[], math operatoins can be performed in Bash environment.
---
```
$ expr 3 \* 7
```
---
## Bash Calculator
###### Float calculations are performed using the bc command: 
---
```
$ bc
>12.35644 * 64.7814
...
```
---

## Redirecting Input & Output using EOF
###### The EOF tool is used to redirect multiple lines of text or commands into another command.
---
```
$ wc << EOF
>
>
>
>EOF

$ cat >> names.txt << EOF
```
---
## Conditioning (if)
- In bash, like other languages, needs to use condition.
- The easiest way to use the condition is if.
- Using else in thes type of condition is optional.
---
```
if [ EXPRESSION1 ]
then
	COMMAND1
	COMMAND2
elif [ EXPRESSION2 ]
then
	COMMAND3
	COMMAND4
else
	COMMAND5
	COMMAND6
fi
```
---
## Conditioning (if)

|     Expression     |                 Meaning                 | Operator |
|:------------------:|:---------------------------------------:|:--------:|
| STRING1 = STRING2  |           Strings are equal.            |    =     |
| STRING1 != STRING2 |         Strings are not equal.          |    ≠     |
|     -n STRING1     | String1 has a length greater than zero. |          |
|     -z STRING1     |      String1 has a length of zero.      |          |
|   INT1 -eq INT2    |         INT1 is equal to INT2.          |    =     |
|   INT1 -ne INT2    |         INT1 is equal to INT2.          |    ≠     |
|   INT1 -ge INT2    | INT1 is greater than or equal to INT2.  |    ≥     |
|   INT1 -gt INT2    |       INT1 is greater than INT2.        |    >     |
|   INT1 -le INT2    |   INT1 is less than or equal to INT2.   |    ≤     |
|   INT1 -lt INT2    |         INT1 is less than INT2.         |    <     |
|  File1 -nt File2   |        File1 is newer than File2        |          |
|  File1 -ot File2   |        File1 is older than File2        |          |

---
## Bash Built-in Variables

| variables |                              Description                              |
|:---------:|:---------------------------------------------------------------------:|
|    $?     |        Exit status of last recently executed command (0 or 1).        |
|    $0     |                             Script name.                              |
|  $1 - 9   |            nth argument passed to the script or function.             |
|    $@     | All arguments passed to the script; each argument is a separate word. |
|    $#     |         Number of arguments passed to the script or function.         |
|    $$     |          PID of the script in which this variable is called.          |
|    $!     |         PID of the last recently executed background command.         |
|  $RANDOM  |            Pseudorandom integer value between 0 to 32767.             |

---
## $? Exit Status Codes

| Code  | Description                           |
| ----- | ------------------------------------- |
| 0     | Successful completion of the command. |
| 1     | General unknown error.                |
| 2     | Misuse of shell command.              |
| 126   | The command can’t execute.            |
| 127   | Command not found.                    |
| 128   | Invalid exit argument.                |
| 128+x | Fatal error with Linux signal x.      |
| 130   | Command terminated with Ctrl+C.       |
| 255   | Exit status out of range.             |

---
## Conditioning (if)
###### Write programthat takes two numbers from the input and compares them in size.
```
artin@host:~$ vi script6.sh
	#!/bin/bash
	read -p "Please enter first number: " var1
	read -p "Please enter second number: " var2
	if [ $var1 -eq $var2 ]
	then
	echo "The values are equal!"
	fi
	if [ $var1 -gt $var2 ]; then
	echo "1st number ($var1) is greater than 2nd number ($var2)"
	elif [ $var1 -lt $var2 ]; then
	echo "2nd number ($var2) is greater than 1st number ($var1)"
	fi
```
---
## Conditioning (if)
- Write a program that takes an IP from the input and checks whether the server in Pingable or sends an Email to the root user if the server is down.
```
artin@host:~$ vi script7.sh
	#!/bin/bash
	read -p "Please Enter Your IP: " IP
	ping -c 1 $IP >> /dev/null
	if [ $? -eq 0 ]
	then
	echo "Server $IP is pingable!"
	else
	echo "Server $IP is down..."
	mail -s "$IP is Down" root@host < /dev/null
	fi
```
---
## Loops (for)
- The purpose of using a loop is to repeat one or more command lines several times.
#### Instead of LIST, the number range can be specified as fallows: 
- 1 2 3 4 5(Specify number of loop numbers one by one)
-  {1..5}(specify a range of numbers)
-  {0..10..2}(Range of numbers from 0 to 10 with space of 2)
- $(seq 0 2 10) (Range of numbers from 0 to 10 with space of 2)

```
for VAR in LIST;
do
	COMMAND1
	COMMAND2
done
```
---
## Loops (for)
```
artin@host:~$ vi script8.sh
	#!/bin/bash
	for i in {1..5}
	do
		echo "welcome $i times!"
	done
arash@host:~$ ./script8.sh
	Welcome 1 times!
	Welcome 2 times!
	Welcome 3 times!
	Welcome 4 times!
	Welcome 5 times!
```
---
## Loops (while)
---
```
while [ CONDITION ]
do
	COMMAND1
done
```
---
- While is used to execute a set of commands as long as the condition is met.
---
```
artin@host:~$ vi script7.sh
	#!/bin/bash
	MYVAR=3
	while [ $MYVAR -gt 0 ]
	do
		echo $MYVAR
		let MYVAR=MYVAR-1
	done
```
---
## Loops (while)
- Write a script that takes two numbers from the input and compares them, and this program is such that if the values of the two numbers were empty, it still wants the value and does not exit the program until it enters the value.
```
artin@host:~$ vi script7.sh
???
???
???
if [ $var1 -eq $var2 ]
then
	echo "The values are equal!"
elif [ $var1 -gt $var2 ]
then
	echo "$var1 is greater than $var2"
else
	echo "$var2 is greater than $var1"
fi
```
---
