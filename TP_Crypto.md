# TP1 Cyber Chef

## Partie 1 : Chiffrement de César

Dans « CyberChef » utilisez la recette « ROT13 »

1. Avec une « Box Height » de 13, chiffrer la phrase suivante : RENDEZ-VOUS À MIDI

- Quel est le texte chiffré ?

  - ERAQRM-IBHF À ZVQV

- Déchiffrez ce texte pour vérifier le résultat

![alt text](Images/Crypto_cyberchef/ROT13.png)


2. Chiffrer le nom de votre film préféré avec une « Box Height » de votre choix

- Transmettre le texte chiffré à votre binôme sans lui communiquer la clé

  - P jiol Pyhxynnu

- Au sein de votre binôme, essayer de retrouver le message en sens inverse 

### **Nicolas**

![alt text](Images/Crypto_cyberchef/Rot25_Nico.png)

## Partie 2 : Vigenère

Dans « CyberChef » utilisez la recette « Vigenère Encode »

1. Encodez le nom de votre plat préféré avec la clé 'KEY'
- Quel est le texte chiffré ?

  - s'eagm dyf tkkdj

- Transmettre le texte chiffré à votre binôme

- Transmettre la clé à votre binôme par un autre canal
  
  - jesuisunecle

- Au sein de votre binôme, déchiffrez le message pour découvrir vos plats préférés
respectifs


### **Nicolas**

![alt text](Images/Crypto_cyberchef/Nico_Vigenere.png)

## Partie 3 : Chiffrement symétrique AES

Dans « CyberChef » utilisez les recettes « AES Encrypt » et « AES Decrypt »

Découverte

- Chiffrez la chaîne 'TESTSECRET1234567' avec les paramètres suivants
   - Key : c34fa73d7c5f8901a23e4cd98e7f650d9a17d4e8f902fa0d3286d0beaad219b6
   - IV :
   - Mode : ECB
   - Input : mode Raw
   - Output : Hex
- Que constatez-vous si vous modifiez 1 caractère du texte initial ?
   - la sortie change

  ![alt text](Images/Crypto_cyberchef/AES_Encrypt.png) 

- Déchiffrez le texte AES chiffré précédemment en adaptant les paramètres
- Vous devez retrouver le texte d'origine

![alt text](Images/Crypto_cyberchef/AES_Decrypt.png)

- Transmission d’un message chiffré à votre binôme
   - Générer une clé adéquate
- Chiffrez le nom de votre équipe de sport préférée avec les paramètres suivants
   - Key : 0C9BEBFA8B9A5F5DD1B4DE0184089800A449641CEA48D2E3D60323A41E30B748
   - IV :
   - Mode : ECB
   - Input : mode Raw
   - Output : Hex
   - Texte a dechiffre : 374654dbf76524cb1078a958ab3bcd14

![alt text](Images/Crypto_cyberchef/AES_Encrypt_club.png)

- Transmettre le texte chiffré à votre binôme
- Transmettre la clé à votre binôme par un autre canal

- Au sein de votre binôme, déchiffrez le message pour découvrir vos équipes de sport préférées respectives

### **Nicolas**

![alt text](Images/Crypto_cyberchef/Nico_AES.png)

## Partie 4 : RSA

Dans « CyberChef » utilisez les recettes « Generate RSA Key Pair » « RSA Encrypt » et « RSA Decrypt »

Génération d’une paire de clés RSA


- Utilisez Generate RSA Key Pair avec une taille de 1024 bits

   - Que contiennent les clés générées ? (formats, longueur)

-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC1SHSH7Ytcg6p9VnnO+wQbeAx1
z4OJ6tCkUy6sNXrBI7wpdYl/3Vp1eA8q9oOD1wRcqSx8LOzx6M5QYStXGDenjIIG
WJpfiTgjs0CZG5HaumvPUO4dlpZRVjplDY+AOOY8mvoGiDyHvL7i10OPQn6uzMzd
m2n7myfOXaHOqRotKwIDAQAB
-----END PUBLIC KEY-----

