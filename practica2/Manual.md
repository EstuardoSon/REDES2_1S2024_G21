## SW1
```CMD
enable
config t
hostname SW1

vlan 73
name A

interface range f0/3-4
channel-group 2 mode active
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

interface range f0/3-4
channel-group 1 mode active
no shutdown
exit

```