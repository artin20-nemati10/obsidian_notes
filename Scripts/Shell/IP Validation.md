```
#!/bin/bash

  

#Practice_08 IP_Validation

  

###################FUNCTIONS######################

SUCCESS()

{

echo -e "\e[32m[SUCCESS] \e[0m"

}

#------------------------------------

  

FAILED()

{

echo -e "\e[31m[FAILED] \e[0m"

}

#------------------------------------

  

INFO()

{

echo -e "\e[35m[INFO] \e[0m"

}

#------------------------------------

  

Progress_bar()

{

for i in {1..100}

do

FILLED=$((i / 5))

EMPTY=$((20 - FILLED))

  

BAR=$(printf '\e[33m%0.s#\e[0m' $(seq 1 $FILLED))

if [ "$EMPTY" -gt 0 ]; then

SPACES=$(printf '\e[33m%0.s-\e[0m' $(seq 1 $EMPTY))

else

SPACES=""

fi

printf "\r[%s%s] %d%%" "$BAR" "$SPACES" "$i"

  

sleep 0.005

done

  

}

####################-CONFIG-####################

BREAK=0

while [ $BREAK -eq 0 ] # All Empty

do

VALID=0

if [ -z $IP ]

then

read -p "Enter Your IP Address: " IP

else

IP=`echo $IP | tr -d [:blank:] | tr -d [:alpha:]` # Delete the spaces and chars

  

NUMBER_OCTETS=`echo $IP | cut -d '.' -f 1- | tr '.' '\n' | wc -l` # Octets

  

if [ $NUMBER_OCTETS -ne 4 ] # 4 Octet Validation

then

  

echo -e "$(INFO) \e[33mInvalid Octets\e[0m"

BREAK=0

IP=""

else

  

for i in {1..4} # Single Octet Validation

do

OCTET=`echo $IP | cut -d "." -f $i`

  

if [ -z $OCTET ] # Empty Octet Validation

then

  

echo -e "$(INFO) \e[33mOctets should not be Empty\e[0m"

VALID=0

BREAK=0

break

  

fi

  

if [ $OCTET -gt 255 ] > /dev/null 2>&1|| [ $OCTET -lt 0 ] > /dev/null 2>&1 # Every Octet between 0-255

then

BREAK=0

echo -e "$(INFO) \e[33mEvery Octet Should be 0-255\e[0m"

break

else

  

let VALID=VALID+1

  

fi

  

done

if [ $VALID -ne 4 ]

then

IP=""

continue

fi

  

if [ $VALID -eq 4 ] # Pinging the IP

then

  

if ping -c 1 "$IP" > /dev/null 2>&1 # Pingable IP

then

  

Progress_bar

#------------------------------------

PING=$(ping -c 1 "$IP" | tail -1 | cut -d '=' -f 2 | cut -d "/" -f 2)

echo -e "\n$(SUCCESS)Average Ping $IP: \e[32m$PING\e[0m ms"

echo -e "\n$(SUCCESS) | $(hostname) | $IP | \e[32m$PING\e[0m ms" >> ~/IP_VALIDATION.log

#echo "-----------------------------------" >> ~/IP_VALIDATION.log

BREAK=1

else

# Not Pingable IP

PING=$(ping -c 1 "$IP" | tail -1 | cut -d '=' -f 2 | cut -d "/" -f 2)

Progress_bar

echo -e "\n$(FAILED) Average Ping $IP: \e[31m-1\e[0m ms"

echo -e "\n$(FAILED) | $(hostname) | $IP | \e[31m-1\e[0m ms" >> ~/IP_VALIDATION.log

#echo "-----------------------------------" >> ~/IP_VALIDATION.log

BREAK=1

fi

fi

fi

fi

done
```