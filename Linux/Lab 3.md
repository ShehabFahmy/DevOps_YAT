1. Create a script that asks for user name then greets him:
```bash
#!/bin/bash
echo -n "Enter Username: "   # -n to write in same line
read username
echo "Hello, $username"
```
2. Create a script called `s1` that calls another script `s2` where:
	- In `s1` there is a variable called `x`, it's value `5`.
	- Try to print the value of `x` in `s2` by two different ways.
`s1`:
```bash
#!/bin/bash                    #!/bin/bash
x=5                            x=5
./s2.sh $x                     source ./s2.sh
```
`s2`:
```bash
#!/bin/bash                    #!/bin/bash
echo "x = $1"                  echo "x = $x"
```
3. Create a script called `mycp` where:
	- It copies a file to another.
	- It copies multiple files to a directory.
```bash
#!/bin/bash
last_index=$(( $# ))
before_last=$(( $#-1 ))
if [ -d ${!last_index} ]; then
	for num in `seq 1 $before_last`
	do
		if [ -f ${!num} ]; then
			cp ${!num} ${!last_index}
		else
			echo "Failed: ${!num} is not a file"
		fi
	done
else
	echo "Failed: last argument must be a directory"
fi
```
4. Create a script called `mycd` where:
	- It changes directory to the user home directory, if it is called without arguments.
	- Otherwise, it changes directory to the given directory.
```bash
#!/bin/bash
if [ $# -gt 0 ]; then
	cd $1
else
	cd ~
fi
```
***Note:*** In order to work, run as source or make an alias.
5. Create a script called `myls` where:
	- It lists the current directory, if it is called without arguments.
	- Otherwise, it lists the given directory.
```bash
#!/bin/bash
if [ -z $1 ]; then
	ls
else
	ls $1
fi
```
6. Enhance the above script to support the following options individually:
	- `–l`: list in long format
	- `–a`: list all entries including the hiding files.
	- `–d`: if an argument is a directory, list only its name
	- `–i`: print inode number
	- `–R`: recursively list sub-directories
```bash
#!/bin/bash
if [ -z $1 ]; then
	ls
elif [ $1 == -l ]; then
	ls -l
elif [ $1 == -a ]; then
	ls -a
elif [ $1 == -d ]; then
	ls -d
elif [ $1 == -i ]; then
	ls -i
elif [ $1 == -R ]; then
	ls -R
else
	ls $1
fi
```
7. Write a script called `mycase`, using the case utility to check the type of character entered by a user:
	- Upper Case.
	- Lower Case.
	- Number.
	- Nothing.
```bash
#!/bin/bash
read -p "Enter Char: " char
case $char in
	[A-Z])
		echo "Uppercase";;
	[a-z])
		echo "Lowercase";;
	[0-9])
		echo "Number";;
	*)
		echo "Nothing";;
esac
```
8. Enhanced the previous script, by checking the type of string entered by a user:
	- Upper Cases
	- Lower Cases
	- Numbers
	- Mix
	- Nothing
```bash
#!/bin/bash
read -p "Enter String: " s
upper_cnt=0
lower_cnt=0
num_cnt=0
for i in `seq 0 ${#s}`   # for (( i=0; i<${#s}; i++ ))
do
	char=${s:i:1}   # Substring start at i and take 1 char
	case $char in
		[A-Z])
			(( upper_cnt++ ));;
		[a-z])
			(( lower_cnt++ ));;
		[0-9])
			(( num_cnt++ ));;
	esac
done
case ${#s} in
	$upper_cnt)
		echo "Uppercases";;
	$lower_cnt)
		echo "Lowercases";;
	$num_cnt)
		echo "Numbers";;
	$(( upper_cnt+lower_cnt+num_cnt )))
		echo "Mix";;
	*)
		echo "Nothing";;
esac
```