Découverte

- Chiffrez le message suivant avec votre clé publique : LE MESSAGE EST SECRETSIMPLE
   - Quelle est la sortie chiffrée ? Mbh4yLkSLjP0uwqGpFs0OA4y5LP4c1Khwkma44SGE6Bn9EEhdDBuKqJu0dpOeWeN3BkKu21KkSHghcXyWzZqHvTJWaP6uQKgTbbl9l+xEjXdRrBUDoVWv0+t5/rZOcKnyPCMOtulaRe5w72CD6kJ42SlplT2MY4fZdTGfGaybKA=
   - Utilisez votre clé privée pour déchiffrer le message
   - La sortie est-elle identique au message d’origine ? Oui

  ![alt text](Images/Crypto_cyberchef/RSA_Decrypt.png)

Transmission d’un message chiffré à votre binôme

- Récupérez la clé publique de votre binôme
   - Chiffrez votre réplique préférée avec les paramètres suivants
   - Key : « -----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC4sfSKBC6S7bq01foHyDsaBMDb
4RNfC1nADmUFnanUTsDSJqFh8/3iHHchu6J2HYngF/dwg+MiESSAiN8NedTa8Kus
qxFGHeJU7QeLECubCr8QRYn78KcD87pXutJrtOItTGzbbUtSx28SCJuUYnME65HY
0ifXI11tJbuhoNExrQIDAQAB
-----END PUBLIC KEY-----
   - Encryption scheme : RSA-OAEP
   - Message Digest Algorithm : SHA-1

- Transmettre le texte chiffré à votre binôme
   - JS/akQlLSOGMqS1plgu3rwhqy2WqC3lnbP9yBPYRX41kvKUgXiWzs47mtlrZ3ME/HWNstD6DinmZT+7FYxaFZnx2JdowlSE4YiUSAtmDR1jD3amy4oBRACUNm4MLVZg/hppXyj5tJ2no7W2O5SuTTcIfuAxOvq3cJjzTawKCZSQ=

- Votre binôme, doit déchiffrer le message à l’aide de sa clé privée pour découvrir votre réplique préférée
- Inversez ensuite les rôles pour que chacun connaisse la réplique privée de son binôme

### **Nicolas**

![alt text](Images/Crypto_cyberchef/RSA_decrypt_Nico.png)


## Partie 5 : Hachage
- Utilisez différents algorithmes de hachage sur la chaîne ADMIN123
   - SHA-1 93a6682a45cca19a71a8c9e3015e0c4b3a80e22c
   - SHA-2 : 256, 512 5b40171489659251097e7790fc2f1892e2183a72546fe1df283d07865db9149c , 25974977f6b51e4e8707e78281ba9b19ec54357901d51383658c57e3747d72a2fe00b3bb2e20d310cbbe1c49a0b6bb71df9f047a6253875041ea567bc85b2fcd
   - SHA-3 : 256, 512 5bddba0700f67dc277fc021c256d888275f9c47f3e8d92752112ddd30edd5743 , 8d224b1287f5e84fbd9d14e493a14d91179c3111de584a2937f1ec76f82d9dccec4b33dad54dca5ab905443210c2d3067b00367c304be18705d0ff6d1be0399f

- Quelles sont les tailles des hashs produits ?

SHA-1	    160 bits

SHA-256	    256 bits

SHA-512	    512 bits

SHA3-256	256 bits

SHA3-512	512 bits	

- Est-il possible de retrouver le mot de passe à partir du hash ? Oui
- Essayez deux textes légèrement différents (TEST et TESt)
- Que constatez-vous dans les résultats des hashs ? ils ont changer
- Hacher le texte « hello » en SHA1 (80 rounds) : aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
- Crackez le hash sur https://crackstation.net/
- Le hash est cracké en quelques secondes, comment cela est-ce possible ? Car il fait parti d'une liste , du coup le hash est deja connu 
- Répéter le point précédent avec SHA1 (50 rounds)
- Le hash est-il cracké ? Pourquoi ? Non il n'est pas cracké car il ne reconnais pas le hash dans sa liste car les parametres de chiffrement on changer .

