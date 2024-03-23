## Capa de Distribucion

``` CMD
ena
config t 

vlan 10
name A
vlan 20
name B
exit

vtp mode server
vtp domain grupo21
vtp password grupo21
vtp version 2

int range f0/1-2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 10,20
exit

```

## Capa de acceso

``` CMD
ena
config t

vtp version 2
vtp domain grupo21
vtp password grupo21
vtp mode client

int range f0/1
switchport mode trunk
switchport trunk encapsulation dot1q
exit

int range f0/2-3
switchport mode access
switchport access vlan #
```