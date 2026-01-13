# Objectifs
Le but de cet exercice est d’effectuer une analyse de type « reverse engineering » à partir d’une infrastructure fonctionnelle, sur le thème de HSRP.

* Analyse de l’infrastructure

### Qu’est-ce que HSRP ? Proposer une définition simple.

HSRP est un protocole Cisco qui permet à plusieurs routeurs de fonctionner ensemble dans un groupe,
fournissant une adresse IP virtuelle (l'adresse de passerelle par défaut) qui est partagée entre eux.

### Pourquoi utilise-t-on HSRP et quel problème résout-il ? Expliquer l'intérêt de HSRP dans ce réseau

Cette technologie offre une passerelle par défaut virtuelle stable, assurant une transition transparente
entre les routeurs actif et de secours en cas de besoin. 

L'intérêt de HSRP dans ce réseau est d'avoir de la redondance

* Analyse de la configuration existante

### Identifier les routeurs primaires et les routeurs de secours HSRP, quels sont leurs rôles respectifs ?

![R1](Images/HSRP1.png)

R1 est le routeur principal celui qui fonctionne en premier
R2 et R3 sont en ecoute si R1 coupe alors l'un des 2 prendra le relais pour assurer la continuité de services.

### Noter les adresses IP virtuelles (VIP) et physiques (R1, R2, R3) utilisées dans les groupes HSRP, à quoi servent ces différentes adresses ?

* IP virtuelle 

Les adresses IP virtuelles sont utilisées comme passerelles par défaut par les hôtes du réseau.
Elles représentent une passerelle logique unique, indépendamment du routeur réellement actif.
En cas de panne du routeur actif, la VIP est automatiquement reprise par un autre routeur sans impact pour les utilisateurs.

Groupe 1 :172.30.128.254

Groupe 2 :92.60.150.1

* Ip Physiques

Adresses réelles des interfaces des routeurs

Elles servent a la communication entre routeurs,l’élection HSRP (actif / standby),l’administration et la supervision.

Elles ne sont jamais configurées comme passerelle sur les postes clients

R1 : Gig 0/0/1 92.60.150.2/24 ; Gig 0/0/0/ 172.30.128.251/24

R2: Gig 0/0/1 92.60.150.3/24 ; Gig 0/0/0/ 172.30.128.252/24

R3: Gig 0/0/1 92.60.150.4/24 ; Gig 0/0/0/ 172.30.128.253/24


### Identifier les interfaces réseau participant à HSRP sur chaque routeur, leurs priorités, les délais et les autres paramètres HSRP configurés sur les routeurs. Que comprenez-vous ?
  
  - Gig 0/0/1 et Gig 0/0/0/

* Groupe 1 (Gig0/0/0) :

R1 possède une priorité de 120

R2 et R3 ont une priorité de 100

➜ R1 est routeur actif

➜ R3 est routeur de secours

* Groupe 2 (Gig0/0/1) :

R3 est routeur actif

R2 est routeur standby

R1 est en état Listen

Priorités égales (100), l’élection s’est faite automatiquement


* Les Delais 

Hello time : 3 secondes

Hold time : 10 secondes

* Les autres paramètres

- Préemption activée

Permet à un routeur avec une priorité plus élevée de reprendre son rôle actif après un redémarrage

- Adresse MAC virtuelle

Associe la VIP à une MAC HSRP spécifique pour assurer la continuité du trafic

* Cette configuration permet :

Une haute disponibilité de la passerelle réseau

Un basculement automatique en cas de panne

Une répartition des rôles entre les routeurs

Aucune modification nécessaire sur les postes clients

### À l'aide des informations que vous avez collectées, proposer un guide de commandes de configuration HSRP. Expliquer brièvement le rôle de chaque commande utilisée. Identifier les éléments clés tels que le numéro de groupe HSRP, les adresses IP virtuelles, les priorités, les délais, ainsi que les commandes permettant d'activer HSRP sur l'interface

* Configuration sur R1 – Groupe 1 (Gig0/0/0)

```
 interface GigabitEthernet0/0/0
 ip address 172.30.128.251 255.255.255.0
 standby 1 ip 172.30.128.254
 standby 1 priority 120
 standby 1 preempt
 standby 1 timers 3 10
 ```


* Configuration sur R2 (GigabitEthernet0/0/1)

```
interface GigabitEthernet0/0/1
 ip address 92.60.150.3 255.255.255.0
 standby 2 ip 92.60.150.1
 standby 2 priority 110
 standby 2 preempt
 standby 2 timers 3 10
 ```

* Configuration sur R3 – Groupe 2 (Gig0/0/1)

```
interface GigabitEthernet0/0/1
 ip address 92.60.150.4 255.255.255.0
 standby 2 ip 92.60.150.1
 standby 2 priority 120
 standby 2 preempt
 standby 2 timers 3 10
```

* Explication des commandes :

standby 1 : numéro du groupe HSRP

ip 172.30.128.254 : adresse IP virtuelle

priority 120 : définit le routeur actif

preempt : permet la reprise du rôle actif

timers : définit les délais HSRP