## Partie 6 : Encodage
- Encodez le mot « Bonjour » en base 64
   - Que représente le résultat ? Qm9uam91cg==

 ![alt text](Images/Crypto_cyberchef/EncodeB64.png) 

- Décoder le résultat obtenu précédemment

![alt text](Images/Crypto_cyberchef/DeccodeB64.png)

- Peut-on confondre encodage et chiffrement ? Pourquoi ? Non le chiffrement necessite une clé alors que l'encodage non 

## Bonus
- Le diaporama contient un message caché, tentez de le découvrir !
- Indice : plusieurs opérations utilisées dans le cadre de ce TP ont été utilisées pour cacher ce message…

![alt text](Images/Crypto_cyberchef/Bonus1.png)

![alt text](Images/Crypto_cyberchef/Bonus2.png)

![alt text](Images/Crypto_cyberchef/Bonus3.png)

- Avec le Hash en MD5

![alt text](Images/Crypto_cyberchef/Bonus.png)

# TP2 AES et RSA avec Open SSL

## Partie 1 : Chiffrement symétrique AES

**En utilisant OpenSSL**

### A.Découverte



- Chiffrez la chaîne 'TESTSECRET1234567' avec les paramètres suivants
   - Mode de chiffrement AES 256 bits en CBC
   - Sortie en base64
   - Ajouter un sel (salt) pour sécuriser la dérivation de clé
   - Fournir une passphrase (pour dériver la clé)

 ```bash
echo -n "TESTSECRET1234567" | openssl enc -aes-256-cbc -salt -pbkdf2 -base64 -pass pass:"lacryptocestgenial"
```

   ![alt text](Images/CryptoAES/CMD_chiffrement_test.png)

- Quelle est la clé réelle utilisée et comment est-elle générée ?

![alt text](Images/CryptoAES/CMD_key.png)

La clé réelle utilisée et la "KEY" et elle est générée automatiquement

- Déchiffrez le texte AES chiffré précédemment en adaptant les paramètres

```bash
echo "U2FsdGVkX18nFqDyPVPnJ+TCOGjlQKwpHZltFp0EqpSXrSpkTbHGTrloh/W2IvhF" | openssl enc -d -aes-256-cbc -pbkdf2 -base64 -pass pass:"lacryptocestgenial"
```
   - Vous devez retrouver le texte d'origine

### B. Transmission d’un message chiffré à votre binôme (passphrase)


```bash
root@CT-Maitre:~# echo -n "je m'en fou des voitures" | openssl enc -aes-256-cbc  -pbkdf2 -base64 -pass pass:"vroumvroum"
```
- Chiffrez le nom de votre voiture préférée avec les paramètres suivants
   - Mode de chiffrement AES 256 bits en CBC
   - Sortie en base64
   - Ne pas ajouter de sel (salt) pour sécuriser la dérivation de clé
   - Fournir une passphrase (pour dériver la clé)

![alt text](Images/CryptoAES/CMD_chiffrement_voiture.png)

- Transmettre le texte chiffré à votre binôme
- Transmettre la passphrase à votre binôme par un autre canal

- Au sein de votre binôme, déchiffrez le message pour découvrir vos voitures
préférées respectives

#### **Nicolas**

![alt text](Images/CryptoAES/Resulat_Nico_voiture.png)

### C.Transmission d’un message chiffré à votre binôme

- Générez une clé de chiffrement et un vecteur d'initialisation (IV) à partir d’une passphrase sans
sel

```bash
openssl enc -aes-256-cbc -nosalt -pbkdf2 -P -pass pass:"musique"
```

   - Notez les valeurs renvoyées

 ![alt text](Images/CryptoAES/CMD_Chiff_musique.png)  

