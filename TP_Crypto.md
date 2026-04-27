# Partie 1 : Chiffrement de César

Dans « CyberChef » utilisez la recette « ROT13 »

1. Avec une « Box Height » de 13, chiffrer la phrase suivante : RENDEZ-VOUS À MIDI

- Quel est le texte chiffré ?

  - ERAQRM-IBHF À ZVQV

- Déchiffrez ce texte pour vérifier le résultat

![alt text](Images/Crypto/ROT13.png)


2. Chiffrer le nom de votre film préféré avec une « Box Height » de votre choix

- Transmettre le texte chiffré à votre binôme sans lui communiquer la clé

  - P jiol Pyhxynnu

- Au sein de votre binôme, essayer de retrouver le message en sens inverse 

### **Nicolas**

![alt text](Images/Crypto/Rot25_Nico.png)

# Partie 2 : Vigenère

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

![alt text](Images/Crypto/Nico_Vigenere.png)

# Partie 3 : Chiffrement symétrique AES

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

   ![alt text](Images/Crypto/AES_Encrypt.png)

- Déchiffrez le texte AES chiffré précédemment en adaptant les paramètres
- Vous devez retrouver le texte d'origine

![alt text](Images/Crypto/AES_Decrypt.png)

- Transmission d’un message chiffré à votre binôme
   - Générer une clé adéquate
- Chiffrez le nom de votre équipe de sport préférée avec les paramètres suivants
   - Key : 0C9BEBFA8B9A5F5DD1B4DE0184089800A449641CEA48D2E3D60323A41E30B748
   - IV :
   - Mode : ECB
   - Input : mode Raw
   - Output : Hex
   - Texte a dechiffre : 374654dbf76524cb1078a958ab3bcd14

![alt text](Images/Crypto/AES_Encrypt_club.png)

- Transmettre le texte chiffré à votre binôme
- Transmettre la clé à votre binôme par un autre canal

- Au sein de votre binôme, déchiffrez le message pour découvrir vos équipes de sport préférées respectives

### **Nicolas**

![alt text](Images/Crypto/Nico_AES.png)

# Partie 4 : RSA

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

   ![alt text](Images/Crypto/RSA_Decrypt.png)

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

![alt text](Images/Crypto/RSA_decrypt_Nico.png)


# Partie 5 : Hachage
- Utilisez différents algorithmes de hachage sur la chaîne ADMIN123
   - SHA-1 93a6682a45cca19a71a8c9e3015e0c4b3a80e22c
   - SHA-2 : 256, 512 5b40171489659251097e7790fc2f1892e2183a72546fe1df283d07865db9149c , 25974977f6b51e4e8707e78281ba9b19ec54357901d51383658c57e3747d72a2fe00b3bb2e20d310cbbe1c49a0b6bb71df9f047a6253875041ea567bc85b2fcd
   - SHA-3 : 256, 512 5bddba0700f67dc277fc021c256d888275f9c47f3e8d92752112ddd30edd5743 , 8d224b1287f5e84fbd9d14e493a14d91179c3111de584a2937f1ec76f82d9dccec4b33dad54dca5ab905443210c2d3067b00367c304be18705d0ff6d1be0399f

- Quelles sont les tailles des hashs produits ?

- Est-il possible de retrouver le mot de passe à partir du hash ? Oui
- Essayez deux textes légèrement différents (TEST et TESt)
- Que constatez-vous dans les résultats des hashs ? ils sont changer
- Hacher le texte « hello » en SHA1 (80 rounds) : aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
- Crackez le hash sur https://crackstation.net/
- Le hash est cracké en quelques secondes, comment cela est-ce possible ? Car il fait parti d'une liste , du coup le hash est deja connu 
- Répéter le point précédent avec SHA1 (50 rounds)
- Le hash est-il cracké ? Pourquoi ? Non il n'est pas cracké car il ne reconnais pas le hash dans sa lite

# Partie 6 : Encodage
- Encodez le mot « Bonjour » en base 64
   - Que représente le résultat ? Qm9uam91cg==

   ![alt text](Images/Crypto/EncodeB64.png)

- Décoder le résultat obtenu précédemment

![alt text](Images/Crypto/DeccodeB64.png)

- Peut-on confondre encodage et chiffrement ? Pourquoi ? Non le chiffrement necessite une clé alors que l'encodage non 

# Bonus
- Le diaporama contient un message caché, tentez de le découvrir !
- Indice : plusieurs opérations utilisées dans le cadre de ce TP ont été utilisées pour cacher ce message…

![alt text](Images/Crypto/Bonus1.png)

![alt text](Images/Crypto/Bonus2.png)

![alt text](Images/Crypto/Bonus3.png)

- Avec le Hash en MD5
![alt text](Images/Crypto/Bonus.png)
