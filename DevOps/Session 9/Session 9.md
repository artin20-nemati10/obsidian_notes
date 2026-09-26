
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
## COnditioning (if)

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

