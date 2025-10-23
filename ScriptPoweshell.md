## 1 -  Vérifiez à l'aide d'un langage de script si vous avez les KB5049622, KB5049625 et Un KB présent de votre choix présent sur votre OS Windows. Le script devra afficher en Vert les KB présents et en rouge les KB absents.

 - ***Lister les KB***

``` Powershell
Get-Hotfix
```
Recuperer un KB valide au choix

 - ***Executez le script***
    
    ``` Powershell
    
    $var = @("KB5049622", "KB5049625", "KB/valide/choisis")
    foreach ( $KB in $var) {
    $result = Get-HotFix -id $KB -ErrorAction SilentlyContinue
    if ($result) { 
        Write-Host "$KB" -ForegroundColor Green
        } else {
            Write-Host "$KB" -ForegroundColor Red
        }
    }
    ```
Cela doit retourner

<img width="586" height="213" alt="image" src="https://github.com/user-attachments/assets/4d46d4f8-ba82-480a-8e7b-8222a1a63d0d" />

## 2 - Une fois que votre script fonctionne, placer la liste des KB dans un fichier texte nommé kb_list.txt, le script devra lire ce fichier pour obtenir la liste des KB.

 - ***Creer le fichier au meme endroit que le script est enregistrer, puis remplacer la premiere ligne par***
  
  ``` Powershell
   
  $var = Get-Content ".\kb_list.txt"
  ```
 - Cela doit donner
    
  ``` Powershell
  
    # Lire la liste des KB depuis le fichier texte
    $var = Get-Content ".\kb_list.txt"

    # Parcourt les KB

    foreach ( $KB in $var) {
    $result = Get-HotFix -id $KB -ErrorAction SilentlyContinue
    if ($result) { 
        Write-Host "$KB" -ForegroundColor Green
        } else {
            Write-Host "$KB" -ForegroundColor Red
        }
    }
  ```
  - Puis relancer le Script.
 
## 3 - Proposer une procédure, à écrire en commentaire du script, pour appliquer ce script sur un parc Windows AD

 ``` Powershell

  # Lire la liste des KB depuis le fichier texte
$var = Get-Content ".\kb_list.txt"

# Parcourt les KB

foreach ( $KB in $var) {
    $result = Get-HotFix -id $KB -ErrorAction SilentlyContinue
    if ($result) { 
        Write-Host "$KB" -ForegroundColor Green
        } else {
            Write-Host "$KB" -ForegroundColor Red
        }
}

<#
Déploiement du script via GPO (Active Directory)

1. Copier ScriptKB.ps1 et kb_list.txt dans un dossier partagé,
   ex : \\SERVEUR\PartageScripts\KBCheck\
2. Créer une GPO :
   - Configuration ordinateur > Stratégies > Paramètres Windows > Scripts (démarrage)
   - Ajouter ScriptKB.ps1 dans la section "Démarrage"
3. Activer l’exécution de scripts :
   Configuration ordinateur > Modèles d’administration >
   Composants Windows > Windows PowerShell >
   "Activer l’exécution de scripts" → Autoriser tous les scripts
4. Forcer la GPO sur les postes : gpupdate /force
   → Le script s’exécutera au démarrage.
5. (Optionnel) Ajouter dans le script :
   "$env:COMPUTERNAME : $KB OK/Non" |
   Out-File "\\SERVEUR\PartageScripts\KBCheck\resultats.txt" -Append

#>
 ```
## 4 - Signer votre script afin d'en prouver l'integrité et l'authenticité

- ***Générer un certificat auto-signé***

Utilisez la cmdlet PowerShell pour créer un certificat pour la signature de code, stocké dans le magasin personnel « Cert:\LocalMachine\My » :
```PowerShell

$SelfSignedCert = New-SelfSignedCertificate -Subject "ScriptPowerShell" -Type CodeSigningCert -CertStoreLocation Cert:\LocalMachine\My -FriendlyName "Signer scripts PowerShell" -NotAfter (Get-Date).AddYears(5)
```

- ***Exporter le certificat dans un fichier .cer***

Pour pouvoir l’installer dans les magasins de confiance, exportez-le sur disque :

```PowerShell

Export-Certificate -Cert $SelfSignedCert -FilePath "C:\Chemin\voulu\certificat.cer"
```

- ***Importer le certificat dans les magasins de confiance***
Pour que le certificat soit reconnu comme valide par Windows et PowerShell, il doit être ajouté à : Autorités de certification racine de confiance :

```PowerShell

Import-Certificate -FilePath "C:\Chemin\voulu\certificat.cer" -CertStoreLocation Cert:\LocalMachine\Root
```

- ***Éditeurs approuvés (TrustedPublisher)***

```PowerShell

Import-Certificate -FilePath "C:\chemin\voulu\certificat.cer" -CertStoreLocation Cert:\LocalMachine\TrustedPublisher
```

- ***Signer le script PowerShell***

Utilisez la cmdlet pour appliquer la signature avec le certificat auto-signé :

```PowerShell

Set-AuthenticodeSignature -FilePath "C:\Chemin\Du\Script\.ps1" -Certificate $SelfSignedCert
```

- ***Vérifier la signature du script***

Pour s’assurer que la signature est bien appliquée :

```PowerShell

Get-AuthenticodeSignature -FilePath "C:\Chemin\Du\Script\.ps1"
```

Cela doit afficher "Valid"

<img width="935" height="60" alt="image" src="https://github.com/user-attachments/assets/23d54be8-a792-43d2-ab54-0e9f64fc0534" />

## 5- Script Final 

<img width="748" height="1313" alt="image" src="https://github.com/user-attachments/assets/0f3b7fb5-a5fa-4459-8aec-793a099c05a3" />


   
  
    






  
