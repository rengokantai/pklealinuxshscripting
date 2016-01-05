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
