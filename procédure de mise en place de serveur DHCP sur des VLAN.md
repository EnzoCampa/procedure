# procédure de mise en place de serveur DHCP sur des VLAN

## étape 1 : création des VLAN
*créer les vlan 3170 et 102*

```bash=
/interface vlan add interface=@int name=@name vlan-id=@id
```
### ex :
```bash=
interface vlan add interface=br-lan vlan-id=102 name=vlan_102
```

## étape 2 : IP sur Vlan
*mettre une IP sur les VLAN*

```bash=
ip address add interface=@int_vlan address=@ip_vlan
```

### ex :
```bash=
ip address add interface=vlan_102 address=160.0.0.1/8
```
## étape 3 : pool dIP
*créer les pool d'adresse IP pour les vlan*

```bash=
ip pool add name=pool_name ranges=@IP_start-@IP_end
```
### ex :
```bash=
ip pool add name=pool_vlan_102 ranges=160.0.0.2-160.0.0.254
```

## étape 4 : serveur DHCP
*création des deux serveurs DHCP ayant une plage d'adresse différente*

```bash=
/ip dhcp-server add address-pool=@pool_name interface=@vlan_name
```
### ex :
```bash=
ip dhcp-server add address-pool=pool_vlan_102 interface=vlan_102 
```
## étape 5 :déclaration réseau

*déclarer *

```bash=
ip dhcp-server network add address=@ip_vlan/8 dns-server=8.8.8.8,8.8.4.4 gateway=@ip_gateway
```
### ex :
```bash=
ip dhcp-server network add  address=160.0.0.0/8 dns-server=8.8.8.8,8.8.4.4 gateway=160.0.0.1 
```
## étape 6 : activation

*activation du dhcp*

```bash=
 ip dhcp-server enable @num
```

### ex :
```bash=
ip dhcp-server enable 2
```
