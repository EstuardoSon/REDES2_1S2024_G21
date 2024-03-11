## SW1
```CMD
enable
config t
hostname SW1

vlan 63
name corporativo63

interface range f0/3-4
channel-group 1 mode active
no shutdown
exit

interface po1
switchport mode trunk
switchport trunk allowed vlan 63

interface range f0/9-11
switchport mode access
switchpor access vlan 63
no shutdown

exit
```

## MSW1
```CMD
enable
config t
hostname MSW1

vlan 63
name corporativo63
vlan 13
name ventas13

interface range f0/3-4
channel-group 1 mode active
no shutdown
exit

interface po1
switchport mode trunk
switchport trunk allowed vlan 63

interface vlan 63
ip address 192.168.63.1 255.255.255.0
no shutdown

interface vlan 13
ip address 1.0.0.1 255.0.0.0
no shutdown

exit
```

## SW3
```CMD
enable
config t
hostname SW3

vlan 63
name corporativo63

interface range f0/3-4
channel-group 1 mode active
no shutdown
exit

interface po1
switchport mode trunk
switchport trunk allowed vlan 63

interface range f0/9-10
switchport mode access
switchport access vlan 63
no shutdown

exit
```

## MSW7
```CMD
enable
config t
hostname MSW7

vlan 63
name corporativo63
vlan 23
name distribucion23

interface range f0/3-4
channel-group 1 mode active
no shutdown
exit

interface po1
switchport mode trunk
switchport trunk allowed vlan 63

interface vlan 63
ip address 192.168.73.1 255.255.255.0
no shutdown

interface vlan 23
ip address 2.0.0.1 255.0.0.0
no shutdown

exit
```

## SW2
```CMD
enable
config t
hostname SW2

vlan 63
name corporativo63

interface range f0/3-4
channel-group 1 mode active
no shutdown
exit

interface po1
switchport mode trunk
switchport trunk allowed vlan 63

interface f0/9
switchport mode access
switchport access vlan 63
no shutdown

exit
```

## MSW4
```CMD
enable
config t
hostname MSW4

vlan 63
name corporativo63
vlan 13
name ventas13
vlan 23
name distribucion23

interface range f0/3-4
channel-group 1 mode active
no shutdown
exit

interface po1
switchport mode trunk
switchport trunk allowed vlan 63

interface vlan 63
ip address 192.168.83.1 255.255.255.0
no shutdown

interface vlan 13
ip address 1.0.0.2 255.0.0.0
no shutdown

interface vlan 23
ip address 2.0.0.2 255.0.0.0
no shutdown

exit
```

