## SW1
```CMD
enable
config t
hostname SW1

vlan 73
name A

interface range f0/3-4
channel-group 1 mode active
switchport mode trunk
switchpor trunk allowed vlan 73
no shutdown
exit

interface range f0/9-11
switchport mode access
switchport access vlan 73
no shutdown

exit
```

## MSW1
```CMD
enable
config t
hostname MSW1

vlan 73
name A
vlan 10
name B

interface range f0/3-4
channel-group 1 mode active
switchport mode trunk
switchpor trunk allowed vlan 73
no shutdown
exit

interface vlan 73
ip address 192.168.73.1 255.255.255.0
no shutdown

interface vlan 10
ip address 1.0.0.1 255.0.0.0
no shutdown

exit
```

## SW3
```CMD
enable
config t
hostname SW3

vlan 93
name A

interface range f0/3-4
channel-group 1 mode active
switchport mode trunk
switchpor trunk allowed vlan 93
no shutdown
exit

interface range f0/9-10
switchport mode access
switchport access vlan 93
no shutdown

exit
```

## MSW7
```CMD
enable
config t
hostname MSW7

vlan 93
name A
vlan 20
name C

interface range f0/3-4
channel-group 1 mode active
switchport mode trunk
switchpor trunk allowed vlan 93
no shutdown
exit

interface vlan 93
ip address 192.168.93.1 255.255.255.0
no shutdown

interface vlan 20
ip address 2.0.0.1 255.0.0.0
no shutdown

exit
```

## SW2
```CMD
enable
config t
hostname SW2

vlan 83
name A

interface range f0/3-4
channel-group 1 mode active
switchport mode trunk
switchpor trunk allowed vlan 83
no shutdown
exit

interface f0/9
switchport mode access
switchport access vlan 83
no shutdown

exit
```

## MSW4
```CMD
enable
config t
hostname MSW4

vlan 83
name A
vlan 10
name B
vlan 20
name C

interface range f0/3-4
channel-group 1 mode active
switchport mode trunk
switchpor trunk allowed vlan 83
no shutdown
exit

interface vlan 83
ip address 192.168.83.1 255.255.255.0
no shutdown

interface vlan 10
ip address 1.0.0.2 255.0.0.0
no shutdown

interface vlan 20
ip address 2.0.0.2 255.0.0.0
no shutdown

exit
```

