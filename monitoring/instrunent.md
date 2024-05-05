###CPU

````
vmstat 1

top
````

###DISK
````
df -h

yum -y install sysstat
iostat -dxyt
````

###RAM
````
free -h
````

###NET
````
ifconfig

ifconfig enp0s9

sar -n DEV
sar -n EDEV

netstat -s
````