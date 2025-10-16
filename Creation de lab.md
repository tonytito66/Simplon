# Creation du Lab

## Sommaire

- [Introduction](#introduction)
- [Schéma réseau](#schéma-réseau)
- [Listes des comptes a risques](#listes-des-comptes-a-risques)
- [Verification du hash](#verification-du-hash)
- [Mises à jour réussies](#mises-à-jour-réussies)
- [Mises en place de WinRM, Samba, Web-Linux](#mises-en-place-de-winrm-samba-web-linux)
- [Statut des Services](#statut-des-services)
- [Connexions SSH et WinRM](#connexions-ssh-et-winrm)

## **Introduction**
- A Marquer


## **Schéma réseau**

```mermaid
flowchart TD
    A[Hyperviseur] -->|hosts| W(Windows Server)
    A --> | hosts| C(Windows Client)
    A --> | hosts| L(Linux Server)

    W --> |running| Z{AD DC}
    W --> |running| E{DNS}
    W --> |running| F{WinRM}
    W --> |running| R{RDP}
    W --> |running| G{SMB} 
    W --> |executed| J>BadBlood] 

    L --> |running| H{WEB VLA}
    L --> |running| I{SSH}

    C --> |joined| Z
```

## **Listes des comptes a risques**

- ***Comptes et Groupes Privilégiés ou Critiques – Windows Server, Windows 10 et Linux***

| Plateforme            | Nom du compte/groupe                     | Type                          | Description                                                                                     | Niveau de risque | Risque spécifique / Exemple d’exploitation |
|-----------------------|------------------------------------------|-------------------------------|-------------------------------------------------------------------------------------------------|------------------|-------------------------------------------|
| **Windows Server (AD)** | **Administrateur** | Utilisateur | Compte d’administration local. | Extrême | Accès total au système local. |
| **Windows Server (AD)** | **Administrateurs** | Groupe de sécurité - Global | Contrôle total sur le domaine. | Extrême | Accès complet à toutes les ressources AD. |
| **Windows Server (AD)** | **Administrateurs clés Enterprise** | Groupe de sécurité - Universel | Administration critique dans toute la forêt. | Extrême | Compromission = contrôle complet de la forêt. |
| **Windows Server (AD)** | **Administrateurs de l’entreprise** | Groupe de sécurité - Universel | Contrôle total de la forêt AD. | Extrême | Peut déléguer les droits sur tous les domaines. |
| **Windows Server (AD)** | **Administrateurs du schéma** | Groupe de sécurité - Universel | Peut modifier le schéma AD. | Extrême | Modification du schéma = impact global irréversible. |
| **Windows Server (AD)** | **Admins du domaine / Domain Admins** | Groupe de sécurité - Global | Contrôle total du domaine. | Extrême | Peut élever tout compte au niveau admin. |
| **Windows Server (AD)** | **DnsAdmins** | Groupe de sécurité - Domaine local | Peut exécuter du code arbitraire en tant que SYSTEM sur le serveur DNS. | Extrême | Exploitation classique via DLL malveillante. |
| **Windows Server (AD)** | **Contrôleurs de domaine** | Groupe de sécurité - Global | Tous les DC du domaine. | Extrême | Contrôle complet sur l’annuaire AD. |
| **Windows Server (AD)** | **krbtgt** | Compte de service AD | Utilisé pour le chiffrement Kerberos. | Extrême | Attaque Golden Ticket (forgery de tickets). |
| **Windows Server (AD)** | **Group Policy Creator Owners** | Groupe de sécurité - Domaine local | Peut créer et modifier des GPO. | Élevé | GPO malveillante = exécution à distance. |
| **Windows Server (AD)** | **Backup Operators** | Groupe de sécurité - Domaine local | Peut sauvegarder et restaurer des fichiers. | Élevé | Accès indirect à des données sensibles. |
| **Windows Server (AD)** | **Account Operators** | Groupe de sécurité - Domaine local | Peut créer/modifier des comptes utilisateurs. | Élevé | Création de comptes administrateurs cachés. |
| **Windows Server (AD)** | **Server Operators** | Groupe de sécurité - Domaine local | Peut gérer les services et ressources du serveur. | Élevé | Arrêt, redémarrage, gestion de services sensibles. |
| **Windows Server (AD)** | **Hyper-V Admins** | Groupe de sécurité - Domaine local | Contrôle les machines virtuelles. | Élevé | Accès au disque virtuel = vol de credentials. |
| **Windows Server (AD)** | **Remote Management Users** | Groupe local | Peut exécuter des commandes à distance (PowerShell Remoting). | Élevé | Exécution de code via WinRM. |
| **Windows Server (AD)** | **RDP Users** | Groupe local | Peut se connecter à distance via RDP. | Moyen/Élevé | Accès distant si MFA absent. |
| **Windows Server (AD)** | **Replicator** | Groupe de sécurité - Domaine local | Utilisé pour la réplication de fichiers. | Élevé | Peut exfiltrer des données sensibles. |
| **Windows Server (AD)** | **SYSTEM** | Compte système | Compte système interne Windows. | Extrême | Exécution avec tous les privilèges. |
| **Windows Server (AD)** | **TrustedInstaller** | Compte système | Gère les installations Windows. | Très élevé | Peut modifier des fichiers système. |
| **Windows Server (AD)** | **Network Service** | Compte système | Service réseau avec privilèges limités. | Élevé | Escalade possible via services vulnérables. |
| **Windows Server (AD)** | **Local Service** | Compte système | Service local à permissions restreintes. | Moyen | Risque limité, mais exploitable localement. |
| **Windows 10** | **Administrateur local** | Utilisateur | Accès complet à la machine. | Extrême | Peut désactiver sécurité et exécuter code arbitraire. |
| **Windows 10** | **SYSTEM / TrustedInstaller** | Compte système | Contrôle total du système. | Extrême | Manipulation directe de fichiers système. |
| **Windows 10** | **Remote Desktop Users** | Groupe local | Accès RDP distant. | Élevé | Tentatives de brute-force RDP. |
| **Windows 10** | **Remote Management Users** | Groupe local | Exécution à distance via PowerShell. | Élevé | Exécution de commandes sans MFA. |
| **Windows 10** | **Power Users** | Groupe local | Droits élevés hérités des anciennes versions. | Moyen/Élevé | Peut exécuter ou installer des logiciels. |
| **Windows 10** | **Users (Builtin)** | Groupe local | Groupe de base des comptes locaux. | Moyen | Mauvaise configuration = élévation potentielle. |
| **Linux** | **root** | Utilisateur | Superutilisateur avec accès complet. | Extrême | Contrôle total du système. |
| **Linux** | **sudo** | Groupe | Peut exécuter des commandes en tant que root. | Très élevé | Mauvaise config sudoers = accès root. |
| **Linux** | **wheel** | Groupe | Peut utiliser `sudo` (selon la distro). | Très élevé | Membre = élévation directe. |
| **Linux** | **adm** | Groupe | Peut lire les logs système. | Moyen | Accès à journaux sensibles. |
| **Linux** | **shadow** | Groupe | Accès à `/etc/shadow`. | Extrême | Lecture des mots de passe hachés. |
| **Linux** | **operator** | Groupe | Peut effectuer certaines opérations système. | Élevé | Exécution de commandes critiques. |
| **Linux** | **staff** | Groupe | Peut installer des logiciels localement. | Élevé | Installation de binaires malveillants. |
| **Linux** | **docker** | Groupe | Contrôle indirect de root via conteneur privilégié. | Extrême | Accès root via `--privileged` ou volumes. |
| **Linux** | **lxd / libvirt / kvm** | Groupes | Accès à la virtualisation. | Élevé/Extrême | Accès à l’hôte via VM. |
| **Linux** | **systemd-journal** | Groupe | Peut lire journaux du système. | Moyen | Accès à des infos sensibles. |
| **Linux** | **bin, daemon, sys, sync, games, lp, mail** | Comptes système | Comptes système historiques. | Moyen | Risques faibles mais existants. |
| **Linux** | **nobody / nogroup** | Utilisateur/Groupe | Utilisé pour processus anonymes. | Moyen | Peut être détourné pour exécution anonyme. |
| **Linux** | **Comptes avec UID 0** | Utilisateur | Tout compte avec UID 0 = root. | Extrême | Contournement total des restrictions. |
| **Linux** | **Comptes de service (www-data, mysql, postfix, etc.)** | Utilisateur | Comptes utilisés par des services. | Moyen/Élevé | Vulnérables selon leur rôle et permissions. |


## **Verification du hash**

- Via la cmd Powershell
- $hash = Get-FileHash C:\Chemin\vers\ton\fichier.iso,
- puis en faisant
- $hash.Hash eq 'hash/trouver/sur/le/sie/fabricant/'     ,pour comparer si les 2 hash sont totalement identique.
  
<img width="1295" height="321" alt="image" src="https://github.com/user-attachments/assets/18c2cef3-e010-443e-b396-419c6d9b40d2" />

<img width="1412" height="163" alt="image" src="https://github.com/user-attachments/assets/04711f8b-1491-4c0f-9964-256c819bbc05" />

#### ***Sha256 de l'ISO "Debian-12.7.0-amd64-netinst.iso***
<img width="736" height="54" alt="image" src="https://github.com/user-attachments/assets/d2a82a77-a182-4342-9608-1308f7acf410" />
 
 #### ***Sha256 de l'ISO "Win10_22H2_French_x64v1.iso"***

<img width="1270" height="412" alt="image" src="https://github.com/user-attachments/assets/67594484-273a-46fc-8dc0-6b1cf6a02e2e" />

#### ***Sha256 de l'ISO "fr-fr_windows_server_2022_x64_dvd_9f7d1adb.iso"***
<img width="1274" height="356" alt="image" src="https://github.com/user-attachments/assets/3408dc27-7620-4586-9424-1f54c2927517" />

## **Mises à jour réussies**

- ***Debian12***

<img width="835" height="282" alt="image" src="https://github.com/user-attachments/assets/2573dfa6-a2a9-4433-b0fc-35afe06a4228" />

- ***WinServ2022***

<img width="1059" height="845" alt="image" src="https://github.com/user-attachments/assets/6ae090a1-c55c-4bfb-bbed-2044c2db1502" />

- ***Win10Client***

<img width="591" height="632" alt="image" src="https://github.com/user-attachments/assets/8fd16054-f80d-4839-aca1-838b30fdfa1f" />


## ***Statut des Services***

- **DNS**

<img width="334" height="393" alt="image" src="https://github.com/user-attachments/assets/d33fde75-517e-4f7c-82a9-5b683247704c" />


- **WEB**
  




## ***Connexions SSH et WinRM***

- ***SSH***

**Serv-->Client**

<img width="290" height="67" alt="image" src="https://github.com/user-attachments/assets/e05caae5-386c-4de4-9b5c-8551e0dc82c5" />


**Client-->Serv**

<img width="439" height="384" alt="image" src="https://github.com/user-attachments/assets/eae489bf-3837-4673-adf3-4a65d72a0285" />

- ***WINRM***

**Client-->Serv**

<img width="484" height="624" alt="image" src="https://github.com/user-attachments/assets/f6885570-1483-4170-ac57-1a3f6353bbcc" />,<img width="830" height="446" alt="image" src="https://github.com/user-attachments/assets/977bec78-a24c-4249-93b8-1443c0b343a0" />

**Serv-->Client**

<img width="858" height="420" alt="image" src="https://github.com/user-attachments/assets/1e697d80-54e0-49b1-a148-85b551e1b72e" />, <img width="630" height="95" alt="image" src="https://github.com/user-attachments/assets/a6fe8451-4973-4686-91b9-02f6e177588a" />


## ***Mises en place de WinRM, Samba, Web-Linux***

- ***WinRM***

<img width="631" height="197" alt="image" src="https://github.com/user-attachments/assets/3b997256-838f-463d-bcac-440e41a49568" />

- ***Partage SMB***

**Read Only**

<img width="483" height="598" alt="image" src="https://github.com/user-attachments/assets/e36dcd07-4f00-4a0b-a40d-746d9e65497b" />, <img width="484" height="600" alt="image" src="https://github.com/user-attachments/assets/553b23fa-571f-49a9-bfe9-1a1bad9df944" />

 **Write**
 
<img width="482" height="603" alt="image" src="https://github.com/user-attachments/assets/387341c4-1508-4ab9-af45-9cef86820245" />,<img width="483" height="600" alt="image" src="https://github.com/user-attachments/assets/2db054b2-4db9-4347-9278-da3207290a1c" />


- ***Web-Linux***
  
<img width="812" height="398" alt="image" src="https://github.com/user-attachments/assets/ad6ea16c-13ee-4052-a1dd-adf9028f7a1d" />

<img width="2506" height="461" alt="image" src="https://github.com/user-attachments/assets/31b29834-22ae-4ff7-ad8f-ea171a5d12c9" />
