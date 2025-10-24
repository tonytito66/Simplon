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

1 - [Eternal Blue](*eternal-blue)

2 - [Krack](*krack)

3 - [Log4shell](*log4shell)

4 - [Looney-tunables](*looney-tunables)

5 -


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