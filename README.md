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
while getouts :xy: opt_char
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
```
