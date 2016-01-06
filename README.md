

#### pklealinuxshscripting

- cp4
exit status
```
ls
echo $?
```
(If prints out 0, it indicates success(non-zero indicates an error)

- cp5
```
a=20
echo $a
unset a
```
```
declare -x varname=value
```
Some traps:
```
var="value"
echo $var     # value
echo "$var"   # value
echo '$var'   # $var
echo \$var    # $var
```
$$ is current process ID of the current shell.
```
echo $$
(1234)
```
print out timezone(for Redhat/fedora /etc/localtime)
```
cat /etc/timezome
```

Export sh:
```
#sh1.sh
foo="foo"
export bar="bar"
./sh2.sh
```
```
#sh2.sh
echo $foo  # will print blank line
echo $bar  # ok
```

Readonly vars:
```
readonly var=value
```
Or
```
declare -r var=value
```
You can not unset readonly values.

shift:
```
set arg1 arg2 arg3 arg4
echo $1    # arg1
shift 1 
echo $1    # arg2
shift 2
echo $1    # arg4
```
```
$1-$9
${10}
$#  #number of vars
$*  print all args
$@  print all args one by one
"$*"   "$1$2$3"
"$@"  "$1""$2""$3"
```

getopts:
```y
USAGE="usage: $0 -x -y"
while getopts :xy: opt_char
do
case opt_char in
x)
echo "x"
;;
y)
echo "$OPTARG"
;;
\?)
echo "$USAGE"
;;
esac
done
```

Default var:
```
# d.sh
var1=$1
var2=${2:-$var1}
echo $var1
echo $var2
```
Execute:
```
./d.sh a  # will print a a
./d.sh a b  # will print a b
```

Arrays:
```
FRUIT=(Apple Banana)
echo ${FRUIT[*]}    # Apple Banana
echo ${FRUIT[1]}    # Banana
FRUIT[2]=Orange
echo ${FRUIT[*]}    # Apple Banana Orange
```
```
declare -a FRUIT=(a b c)
echo ${FRUIT[*]}
echo ${#FRUIT[*]}   # arr len
```
non-regular assign
```
fish=(eel [2]=piranha [1]=carp)
```
- cp6
raed with prompt
```
read -p "Enter value: "  var
echo $value
```
Or, using built-in $REPLY
```
read
echo $REPLY
```
Read args as array:
```
read arg1 arg2 arg3
echo $arg1
....
```
Or
```
echo -n "Please input.."
read -a arrayargs     # -a tag
echo ${arrayargs[0]}
....
```

EOF, <<
First example. send email
```
tar -cvf /dev/st0 /home/stu 2>/dev/null
[$? -eq 0] && status="success"||status="fail"
mail -s 'title' z@z.com <<EOF
$status
$(date)
EOF
```
Second exapmle, vim
```
ed x.txt <<quit
,s/old/new/g
w
q
quit
```
wall command is used for sending message to all logged users

To avoid var substitution, we need to add quote
```
cat << 'EOF'
$a
EOF
```
will print $a.

 here string. <<<
 ```
 wc -c <<< 'sample string'
 ```
 File handling
 
 
 Debugging
 To check syntax error
 ```
 bash -n x.sh
 ```
 
 -v #verbose
 -x #show trace
 ```
 bash +vx #disable options vx
 bash -vx #enable options vx
 ```
 In bash script,
 ```
 set -x #enable debigging
 set +x #diable debugging
 ```
 
 

- cp7
expr  (in /uer/bin/expr)
```
expr 42 % 10     #2
expr 4 \* 10     #40
expr "4 * 10"    #40
```

Two syntax:
```
a=1
b=2
c=$((a+b))
c=$[$a+$b]
c=$[a+b]  #ok
```

Number system. syntax: base#numberinthatbase
```
declare -i x
x=8#25  #21
x=2#10101  #21
```

Floating-point arithmetic (use bc utility)
```
echo "scale=2;15/2" |bc  #7.50
```
use awk:
```
result = `awk -v a=1 -v b=2 'BEGIN{printf "%.2f\n", a*b}'`
```


- cp8
set IFS
```
file=/etc/resolv.conf
while IFS=read -r line
do
  echo $line
done < "$file"
```
until (use commands)
```
until who | grep "$1" > /dev/null
do
 sleep 40
done
echo -e \\a
```
To execute:
```
xx.sh username
```

piping out for loops
```
for value in 1 2 3
do
 echo $value
done | sort -n
```

Running in backgorund
```
for value in 1 2 3
do
 echo $value
done &
```

Reassign IFS
```
#!
longword = "a:b:c"
IFS=":"
for char in longword
do
 echo $char
done
```

- cp9
declare local var in func
```
x = 1
funcname(){
local x =2
}
echo $x   #1
```
- cp11
ctrl alt t  # create a new interactive shell





- cp12
sed
```
sed '3d' x.txt  # delete line 3
sed '1,3d' x.txt # delete line 1-3
sed '3,$d' x.txt # delete lines other than 3
```

awk

scr.sh
```
/pattern/{print $1,$2}
```
Exucete:
```
awk -f scr.sh filename
```
```
awk -f

