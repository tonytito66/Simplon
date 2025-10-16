# Creation du Lab

## Sommaire

- [Introduction](#introduction)
- [Schéma réseau](#schéma-réseau)
- [Listes des comptes](#listes-des-comptes)
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

## **Listes des comptes**

| Utilisateurs   | Emplacement |Systeme  |
|-------------|------------|------|
| Admin    |Local        |WinServ    |
| Anthoad  |Local          |WinServ    |



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

![alt text](image-7.png)

## ***Statut des Services***

- **DNS**

![alt text](image-6.png)

- **WEB**


## ***Connexions SSH et WinRM***

- ***SSH***

**Serv-->Client**

![alt text](image-8.png)

**Client-->Serv**

![alt text](image-9.png)


- ***WINRM***

**Client-->Serv**

![alt text](image-10.png),![alt text](image-13.png)

**Serv-->Client**

![alt text](image-11.png),![alt text](image-12.png)

## ***Mises en place de WinRM, Samba, Web-Linux***

- ***WinRM***

![alt text](image-1.png)

- ***Partage SMB***

**Read Only**

![alt text](image-2.png), ![alt text](image-3.png)

 **Write**

![alt text](image-4.png), ![alt text](image-5.png)


- ***Web-Linux***

![alt text](image-14.png)

![alt text](image-15.png)

