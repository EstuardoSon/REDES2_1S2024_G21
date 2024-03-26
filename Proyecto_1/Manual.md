## Capa de Distribucion

``` CMD
ena
config t 

! Configuracion de vlans
vlan 100
name A
vlan 200
name B
vlan 10
name C
exit

! Configuracion de VTP
vtp mode server
vtp domain grupo21
vtp password grupo21
vtp version 2

! Configuracion de enlaces troncales
int range f0/1-2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 100,200
exit

! Configuracion de interfaz vlan
int vlan 10
ip add 10.#.21.4 255.255.255.248
no shutdown

! Configuracion de interfaz de acceso
int f0/11
switchport mode access
switchport access vlan 10
exit

int f0/10
switchport mode access
switchport access vlan 10
exit
```

## Switches HSRP (IZQ)

``` CMD
ena
config t

! Configuracion de vlans
vlan 10
name C
vlan 20
name D

! Configuracion de HSRP
int vlan 10
ip add 10.#.21.2 255.255.255.248
no shutdown
standby version 2
standby 10 ip 10.#.21.1
standby 10 preempt
exit

! Configuracion de interfaz vlan
int vlan 20
ip add 20.#.21.1 255.255.255.252
no shutdown

! Configuracion de interfaz de acceso
int f0/11
switchport mode access
switchport access vlan 10
exit

int f0/12
switchport mode access
switchport access vlan 20
exit
```

## Switches HSRP (DER)

``` CMD
ena
config t

! Configuracion de vlans
vlan 10
name C
vlan 30
name E

! Configuracion de HSRP
int vlan 10
ip add 10.#.21.3 255.255.255.248
no shutdown
standby version 2
standby 10 ip 10.#.21.1

! Configuracion de interfaz vlan
int vlan 30
ip add 30.#.21.1 255.255.255.252
no shutdown

! Configuracion de interfaz de acceso
int f0/10
switchport mode access
switchport access vlan 10
exit

int f0/9
switchport mode access
switchport access vlan 30
exit
```

## LACP (IZQ)

``` CMD
ena
config t

! Configuracion de vlans
vlan 100
```

## Capa de acceso

``` CMD
ena
config t

! Configuracion de vtp
vtp version 2
vtp domain grupo21
vtp password grupo21
vtp mode client

! Configuracion de interfaz truncal
int range f0/1
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 100,200
exit

! Configuracion de interfaz de acceso
int range f0/2-3
switchport mode access
switchport access vlan #
exit


```