- Chiffrez le nom de votre chanson préférée en utilisant la clé et l’IV générés précédemment
```bash
echo -n "Bohemian Rhapsody" | openssl enc -aes-256-cbc -base64 -K E100B969CE2D970B63B4E2FEFBA0864765E1BCB615CE1BA8A9D45DB256F5EBCC -iv 906B2632BE8855E64663181580356E23
```

![alt text](Images/CryptoAES/CMD_Chiff_musique2.png)

- Transmettre le texte chiffré à votre binôme
- Transmettre la clé et l’IV à votre binôme par un autre canal

   - Au sein de votre binôme, déchiffrez le message pour découvrir votre chanson
préférée respective

```bash
echo "yPU9P+3CQT+wDvK2P79ETRdXeeOnChn224hpXHtItks=" | openssl enc -d -aes-256-cbc -base64 -K E20458E08464955B200E6F07F79E87993AA11DAF97B5CBABFB3ADB6A9144F5E3 -iv 1E67EC9C18ED0FF43B9B597DF57DE86B
```

#### **Nicolas**

![alt text](Images/CryptoAES/Resultat_Nico_2.png)


## Partie 2 : RSA

En vous inspirant de l’exercice AES, réalisez l’équivalent avec RSA :

### A. Génération de la paire de clés RSA

- Générez une paire de clés RSA de 2048 bits

```bash
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
```

- Extraire la clé publique

```bash
openssl pkey -in private_key.pem -pubout -out public_key.pem
```

![alt text](Images/CryptoAES/Generate_RSA.png)

### B. Chiffrement d’un message

- Écrivez un court message (ex. : le nom de votre destination de tourisme préférée)

```bash
echo -n "MESSAGE" > message.txt
```

- Chiffrez-le avec la clé publique de votre binôme

```bash
openssl pkeyutl -encrypt -pubin -inkey public_key_binome.pem -in message.txt -out message_rsa.bin
```

![alt text](Images/CryptoAES/Generate_RSA_message.png)

### C. Échange et déchiffrement

- Transmettez le fichier chiffré (message_rsa.bin) à votre binôme.
- Votre binôme doit déchiffrer le message avec sa clé privée

![alt text](Images/CryptoAES/Nico_message_RSA.png)

## Partie 3 : BONUS

- Utilisez le chiffrement hybride pour transmettre à votre binôme les paroles de votre chanson préférée !

Le chiffrement hybride combine :
- **AES** → pour chiffrer les données (rapide)
- **RSA** → pour chiffrer la clé AES (sécurisé)

## 1. Génération des clés RSA (binôme)

```bash
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
openssl pkey -in private_key.pem -pubout -out public_key.pem
```


## 2. Génération clé AES + IV

```bash
openssl rand -hex 32 > aes_key.hex
openssl rand -hex 16 > aes_iv.hex
```


## 3. Chiffrement des données (AES-256-CBC)

```bash
openssl enc -aes-256-cbc -in paroles.txt -out paroles_chiffrees.bin \
-K $(cat aes_key.hex) -iv $(cat aes_iv.hex)
```
![alt text](Images/CryptoAES/Bonus1.png)

## 4. Chiffrement de la clé AES (RSA)

```bash
openssl pkeyutl -encrypt -pubin -inkey public_key_binome.pem \
-in aes_key.hex -out aes_key_chiffree.bin
```



## 5. Transmission

Envoyer au binôme :

- `paroles_chiffrees.bin`
- `aes_key_chiffree.bin`
- `aes_iv.hex`

![alt text](Images/CryptoAES/Bonus2.png)

## 6. Déchiffrement de la clé AES (RSA)

```bash
openssl pkeyutl -decrypt -inkey private_key.pem \
-in aes_key_chiffree.bin -out aes_key_dechiffree.hex
```


## 7. Déchiffrement des données (AES)

