## Configuration SW1

```CMD
!--- Nombre del Hostname
hostname SW1_G21

!--- Configuración de las interfaces troncales
int range fa0/1-5
switchport mode trunk 
switchport trunk allowed vlan 13,23,33
exit

!--- Creación de las VLAN
vlan 13
name PRIMARIA

vlan 23
name BASICOS

vlan 33
name DIVERSIFICADOS
exit

!--- Configuración de VTP
vtp version 2
vtp domain g21
vtp mode server

do write
```

## Configuration SW2, SW3, SW8 y SW9

```CMD
!--- Nombre del Hostname
hostname SW#A_G21

!--- Configuración de las interfaces troncales
int range fa0/1-5
switchport mode trunk 
switchport trunk allowed vlan 13,23,33
exit

!--- Creación de las VLAN
vtp version 2
vtp domain g21
vtp mode client

do write
```

#A: Hace referencia al numero del switch que se esta configurando, en este caso SW2, SW3, SW8 y SW9.

## Configuration SW5, SW7, SW10 y SW12

```CMD
!--- Nombre del Hostname
hostname SW#A_G21

!--- Configuración de las interfaces troncales
int range fa0/1-2
switchport mode trunk 
switchport trunk allowed vlan 13,23,33
exit

!--- Configuración de las interfaces de acceso
int range fa0/3-4
switchport mode access
switchport access vlan 33
exit

!--- Creación de las VLAN
vtp version 2
vtp domain g21
vtp mode client

do write
```

#A: Hace referencia al numero del switch que se esta configurando, en este caso SW5, SW7, SW10 y SW12.

#V: Hace referencia al numero de la VLAN que se esta configurando, en este caso 13 para SW5 y 12; y 33 para vlan 7 y 10.

## Configuration SW6 y SW11

```CMD
!--- Nombre del Hostname
hostname SW#A_G21

!--- Configuración de las interfaces troncales
int range fa0/1-2
switchport mode trunk 
switchport trunk allowed vlan 13,23,33
exit

!--- Configuración de las interfaces de acceso
int range fa0/3
switchport mode access
switchport access vlan 23
exit

!--- Creación de las VLAN
vtp version 2
vtp domain g21
vtp mode client

do write
```

#A: Hace referencia al numero del switch que se esta configurando, en este caso SW6 y SW11.