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


## Mission 1 : Installation et Configuration de Wazuh - Installer Wazuh dans un environnement simulé et configurer la collecte de logs

### Installation OS 

- J'ai installé **Ubuntu 24.04** avec GUI qui fait partie des OS recommandés avec une carte en bridge.  

- Je mets à jour la liste des paquets et je mets à jour ensuite le système

`sudo apt update && sudo apt upgrade -y`  

### Installation Wazuh

Installation de Wazuh avec curl (après instll de curl)  
`curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a`  

- A la fin de l'installation le username et un password fort sont générés automatiquement.  



- Je peux ensuite me connecter avec l'interface Web : **`Mon_ip`** et me connecter 

![alt text](Images/Wazuh/connexion_wazuh.png)

- Les user/password sont stockés dans un ficher compressé accessible avec : `sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt`  

- Désactivation des mises à jour de Wazuh pour éviter les mises à jour accidentelles susceptibles de perturber l'environnement :  

`sudo sed -i "s/^deb /#deb /" /etc/apt/sources.list.d/wazuh.list`  
`sudo apt update`  


## Mission 2 : Explorer les capacités de Wazuh à travers les différents uses cases proposés dans sa documentation officielle (à travers la réalisation de use-cases pratiques)

### 1 - Intégration de l'IDS Suricata : https://documentation.wazuh.com/current/proof-of-concept-guide/integrate-network-ids-suricata.html

#### Installation NIDS Suricata

- J'ai décidé d'installer l'agent Suricata sur une VM cliente Debian 12.

```bash
# 1. Configurer les dépôts officiels Debian 12 + backports
cat > /etc/apt/sources.list <<'EOF'
deb http://deb.debian.org/debian bookworm main
deb http://deb.debian.org/debian-security bookworm-security main
deb http://deb.debian.org/debian bookworm-updates main
deb http://deb.debian.org/debian bookworm-backports main
EOF

# 2. Mettre à jour les dépôts
sudo apt update

# 3. Installer Suricata depuis les backports Debian
sudo apt install -t bookworm-backports -y suricata

# 4. Vérifier l'installation
suricata --build-info

# 5. Activer et démarrer le service
sudo systemctl enable --now suricata

# 6. Vérifier l'état du service
sudo systemctl status suricata
```
- Télécharger et extraire le jeu de règles Emerging Threats Suricata 

```bash
cd /tmp/ && curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz
sudo tar -xvzf emerging.rules.tar.gz && sudo mkdir /etc/suricata/rules && sudo mv rules/*.rules /etc/>suricata/rules/
sudo find /etc/suricata/rules -name "*.rules" -exec chmod 777 {} \;
```
- Modifier le fichier .yml dans /etc/suricata/suricata.yaml

```bash
HOME_NET: "<UBUNTU_IP>"
EXTERNAL_NET: "any"

default-rule-path: /etc/suricata/rules
rule-files:
- "*.rules"

# Global stats configuration
stats:
enabled: yes

# Linux high speed capture support
af-packet:
  - interface: "selon l'interface"
  ```

  Puis

  ```sudo systemctl restart suricata```

  #### Installation AGENT Wazuh sur Linux (Debian 12)

  ```bash
  # 1. Installer le paquets i il est manquant
  apt-get install gnupg apt-transport-https

  # 2. Insataller la clé GPG
  curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg

  ![alt text](Images/Wazuh/cléGpg.png)

  # 3.Ajouter au Repo
  echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
  
  # 4. Update le paquet
  apt-get update
  ```
  #### Deployer AGENT Wazuh sur Linux (Debian 12)

  ```bash
  WAZUH_MANAGER="IP_Serveur_Wazuh" apt-get install wazuh-agent
  ```
![alt text](Images/Wazuh/wazuh_agent.png)
 
 - Redemarrer les Services

 ```bash
systemctl daemon-reload
systemctl enable wazuh-agent
systemctl start wazuh-agent
```

#### Ajouter la config dans /var/ossec/etc/ossec.conf il permet a l'agent de lire les logs de suricata

```bash
<ossec_config>
  <localfile>
    <log_format>json</log_format>
    <location>/var/log/suricata/eve.json</location>
  </localfile>
</ossec_config>
```
Puis

```
sudo systemctl restart wazuh-agent
```

#### Test D'attaque 

Depuis la machine Wazuh serveur faire un 

```bash
ping -c 20 "IP_agent"
```
Puis aller sur L'interface GUI de Wazuh dans Threat intelligence ->Treat Hunting -> et en haut a gauche Events
Dans la barre search mettre " rule.groups:suricata"

![alt text](Images/Wazuh/wazuh_threat.png)

![alt text](<Images/Wazuh/wazuh icmp.png>)

### 2 - Surveillance de l'intégrité de répertoires/fichiers sensibles : https://documentation.wazuh.com/current/proof-of-concept-guide/poc-file-integrity-monitoring.html

- Ajouter cette ligne dans /var/ossec/etc/ossec.conf , Dans le block syscheck 

```bash
<directories check_all="yes" report_changes="yes" realtime="yes">/root</directories>
```
Puis 

```
sudo systemctl restart wazuh-agent

```
![alt text](Images/Wazuh/syscheck.png)

Creer un fichier a la racine ou dans le documents choisi auparavent puis ecrire dessus et le supprimer, ensuite aller verifier dans Wazuh .

![alt text](Images/Wazuh/integrité.png)
