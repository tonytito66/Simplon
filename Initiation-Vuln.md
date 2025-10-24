# Initiation-Vuln

## Objectif

***Évaluer les vulnérabilités ci-dessous***

- Eternal Blue
- Krack
- Log4shell
- Looney-tunables
- Une vulnérabilité récente de votre choix issue du site du CERT-Fr


***Pour chacune des vulnérabilités***

* Donnez la référence CVE

* Décrire la vulnérabilité en une phrase

* Citez des éléments d'infrastructure pouvant être concernés

* Trouvez, mettez à jour ou calculez le score base CVSS (dernière version)

* Déterminer si un exploit est disponible publiquement, si oui en prendre connaissance et le citer en référence.

* Trouver si un score EPSS existe pour cette vuln



## Sommaire

- [Eternal Blue](*eternal-blue)

- [Krack](*krack)

- [Log4shell](*log4shell)

- [Looney-tunables](*looney-tunables)

- [Netgear](*netgear)


## Eternal Blue

- ***CVE***

CVE-2017-0144

- ***Decrire la Vuln***

EternalBlue exploite les vulnérabilités du protocole SMBv1 pour insérer des paquets de données malveillants et diffuser des malwares sur le réseau.

- ***Elements Infra concernés***

Microsoft Windows Vista SP2; Windows Server 2008 SP2 and R2 SP1; Windows 7 SP1; Windows 8.1; Windows Server 2012 Gold and R2; Windows RT 8.1; and Windows 10 Gold, 1511, and 1607; and Windows Server 2016

- ***CVSS***

CVSS 8.8 High

- ***Exploit***

Microsoft Windows 7/8.1/2008 R2/2012 R2/2016 R2 - 'EternalBlue' SMB Remote Code Execution (MS17-010)
Microsoft Windows 7/2008 R2 - 'EternalBlue' SMB Remote Code Execution (MS17-010)
Microsoft Windows 8/8.1/2012 R2 (x64) - 'EternalBlue' SMB Remote Code Execution (MS17-010)

- ***EPSS***

94.32%

## Krack

- ***CVE***

CVE-2017-13077
CVE-2017-13078
CVE-2017-13079
CVE-2017-13080
CVE-2017-13081
CVE-2017-13082
CVE-2017-13084
CVE-2017-13086
CVE-2017-13087
CVE-2017-13088

- ***Decrire la Vuln***

Pour le CVE-2017-13088 : L'accès protégé Wi-Fi (WPA et WPA2) prenant en charge 802.11v permet la réinstallation de la clé temporelle du groupe d'intégrité.
Mais les autres se sont aussi des problemes de Wifi

- ***Elements Infra concernés***

Microsoft Windows, macOS, iOS, Android, Linux, OpenBSD

- ***CVSS***

CVSS 5.3 Medium

- ***Exploit***



- ***EPSS***

0.20%

## Log4shell 

- ***CVE***

CVE-2021-44228

- ***Decrire la Vuln***

une vulnérabilité zero-day exploitée par exécution de code arbitraire et touchant l'utilitaire Java Log4j qui ne vérifie pas les requêtes LDAP et JNDI.

- ***Elements Infra concernés***

Apache Log4j2

- ***CVSS***

CVSS 10 Critical

- ***Exploit***

AD Manager Plus 7122 - Remote Code Execution (RCE)
Apache Log4j 2 - Remote Code Execution (RCE)
Apache Log4j2 2.14.1 - Information Disclosure

- ***EPSS***

94.36%


## Looney-tunables

- ***CVE***

CVE-2023-4911

- ***Decrire la Vuln***

Buffer overflow qui en utilisant des varaibles d'environnement permet d'executer du code avec des privilèges élevés.


- ***Elements Infra concernés***

linux,debian,ubuntu,redhat,fedora,GNU » Glibc

- ***CVSS***

7.8	High

- ***Exploit***

https://github.com/hadrian3689/looney-tunables-CVE-2023-4911
https://www.rapid7.com/db/modules/exploit/linux/local/glibc_tunables_priv_esc/

- ***EPSS***

78.36% 

## Netgear

- ***CVE***

CVE-2017-6862

- ***Decrire la Vuln***

Via un Buffer overflow il autorise le contournement de l'authentification et l'execution de code a distance , en utilisant un parametre de la Webapp.

- ***Elements Infra concernés***

Routeur NETGEAR WNR2000v3 avant la V 1.1.2.14
Routeur NETGEAR WNR2000v4 avant la V 1.0.0.66
Routeur NETGEAR WNR2000v5 avant la V 1.0.0.42

- ***CVSS***
 
 9.8 Critical

- ***Exploit***

-None

- ***EPSS***

49.86%


