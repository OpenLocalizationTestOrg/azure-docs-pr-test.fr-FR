---
title: "aaaConnect tooAzure pile avec l’interface CLI | Documents Microsoft"
description: "Découvrez comment toouse hello (CLI) d’une interface de ligne inter-plateformes toomanage et déployer des ressources sur la pile de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: ffb1ffd2b7784e188487bef98fe5b2add8e96784
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a>Installer et configurer l’interface CLI pour une utilisation avec Azure Stack

Dans ce document, nous vous guidera hello d’utilisation des ressources de Kit de développement Azure pile toomanage Azure Interface de ligne de commande (CLI) à partir de plateformes de client Mac et Linux. 

## <a name="export-hello-azure-stack-ca-root-certificate"></a>Exporter le certificat de hello Azure pile autorité de certification racine

Si vous utilisez l’interface CLI à partir d’un ordinateur virtuel qui est en cours d’exécution dans l’environnement du Kit de développement de pile Azure hello, certificat racine de pile de Azure hello est déjà installé dans l’ordinateur virtuel de hello afin de récupérer directement. Alors que si vous utilisez CLI à partir d’une station de travail à l’extérieur du kit de développement hello, vous devez exporter le certificat de hello Azure pile autorité de certification racine du kit de développement hello et ajoutez-le toohello Python magasin de certificats de votre station de travail de développement (externe Linux ou Mac plateforme ). 

Se connecter dans le kit de développement tooyour et exécutez hello suivant script tooexport hello Azure pile certificat au format PEM :

```powershell
   $label = "AzureStackSelfSignedRootCert"
   Write-Host "Getting certificate from hello current user trusted store with subject CN=$label"
   $root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
   if (-not $root)
   {
       Log-Error "Cerficate with subject CN=$label not found"
       return
   }

   Write-Host "Exporting certificate"
   Export-Certificate -Type CERT -FilePath root.cer -Cert $root

   Write-Host "Converting certificate tooPEM format"
   certutil -encode root.cer root.pem
```

## <a name="install-cli"></a>Installer l’interface CLI

Ensuite, vous devez vous connecter une station de travail de développement tooyour et installer l’interface CLI. Pile Azure nécessite une version 2.0 de hello du CLI d’Azure, vous pouvez installer à l’aide des étapes hello Bonjour [installer Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) l’article. tooverify si l’installation de hello a réussi, ouvrez un terminal ou une fenêtre d’invite de commandes et leur exécution hello commande suivante :

```azurecli
az --version
```

Vous devez voir version hello de CLI d’Azure et d’autres bibliothèques dépendantes sont installés sur votre ordinateur.

## <a name="trust-hello-azure-stack-ca-root-certificate"></a>Certificat de hello Azure pile autorité de certification racine de confiance

tootrust hello Azure pile certificat racine, vous devez l’ajouter de certificat de python toohello existant. Si vous exécutez CLI à partir d’un ordinateur Linux est créé dans l’environnement de Azure pile hello, suivante d’exécution hello bash commande :

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

Si vous exécutez à partir d’un ordinateur en dehors de l’environnement de Azure sac hello CLI, vous devez tout d’abord configurer [tooAzure de connectivité VPN pile](azure-stack-connect-azure-stack.md). Maintenant, copiez hello PEM certificat que vous avez exporté précédemment sur votre station de travail de développement et exécutez hello suivant de commandes en fonction du système d’exploitation de votre station de travail développement :

### <a name="linux"></a>Linux

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a>macOS

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a>Windows

```powershell
$pemFile = "<Fully qualified path toohello PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from hello cert file"
$md5Hash=(Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash=(Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash=(Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry  = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path root.pem -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding hello certificate content tooPython Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing hello azure stack CA root certificate"
```

## <a name="set-up-hello-virtual-machine-aliases-endpoint"></a>Définir des points de terminaison alias hello machine virtuelle

