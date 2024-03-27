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

## LACP Red de Edificios

``` CMD
ena
config t

! Configuracion de vlans
vlan 20
name D
vlan 30
name E
vlan 40
name F

! Configuracion de LACP
int range f0/1-3
channel-group 1 mode active
no shutdown
exit

! Configuracion de interfaz po1
int po1
switchport mode access
switchport access vlan 40
exit

! Configuracion de interfaz de acceso
int f0/12
switchport mode access
switchport access vlan 20
exit

int f0/9
switchport mode access
switchport access vlan 30
exit

! Configuracion de interfaz vlan
int vlan 40
ip add 40.#.21.1 255.255.255.252
no shutdown
exit

int vlan 20
ip add 20.#.21.1 255.255.255.252
no shutdown
exit

int vlan 30
ip add 30.#.21.1 255.255.255.252
no shutdown
exit
```

## SW Edificios (IZQ)

``` CMD
ena
config t

! Configuracion de vlans
vlan 40
name F
vlan 50
name G
vlan 60
name H
vlan 70
name I

! Configuracion de LACP
int range Gig1/0/1-3
channel-group 1 mode active
no shutdown
exit

! Configuracion de interfaz de acceso
int range Gig1/1/2
switchport mode access
switchport access vlan 60
exit

int range Gig1/1/3
switchport mode access
switchport access vlan 50
exit

int range Gig1/1/1
switchport mode access
switchport access vlan 70
exit

! Configuracion de interfaz po1
int po1
switchport mode access
switchport access vlan 40
exit

! Configuracion de interfaz vlan
int vlan 40
ip add 40.0.21.2 255.255.255.252
no shutdown
exit

int vlan 50
ip add 50.0.21.1 255.255.255.252
no shutdown
exit

int vlan 60
ip add 60.0.21.1 255.255.255.252
no shutdown
exit

int vlan 70
ip add 70.0.21.1 255.255.255.252
no shutdown
exit
```

## SW Edificios (DER)

``` CMD
ena
config t

! Configuracion de vlans
vlan 40
name F
vlan 50
name G
vlan 61
name I
vlan 71
name H

! Configuracion de LACP
int range Gig1/0/1-3
channel-group 1 mode active
no shutdown
exit

! Configuracion de interfaz de acceso
int range Gig1/1/2
switchport mode access
switchport access vlan 71
exit

int range Gig1/1/3
switchport mode access
switchport access vlan 50
exit

int range Gig1/1/1
switchport mode access
switchport access vlan 61
exit

! Configuracion de interfaz po1
int po1
switchport mode access
switchport access vlan 40
exit

! Configuracion de interfaz vlan
int vlan 40
ip add 40.1.21.2 255.255.255.252
no shutdown
exit

int vlan 50
ip add 50.0.21.2 255.255.255.252
no shutdown
exit

int vlan 61
ip add 60.1.21.1 255.255.255.252
no shutdown
exit

int vlan 71
ip add 70.1.21.1 255.255.255.252
no shutdown
exit
```

## SW Edificios (UP)

``` CMD
ena
config t

! Configuracion de vlans
vlan 60
name H
vlan 61
name I

! Configuracion de interfaz de acceso
int range Gig1/1/2
switchport mode access
switchport access vlan 60
exit

int range Gig1/1/1
switchport mode access
switchport access vlan 61
exit

! Configuracion de interfaz vlan
int vlan 60
ip add 60.0.21.2 255.255.255.252
no shutdown
exit

int vlan 61
ip add 60.1.21.2 255.255.255.252
no shutdown
exit
```

## SW Edificios (DOWN)

``` CMD
ena
config t

! Configuracion de vlans
vlan 70
name I
vlan 71
name H

! Configuracion de interfaz de acceso
int range Gig1/1/2
switchport mode access
switchport access vlan 71
exit

int range Gig1/1/1
switchport mode access
switchport access vlan 70
exit

! Configuracion de interfaz vlan
int vlan 70
ip add 70.0.21.2 255.255.255.252
no shutdown
exit

int vlan 71
ip add 70.1.21.2 255.255.255.252
no shutdown
exit
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