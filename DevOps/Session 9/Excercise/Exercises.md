# Exercise 1: 
#### Write a program that takes a number from the input, compares it to 10, and returns a message for each of the 3 modes (larger, equal, and smaller).
---
```
#!/bin/bash

####################-CONFIG-####################

while [ -z $NUM ]

do

		read -p "Enter Your Number: " NUM

done

NUM=`echo $NUM | tr -d [:alpha:] | tr -d [:blank:]`

if [ $NUM -eq 10 ]

then

		echo "$NUM is Equal to 10"

elif [ $NUM -gt 10 ]

then

		echo "$NUM is Larger than 10"

else

		echo "$NUM is smaller than 10"

fi

#DONE
```
---
# Exercise 2
###### Exercise 2: Write a program that takes 20 numbers from the input, compares them, and states which number is the largest and smallest.
---
```
#!/bin/bash

###############-ATTENTION-###############

echo -e " \e[31m!Attention!\e[0m "

echo -e "\e[91mJust 20 Numbers no more no less\e[0m "

################-CONFIG-#################

while [ $(echo $NUMS | tr " " "\n" | wc -l) -ne 20 ]

do

		read -p "Enter 20 numbers: " NUMS

done

MAX=`echo $NUMS | tr ' ' '\n' | sort -n | tail -1 `

MIN=`echo $NUMS | tr ' ' '\n' | sort -n | head -1 `

echo "Max Number is: $MAX"

echo "MIN Number is: $MIN"
 
#DONE
```
---

# Exercise 3
###### Exercise 3: Write a program that has the IP of a server and its User/Pass in front of the Script name and if it is pingable, sends its /etc/passwd file to /home/user path of that server, otherwise a message displayed that the server is not accessible.
---
```
#!/bin/bash

####################-VARS-####################

IP=$1

USER=$2

PASS=$3

####################-CONFIG-####################

if ping -c 1 "$IP" > /dev/null 2>&1

then

		echo "Server is pingable"

		sshpass -p "$PASS" scp /etc/passwd "$USER@$IP:/home/$USER/"

else

		echo "server is not accessible"

fi

#DONE
```
---
# Exercise 4
###### Exercise 4: Write a program that prints from 5 to 50 on the screen.
---
```
#!/bin/bash

####################-CONFIG-####################

for i in {5..50}

do

		echo "Number is $i"

done

#DONE
```
---
# Exercise 5
###### Exercise 5: Write a program that saves the first and third fields of the /etc/passwd file every day in a file with the same date and does not hold it for more than two days.
---
```
#!/bin/bash

####################-VARS-####################

DATE=$(date +%F)

FILE="$DATE.txt"

####################-CONFIG-####################

cut -d ":" -f 1,3 /etc/passwd > ~/Practice/Practice_05_dir/$FILE

find ./Practice_05_dir -name "*.txt" -mtime 2 -delete

#DONE
```
---
# Exercise 6
###### Exercise 6: Write a program that take a backup from home directory of your user after each time user logged out.
---
```
#!/bin/bash

####################-CONFIG-####################

tar -cJf backup-$(date +%F%H%M).tar.xz /home/artin

#DONE
```
---
# Exercise 7
###### Exercise 7: Write a program that reads, pings one by one from within a file containing the list of destination IPs, and saves the result in a log file on the same day with the hostname of that machine.
---
```
#!/bin/bash

####################-VARS-####################

DATE=$(date +%F)

LOG="$DATE.log"

HOST=$(hostname)

####################-CONFIG-####################

while read IP

do

		if ping -c 1 "$IP" > /dev/null 2>&1

		then

				echo "$HOST - $IP is UP!" >> "$LOG"

		else

				echo "$HOST - $IP is DOWN!!" >> "$LOG"

		fi

done < ips.txt

echo "----------------------" >> "$LOG"

#DONE
```
---
# Exercise 8
###### IP Validation
---
```
#!/bin/bash

####################-VARS-####################

VALID=0

####################-CONFIG-####################

while [ -z $IP ]

do

		read -p "Enter Your IP Address:" IP

done

IP=`echo $IP | tr -d [:blank:] | tr -d [:alpha:]`

NUMBER_OCTETS=`echo $IP | cut -d '.' -f 1- | tr '.' '\n' | wc -l`

if [ $NUMBER_OCTETS -ne 4 ]

then

		echo "IP is Invalid!"

else

		for i in {1..4}

do

OCTET=`echo $IP | cut -d "." -f $i`

if [ -z $OCTET ]

then

		echo "Empty Octet"

		let VALID=VALID-1

fi

if [ $OCTET -gt 255 ] > /dev/null 2>&1|| [ $OCTET -lt 0 ] > /dev/null 2>&1

then

		let VALID=VALID-1

else

		let VALID=VALID+1

fi

done

if [ $VALID -eq 4 ]

then

	if ping -c 1 "$IP" > /dev/null 2>&1
	
	then
	
			echo -e " \e[32m!PINGABLE!\e[0m "
	
			echo -e "Average Ping $IP: \e[32m$(ping -c 2 "$IP" | tail -1 | cut -d '=' -f 2 | cut -d "/" -f 2)\e[0m ms" | tee -a Practice_08_output.txt
			
			echo "-----------------------------------" >> Practice_08_output.txt
	
	else
	
			echo -e " \e[31m!NOT PINGABLE!\e[0m "
			
			echo -e "Average Ping $IP: \e[31m-1\e[0m ms" | tee -a Practice_08_output.txt
			
			echo "-----------------------------------" >> Practice_08_output.txt

		fi
	
	fi

  

fi
```
---