Avant que les utilisateurs peuvent créer des machines virtuelles à l’aide de CLI, administrateur du cloud hello doit définir un point de terminaison accessible publiquement qui contiennent des alias d’image de machine virtuelle et inscrire ce point de terminaison avec le cloud de hello. Hello `endpoint-vm-image-alias-doc` paramètre Bonjour `az cloud register` commande est utilisée à cet effet. Les administrateurs de cloud doivent télécharger marketplace d’Azure pile hello image toohello avant de leur point de terminaison tooimage alias l’ajouter.
   
Par exemple, Azure utilise l’URI suivant : https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json. Hello cloud administrateur doit configurer un point de terminaison similaire pour la pile d’Azure avec des images hello qui sont disponibles dans le marketplace d’Azure pile hello.

## <a name="connect-tooazure-stack"></a>Se connecter tooAzure pile

Utilisez hello suivant les étapes tooconnect tooAzure pile :

1. Inscrire votre environnement Azure pile en exécutant la commande de Registre hello az cloud.
   
   a. tooregister hello **cloud administration** environnement, utilisez :

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

   b. tooregister hello **utilisateur** environnement, utilisez :

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

2. Ensemble hello environnement actif à l’aide de hello suivant de commandes :

   a. Pourquoi **cloud administration** environnement, utilisez :

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   b. Pourquoi **utilisateur** environnement, utilisez :

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. Mettre à jour votre hello de toouse configuration environnement profil version API spécifique de pile de Azure. configuration de hello tooupdate, exécutez hello de commande suivante :

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. Se connecter dans l’environnement de Azure pile tooyour à l’aide de hello **ouverture de session az** commande. Vous pouvez vous connecter dans l’environnement de Azure pile toohello en tant qu’un utilisateur ou un [principal du service](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects). 

   * Connectez-vous en tant qu’un **utilisateur**: vous pouvez spécifier le nom d’utilisateur hello et un mot de passe directement dans la commande de connexion az hello ou authentifier à l’aide d’un navigateur. Vous devriez hello toodo ce dernier cas, si votre compte dispose de l’authentification multifacteur activée.

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > Si votre compte d’utilisateur a l’authentification multifacteur activée, vous pouvez utiliser la commande de connexion hello az sans fournir le paramètre -u de hello. Commande hello en cours d’exécution, vous donne une URL et un code que vous devez utiliser tooauthenticate.
   
   * Connectez-vous en tant qu’un **principal du service**: avant de vous connecter, [créer un principal de service via hello portail Azure](azure-stack-create-service-principals.md) ou l’interface CLI et lui attribuer un rôle. Maintenant, connectez-vous à l’aide de hello de commande suivante :

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of hello Service Principal> \
     -p <Key generated for hello Service Principal>
   ```

## <a name="test-hello-connectivity"></a>Tester la connectivité hello

Maintenant que nous avons tout ce que le programme d’installation, nous allons utiliser les ressources de toocreate CLI au sein de la pile de Azure. Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle. Hello utilisation suivant commande toocreate un groupe de ressources nommé « MyResourceGroup » :

```azurecli
az group create \
  -n MyResourceGroup -l local
```

Si le groupe de ressources hello est créé avec succès, commande précédente hello génère hello propriétés de ressource de hello nouvellement créé suivantes :

![Sortie de la création du groupe de ressources](media/azure-stack-connect-cli/image1.png)

Il existe certains problèmes connus lors de l’utilisation de CLI 2.0 dans Azure pile, toolearn sur ces problèmes, consultez hello [problèmes connus dans Azure pile CLI](azure-stack-troubleshooting.md#cli) rubrique. 

## <a name="next-steps"></a>Étapes suivantes

[Déployer des modèles avec l’interface de ligne de commande Azure](azure-stack-deploy-template-command-line.md)

[Se connecter avec PowerShell](azure-stack-connect-powershell.md)

[Gérer les autorisations utilisateur](azure-stack-manage-permissions.md)

