

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303181157.png)

## ECHO

to sabe variable that are rewriting. this are storage in REM
```
# print a question using  ECHO
echo "entre your name: "
```

```
$name

echo $name
```

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303181903.png)

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303182008.png)



```
## To create a new bash

sudo nano myfirstbash.shD
```

```

#!/bin/bash

# followeed by exclaimation links from library

#comment statment

echo -n "Welcome to the class. What is yout name"
read name
echo "Hello $name welcom and join the fun...?"

ctrl + X
```

ls -l /bin/bash
ls - l myfirstbash.sh
sudo chmod 755 myfirstbash.sh

ls - l myfirstbash.sh
bash myfirstbash.sh

\\ backslash
![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303182714.png)
![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303182902.png)

```
#!/bin/bash

# followeed by exclaimation links from library

#comment statment

#echo -n "Welcome to the class. What is yout name"
#read name
#echo "Hello $name welcom and join the fun...?"



echo "Welcom to Maths class..."

echo -n "enter number a: "
read a

echo -n "enter number b:  "
read b
c=`expr $a + $b`

echo "Sum of $a and $b is $c"

```



![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303184525.png)

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303184558.png)

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303184840.png)


```
#!/bin/bash

# followeed by exclaimation links from library

#comment statment

#echo -n "Welcome to the class. What is yout name"
#read name
#echo "Hello $name welcom and join the fun...?"



echo "Welcom to Maths class..."

echo -n "enter number a: "
read a

echo -n "enter number b:  "
read b
c=`expr $a + $b`
echo "Sum of $a and $b is $c"

c=`expr $a - $b`
echo "Difference of $a and $b is $c"

c=`expr $a \* $b`
echo "Product of $a and $b is $c"

c=`expr $a % $b`
echo "Reminder of $a and $b is $c"

c=`expr $a / $b`
echo "quotient of $a and $b is $c"


echo -n "enter a new number to print its table : "
read num
ctr=1

## -LE is less and equal
while [ $ctr -le 10 ]
do 
	output=`expr $num \* $ctr`
	echo "$num * ctr = $output"
	$ctr=`expr $ctr + 1`
done

#for (inicial valur , final valu, inc or dec value)
		#statement
#while [condition]
#do
		#statement
#done

#until
#do 
		#statement
#done
#[condition]
``` 

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303185251.png)

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303190319.png)

```

sudo nano math.sh

echo -n "Enter a number to print its table: "
read num
ctr=1

while [ $ctr -le 10 ]; do
    output=`expr $num \* $ctr`
    echo "$num * $ctr = $output"
    ctr=`expr $ctr + 1`      
done
 ```

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303191329.png)

![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303192014.png)

```
ctr=ls0
a=0
b-1
echo $a
echo$b
while [$ctr -le 10]
do
	c=`expr $a + $b`
	echo $c
	a=$b
	b=$c
	ctr=`expr $ctr + 1`
#if statement
	if  [$ctr == 5]
	then
		break
	fi
done
```


![](../IMG/IMG-%20Class%204%20-%2003.03.2025%20-%20Linux%20-%20Operators%20and%20Operands%20Class%20I/Pasted%20image%2020250303192755.png)