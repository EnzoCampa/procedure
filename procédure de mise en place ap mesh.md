# procédure de mise en place ap mesh


## étape 1 : étiquetage
*donner un nom a l'ap pour la repérer*
- donner un nom du style XX:YY:AP 1 ou XX et YY son les 4 deniers octets de l'addresse mac

## étape 2 : DHCP option
*vérification et mise en place du dhcp option*

- il faut convertir l'addresse IP du site unifi sur ce site : https://www.browserling.com/tools/ip-to-hex 

- vérifier si il existe dans le routeur

```bash=
ip dhcp-server option print 
```

| #   | NAME  | code | value          | raw-value    |
| --- | ----- | ---- | -------------- | ------------ |
| 0   | unifi | 43   | 0x0104d48120f5 | 0104d48120f5 |

- si il n'esxiste pas il faut le créer

```bash=
ip dhcp-server option add name=@name code=43 value=@ip_hexa
```
```bash=
ip dhcp-server optionadd name=unifi_set options=unifi
```

## étape 3 : Branchement 

*Brancher un AP sur le routeur.*

- Vérifier que le port soit sur le même VLAN que que le port “INTERNET”.

- si le vlan n'est pas en place, suivre ce lien : https://codimd.ruffat.org/s/rFyN9ErkW

## étape 4 : Site UNIFI
*Se rendre sur le site internet "https://unifi3.iwibox.net:8443/manage”.*

## étape 5 : SITE
*Se déplacer dans le SITE que l’on souhaite.*

<div  style="text-align: center">
    
![](https://imgur.com/ByHhQ5o.png)

</div>

## étape 6 : Adoption de l'AP
*Adopter l'AP dans le site voulu.*

<div  style="text-align: center">
    

![](https://imgur.com/IUs4uR0.png)

</div>
    
- cliquer sur l'AP nous emmenera sur la page permettant l'adoption
    
<div  style="text-align: center">
    
![](https://imgur.com/nbWVzN9.png)
    
</div>

## étape 7 : Configuration
*Attendre que la configuration se fasse*
## étape 8 : Changer IP et nom
*Changer l'adresse IP et le nom pour finaliser la procédure*

++nom :++



Dans le même onglet, cliquer sur "général" et changer l'alias

<div  style="text-align: center">
    
![](https://imgur.com/QINlSoW.png)
    
</div>

++adresse ip :++


Dans le même onglet, cliquer sur "réseau" et choisir IP fixe

<div  style="text-align: center">
    
![](https://imgur.com/94g37zG.png)

![](https://imgur.com/7yEYolh.png)

![](https://imgur.com/ppHclrc.png)

</div>

## étape facultative : Gratuit

*Si besoin de mettre l’accès en gratuit il faut se rendre dans le ”wlans”*

<div  style="text-align: center">

![](https://imgur.com/Q2A2W6k.png)

</div>






Ancienne procédure avant l'automatisation de ces 3 étapes
```bash=
## étape 2 : Recherche d'IP
Se connecter sur le routeur pour trouver l ip.


/ip dhcp-server lease print 

## étape 3 : Connection 

Se connecter en SSH sur l’AP. Avec la commande de style ”ssh users@IP”.*


ssh ubnt@192.168.16.43

## étape 4 : Adoption request
*Taper la commande de style ”Set-inform “http:@ip:8080/inform”.*


UBNT-BZ.v3.9.54# set-inform http://unifi3.iwibox.net:8080/inform

Adoption request sent to 'http://unifi3.iwibox.net:8080/inform'.  Use the controller to complete the adopt process.

```