```bash
openssl enc -d -aes-256-cbc -in paroles_chiffrees.bin \
-out paroles_dechiffrees.txt \
-K $(cat aes_key_dechiffree.hex) -iv $(cat aes_iv.hex)
```
## 8. Lecture des paroles

```bash
cat paroles_dechiffrees.txt
```

#### **Nicolas**

![alt text](Images/CryptoAES/Nico_parole.png)

# TP3 SSH

## Partie1 : Configuration initiale

**Génération de la clé SSH**

- Générer une paire de clé RSA 4096

```bash
ssh-keygen -t rsa -b 4096 -C
```
![alt text](Images/Crypto_SSH/Generatekey.png)

   - Deux fichiers doivent être générés :
     - id_rsa (clé privée, à ne pas partager)
     - id_rsa.pub (clé publique)

![alt text](Images/Crypto_SSH/Generatekey2.png)


- Dépôt de la clé publique dans le serveur distant

```bash
scp ~/.ssh/id_rsa_VM_ansible.pub root@192.168.1.13:~
```
![alt text](Images/Crypto_SSH/Import_keyssh_serveur.png)

   - Copier `id_rsa.pub` dans le home de l'utilisateur
   - Déplacer la clé à l'emplacement correct et ajuster les droits (créer les dossiers nécessaires
le cas échéant)

```bash
cat ~/id_rsa_VM_ansible.pub >> ~/.ssh/authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
![alt text](Images/Crypto_SSH/Copie_keyssh_serveur.png)

- Configuration du serveur pour forcer l’authentification par clé

```bash
sudo nano /etc/ssh/sshd_config
```
- Adapter le fichier de configuration ssh pour forcer l’authentification par clé uniquement
```
PermitRootLogin prohibit-password
PubkeyAuthentication yes
PasswordAuthentication no

```
![alt text](Images/Crypto_SSH/ssh_config.png)

- Redémarrer le service SSH pour appliquer la configuration
   
```bash
sudo systemctl restart ssh
```

## Partie2 : Validation du fonctionnement

- Connectez-vous au serveur sans mot de passe à l’aide de votre clé privée

```bash
 ssh -i $env:USERPROFILE\.ssh\id_rsa_VM_ansible root@192.168.1.13
```
![alt text](Images/Crypto_SSH/Connexion.png)

- Répondez aux questions suivantes :

  - Ce qui se passe si vous supprimez la clé privée 
     - On ne peut plus se connecter au serveur.

  - Comment réactiver l'authentification par mot de passe en cas de besoin
     - il faut passer le champ "PasswordAuthentication" de "no" à "yes", et redemarrer les services.

## Supplement : Créer un alias SSH

- Dans le Dossier .ssh creer un fichier config avec le bloc notes et supprimer l'extension .txt
  - Ouvrez ce fichier et coller :
```
Host NOM_CHOISI "ex: VM"
    HostName IP du serveur 
    User Nom de l'user
    Port 22 par default 
    IdentityFile Chemin\de\la\cle\privee
```
![alt text](Images/Crypto_SSH/config_alias.png)

- Test de connexion

```bash
 ssh VM
```
![alt text](Images/Crypto_SSH/Connexion_alias.png)

## Partie 3 : Bonus

- Activation et utilisation de ssh-agent

- Quel est le rôle de ssh-agent ?
 - Stocker les clés privées en mémoire
 - Éviter de taper la passphrase à chaque connexion
 - Gérer plusieurs clés facilement

 - Configurez et testez ssh-agent
     - Sur l’OS Windows

 ```bash
ssh-add $env:USERPROFILE\.ssh\id_rsa_VM_ansible
```
![alt text](Images/Crypto_SSH/Add_agent_windows.png)

- Test de Connexion IP + Alias

  ![alt text](Images/Crypto_SSH/Connexion_avec_agent.png)


# TP4 RockYou John

- Vous devez cracker les différents fichiers mis à votre disposition

- Utiliser pour cela John The Ripper et la wordlist « RockYou »
