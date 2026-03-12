# ***ANSIBLE***

##  Prérequis de l'atelier Ansible 

- Le Controller (Machine A) : Un système sous Ubuntu ou Debian (VM ou CT) où vous allez travailler.
- La Cible (Machine B) : Un serveur sous Ubuntu ou Debian (VM ou CT), accessible par le réseau.
- Accès SSH : Vous devez pouvoir vous connecter en SSH depuis le Controller vers la Cible (avec un utilisateur ayant les droits sudo ou root > `PermitRootLogin Yes` dans `/etc/ssh/sshd_config` de la Cible).

## Étape 1 : Installation et préparation du Controller
L'objectif de cette étape est de mettre en place l'environnement de travail local.

- Mettre à jour les paquets locaux et installer Ansible.
- Créer un répertoire de travail pour garder les fichiers organisés.

### Sur le Controller
```
sudo apt update
sudo apt install ansible -y
```

### Création de l'espace de travail
```
mkdir ~/ansible-lab
cd ~/ansible-lab
```
## Étape 2 : L'inventaire, les prérequis et le "Ping" (La prise de contact)

Ansible a besoin de savoir à quelles machines il doit parler. Au lieu de modifier les fichiers globaux du système, nous allons utiliser les bonnes pratiques en créant un inventaire local. 

De plus, comme nous n'avons pas encore configuré de clés SSH, nous allons utiliser une connexion par mot de passe pour ce premier test.

## Action 1 : Installer l'utilitaire de mot de passe
Pour qu'Ansible puisse injecter automatiquement un mot de passe lors de la connexion SSH (sans que SSH ne le bloque), le paquet sshpass est requis sur le Controller.

### Sur le Controller
`sudo apt install sshpass -y`

## Action 2 : Créer l'inventaire

- Créer un fichier nommé `inventory.ini` dans le dossier `ansible-lab`.
- Y ajouter l'adresse IP du serveur cible et spécifier l'utilisateur de connexion.

`nano /root/ansible-lab/inventory.ini`

```
[serveurs_web]
IP_DE_VOTRE_SERVEUR_CIBLE ansible_user=votre_utilisteur_ssh
```

![alt text](Images/inventory.png)

*Remarque: Ubuntu bloque l'accès SSH direct pour root, il faudra renseigner un utilisateur autorisé sudoers.*


## Le Test (Ping) :
Pour lancer le test, nous ajoutons l'option -k (minuscule) à la commande. Cela indique à Ansible de vous demander le mot de passe SSH de l'utilisateur cible avant de lancer l'action.

`ansible -i inventory.ini serveurs_web -m ping -k`

*(Ansible affichera SSH password:, tapez le mot de passe de votre utilisateur cible).*

![alt text](Images/Ping.png)


# Étape 3 : Playbook 1 - Mise à jour de l'OS
C'est l'heure du premier Playbook (fichier YAML). L'objectif est de s'assurer que le serveur cible est à jour.

- Créer un fichier 1-update-os.yml et y insérer le code suivant. Observez l'indentation, elle est stricte en YAML !

`nano 1-update-os.yml`

```
---
- name: Udpate OS
  hosts: all
#  become: yes # Permet d'executer les commandes avec sudo pour Ubuntu

  tasks:
    - name: Mettre a jour le cache APT et faire un upgrade
      apt:
        update_cache: yes
        upgrade: dist
```
## Executer votre 1er Playbook

`ansible-playbook -i inventory.ini 1-update-os.yml -k`

![alt text](Images/test_playbook.png)