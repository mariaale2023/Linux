```
sudo nano newfile.sh

#!/bin/bash

##---for statement of conditions-------

#do 
	#statement
#done


i=0
for i in 1 2 3 4 5
do
	echo "welcome i $i times."
done


for i in {1..5}
do
	echo "welcome i $i times."
done

for i in {1..15..2}
do 
	echo "welcome i $i times."
done
```

![](../IMG/IMG-%20Class%205%20-%2004.03.2025%20-%20Linux%20-%20Introduction%20to%20Bash%20Scripting%20-%20Class%20II/Pasted%20image%2020250304181440.png)

this las imagen shows an image because  we added space between {} example  this {1..5} vs { 1..5 }

if we remove the space in side of bracket, we get:
![](../IMG/IMG-%20Class%205%20-%2004.03.2025%20-%20Linux%20-%20Introduction%20to%20Bash%20Scripting%20-%20Class%20II/Pasted%20image%2020250304181800.png)


```
sudo nano newfile.sh

#!/bin/bash

##---for statement of conditions-------

#do 
	#statement
#done


i=0
for i in 1 2 3 4 5
do
	echo "welcome i $i times."
done


for i in {1..5}
do
	echo "welcome i $i times."
done

for i in {1..15..2}
do 
	echo "welcome i $i times."
done

echo ""
echo ""

for i in $(seq 1 2 15 )
do 
	echo "welcome i $i times."
done

```

![](../IMG/IMG-%20Class%205%20-%2004.03.2025%20-%20Linux%20-%20Introduction%20to%20Bash%20Scripting%20-%20Class%20II/Pasted%20image%2020250304182013.png)

```
# i++ | ++i | i+=1 ==> i=i+1

#!/bin/bash

spc = " "
j=5
 for (( i=1; i<=5; i++ ))
 do 
 
	 for ((j=1; j<=5: j++))
	 do
		 if [ $j -ge $((6-$i)) ]
			 then
				 echo -n "$spc"
	done
		echo -n "$i"


```

![](../IMG/IMG-%20Class%205%20-%2004.03.2025%20-%20Linux%20-%20Introduction%20to%20Bash%20Scripting%20-%20Class%20II/Pasted%20image%2020250304184223.png)
```


```