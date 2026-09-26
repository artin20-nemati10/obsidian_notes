
# Percentage 
---
```
#!/bin/bash

  

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

echo
```
----
# Simple
```
#!/bin/bash

  
  

Progress_bar()

{

for i in {1..20}

do # Progress Bar

printf '\e[95m%.0s.\e[0m'

sleep 0.2

done

}

Progress_bar
```