## Subneting
### Akado: 192.168.31.0 /24
|Nombre de Red|Subred|Gateway|Mascara de Subred|Abreviatura|
|-------------|------|-------|------------------|-----------|
| Rostec | 192.168.31.0 | 192.168.31.1 | 255.255.255.192 | /26 |
| Sberbank | 192.168.31.64 | 192.168.31.65 | 255.255.255.192 | /26 |
| MSW1 - Akado | 192.168.31.128 | - | 255.255.255.252 | /30 |

### Yota: 192.168.41.0 /24
|Nombre de Red|Subred|Gateway|Mascara de Subred|Abreviatura|
|-------------|------|-------|------------------|-----------|
| Rostec | 192.168.41.0 | 192.168.41.1 | 255.255.255.192 | /26 |
| Sberbank | 192.168.41.64 | 192.168.41.65 | 255.255.255.192 | /26 |
| MSW3 - Yota | 192.168.41.128 | - | 255.255.255.252 | /30 |

### Rostelecom: 192.168.71.0 /24
|Nombre de Red|Subred|Gateway|Mascara de Subred|Abreviatura|
|-------------|------|-------|------------------|-----------|
| Rostec | 192.168.71.0 | 192.168.71.1 | 255.255.255.192 | /26 |
| Sberbank | 192.168.71.64 | 192.168.71.65 | 255.255.255.192 | /26 |
| MSW3 - Yota | 192.168.71.128 | - | 255.255.255.252 | /30 |

### ISP
|Nombre de Red|Subred|Gateway|Mascara de Subred|Abreviatura|
|-------------|------|-------|------------------|-----------|
| Akado - Rostelecom | 10.10.10.0 | - | 255.255.255.252 | /30 |
| Akado - Yota | 20.20.20.0 | - | 255.255.255.252 | /30 |
| Rostelecom - Yota | 30.30.30.0 | - | 255.255.255.252 | /30 |  

## RED de Akado
### Rostec1 y Rostec2
```
vtp domain g21
vtp password g21
vtp mode client

int f0/1
switchport mode trunk
exit

int range f0/2-3
switchport mode access
switchport access vlan 10
exit
```

### Sberbank
```
vtp domain g21
vtp password g21
vtp mode client

! Configura LACP

int range fa0/1-2
channel-group 2 mode active
exit

int po1
switchport mode trunk
exit

int f0/3
switchport mode access
switchport access vlan 20
exit
```

### Switch5
```
vlan 10
name Rostec
vlan 20
name Sberbank
exit

vtp domain g21
vtp password g21
vtp mode server
vtp version 2

! Configura LACP

int range f0/1-2
channel-group 2 mode active
exit

int range f0/4-5
channel-group 1 mode active
exit

int range fa0/3, fa0/6
switchport mode trunk
exit

int po1
switchport mode trunk
exit

int po2
switchport mode trunk
exit
```

### MSW1
```
vlan 10
name Rostec
vlan 20
name Sberbank
exit

! Configuracion LACP

int range f0/2-3
channel-group 2 mode active
exit

int po1
switchport mode trunk
exit

! Interfaz de VLAN

int vlan 10
ip address 192.168.31.1 255.255.255.192
no shutdown
exit

int vlan 20
ip address 192.168.31.65 255.255.255.192
no shutdown
exit

int fa0/1
no switchport
ip address 192.168.31.129 255.255.255.252
no shutdown
exit
```

## RED de Yota
### Capa de Acceso
#### Adif
```
vtp domain g21
vtp password g21
vtp mode client

int range f0/1, fa0/5
switchport mode trunk
exit

int range f0/2-4
switchport mode access
switchport access vlan 30
exit
```

#### Rosneft
```
vtp domain g21
vtp password g21
vtp mode client

int range f0/1, fa0/4
switchport mode trunk
exit

int range f0/2-3
switchport mode access
switchport access vlan 40
exit
```

### Capa de Distribucion
#### Switch6
```
vlan 30
name Adif
vlan 40
name Rosneft
exit

vtp domain g21
vtp password g21
vtp mode server

int range f0/3-5
switchport mode trunk
exit

! Configuracion LACP

int range f0/1-2
channel-group 1 mode active
exit

int po1
switchport mode trunk
exit
```

#### Switch7
```
vlan 30
name Adif
vlan 40
name Rosneft
exit

vtp domain g21
vtp password g21
vtp mode transparent

int range f0/3-5
switchport mode trunk
exit

! Configuracion LACP

int range f0/1-2
channel-group 2 mode active
exit

int po1
switchport mode trunk
exit
```

### Capa de Nucleo
#### MSW3
```
vlan 30
name Adif
vlan 40
name Rosneft
exit

! Configuracion LACP

int range f0/2-3
channel-group 1 mode active
exit

int range f0/4-5
channel-group 2 mode active
exit

int po1
switchport mode trunk
switchport trunk encapsulation dot1q
exit

int po2
switchport mode trunk
switchport trunk encapsulation dot1q
exit

! Interfaz de VLAN

int vlan 30
ip address 192.168.41.1 255.255.255.192
no shutdown
exit

int vlan 40
ip address 192.168.41.65 255.255.255.192
no shutdown
exit

int fa0/1
no switchport
ip address 192.168.41.129 255.255.255.252
no shutdown
exit
```

## RED de Rostelecom
### MSW2
```
vlan 50
name Mercasa
vlan 60
name Navatia
exit

int range f0/2-6
switchport trunk encapsulation dot1q
exit

! Interfaz de VLAN

int vlan 50
ip address 192.168.71.1 255.255.255.192
no shutdown
exit

int vlan 60
ip address 192.168.71.65 255.255.255.192
no shutdown
exit

int fa0/1
no switchport
ip address 192.168.71.129 255.255.255.252
no shutdown
exit
```

### Mercasa1-4
```
vlan 50
name Mercasa
vlan 60
name Navatia
exit

int f0/1
switchport mode trunk
exit

int f0/2
switchport mode access
switchport access vlan 50
exit
```

### Navatia
```
vlan 50
name Mercasa
vlan 60
name Navatia
exit

int f0/1
switchport mode trunk
exit

int f0/2
switchport mode access
switchport access vlan 60
exit
```

## ISP
### Akado
```
int g1/0/3
no switchport
ip address 192.168.31.130 255.255.255.252
no shutdown
exit

int g1/0/2
no switchport
ip address 10.10.10.1 255.255.255.252
no shutdown
exit

int g1/0/1
no switchport
ip address 20.20.20.1 255.255.255.252
no shutdown
exit
```

### Yota
```
int g1/0/3
no switchport
ip address 192.168.41.130 255.255.255.252
no shutdown
exit

int g1/0/1
no switchport
ip address 20.20.20.2 255.255.255.252
no shutdown
exit

int g1/0/2
no switchport
ip address 30.30.30.1 255.255.255.252
no shutdown
exit
```

### Rostelecom
```
int g1/0/3
no switchport
ip address 192.168.71.130 255.255.255.252
no shutdown
exit

int g1/0/1
no switchport
ip address 10.10.10.2 255.255.255.252
no shutdown
exit

int g1/0/2
no switchport
ip address 30.30.30.2 255.255.255.252
no shutdown
exit
```
