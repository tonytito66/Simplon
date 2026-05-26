# Déployer une surveillance de sécurité avec Wazuh et détecter des incidents

## Objectif

 L’entreprise Let'sInnov poursuit la modernisation et la sécurisation de son infrastructure informatique. Après plusieurs alertes de sécurité liées à des connexions suspectes, des tentatives de brute force et des comportements anormaux observés sur certains serveurs, la direction souhaite améliorer ses capacités de supervision et de détection des incidents.

En tant qu’administrateur d’infrastructures sécurisées au sein de l’équipe SOC interne, vous êtes chargé de mettre en œuvre une solution centralisée de supervision de sécurité reposant sur un SIEM open-source. L’objectif est de collecter et corréler les journaux issus des équipements réseau, des serveurs Linux et Windows ainsi que des postes utilisateurs afin de détecter rapidement des comportements suspects.

Vous devrez installer et configurer Wazuh dans un environnement virtualisé, intégrer différentes sources de logs et mettre en œuvre plusieurs cas d’usage de détection. Vous serez également amené à déployer un IDS réseau, configurer des règles de surveillance et analyser les alertes générées lors de simulations d’attaques.

L’infrastructure devra permettre :

la collecte centralisée des journaux
la supervision des événements de sécurité
la détection d’activités malveillantes
l’analyse des alertes
la documentation des incidents détectés
l’amélioration continue des règles de détection
L’ensemble des opérations devra respecter les bonnes pratiques de cybersécurité et être documenté afin de permettre une exploitation par l’équipe informatique.


### Mission 1 : Installation et Configuration de Wazuh - Installer Wazuh dans un environnement simulé et configurer la collecte de logs

### Installation OS 

- J'ai installé **Ubuntu 24.04** avec GUI qui fait partie des OS recommandés avec une carte en bridge.  

- Je mets à jour la liste des paquets et je mets à jour ensuite le système

`sudo apt update && sudo apt upgrade -y`  

### Installation Wazuh

Installation de Wazuh avec curl (après instll de curl)  
`curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a`  

- A la fin de l'installation le username et un password fort sont générés automatiquement.  



- Je peux ensuite me connecter avec l'interface Web : **`127.0.0.1`** et me connecter 



- Les user/password sont stockés dans un ficher compressé accessible avec : `sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt`  

- Désactivation des mises à jour de Wazuh pour éviter les mises à jour accidentelles susceptibles de perturber l'environnement :  

`sudo sed -i "s/^deb /#deb /" /etc/apt/sources.list.d/wazuh.list`  
`sudo apt update`  
