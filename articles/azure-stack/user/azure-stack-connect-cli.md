---
title: "Se connecter à Azure Stack avec l’interface CLI | Microsoft Docs"
description: "Découvrez comment utiliser l’interface de ligne de commande (CLI) multiplateforme pour gérer et déployer des ressources sur Azure Stack."
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
ms.openlocfilehash: bd731c32d32063b54d5899db3b3a13a911ca79be
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a>Installer et configurer l’interface CLI pour une utilisation avec Azure Stack

Dans ce document, nous vous guidons tout au long du processus d’utilisation de l’interface de ligne de commande (CLI) Azure pour gérer les ressources du kit de développement Azure Stack à partir des plateformes clientes Mac et Linux. 

## <a name="export-the-azure-stack-ca-root-certificate"></a>Exporter le certificat racine d’autorité de certification Azure Stack

Si vous utilisez l’interface CLI à partir d’une machine virtuelle exécutée dans l’environnement du Kit de développement Azure Stack, le certificat racine d’Azure Stack est déjà installé sur la machine virtuelle. Vous pouvez donc le récupérer directement. En revanche, si vous utilisez l’interface CLI à partir d’une station de travail à l’extérieur du kit de développement, vous devez exporter le certificat racine d’autorité de certification Azure Stack à partir du kit de développement et l’ajouter au magasin de certificats Python de votre station de travail de développement (plateforme Linux ou Mac externe). 

Connectez-vous à votre kit de développement et exécutez le script suivant pour exporter le certificat racine Azure Stack au format PEM :

```powershell
   $label = "AzureStackSelfSignedRootCert"
   Write-Host "Getting certificate from the current user trusted store with subject CN=$label"
   $root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
   if (-not $root)
   {
       Log-Error "Cerficate with subject CN=$label not found"
       return
   }

   Write-Host "Exporting certificate"
   Export-Certificate -Type CERT -FilePath root.cer -Cert $root

   Write-Host "Converting certificate to PEM format"
   certutil -encode root.cer root.pem
```

## <a name="install-cli"></a>Installer l’interface CLI

Vous devez maintenant vous connecter à votre station de travail de développement et installer l’interface CLI. Azure Stack requiert la version 2.0 d’Azure CLI, que vous pouvez installer en suivant les étapes décrites dans l’article [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Pour vérifier que l’installation a réussi, ouvrez un terminal ou une fenêtre d’invite de commandes et exécutez la commande suivante :

```azurecli
az --version
```

Vous devriez voir la version d’Azure CLI et d’autres bibliothèques dépendantes installées sur votre ordinateur.

## <a name="trust-the-azure-stack-ca-root-certificate"></a>Approuver le certificat racine d’autorité de certification Azure Stack

Pour approuver le certificat racine d’autorité de certification Azure Stack, vous devez l’ajouter au certificat Python existant. Si vous exécutez l’interface CLI sur une machine Linux créée dans l’environnement Azure Stack, exécutez la commande bash suivante :

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

Si vous exécutez l’interface CLI sur une machine qui se trouve en dehors de l’environnement Azure Stack, vous devez tout d’abord configurer la [connectivité VPN à Azure Stack](azure-stack-connect-azure-stack.md). Copiez à présent le certificat PEM que vous avez exporté auparavant dans votre station de travail de développement et exécutez les commandes suivantes en fonction du système d’exploitation de votre station de travail de développement :

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
$pemFile = "<Fully qualified path to the PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from the cert file"
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

Write-Host "Adding the certificate content to Python Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing the azure stack CA root certificate"
```

## <a name="set-up-the-virtual-machine-aliases-endpoint"></a>Configurer le point de terminaison des alias de machines virtuelles

Pour que les utilisateurs puissent créer des machines virtuelles à l’aide de l’interface CLI, l’administrateur de cloud doit d’abord configurer un point de terminaison accessible publiquement qui contienne les alias d’images de machines virtuelles et inscrire ce point de terminaison sur le cloud. Le paramètre `endpoint-vm-image-alias-doc` dans la commande `az cloud register` est utilisé à cet effet. Les administrateurs de cloud doivent télécharger l’image sur la Place de marché Azure Stack avant de l’ajouter au point de terminaison des alias d’images.
   
Par exemple, Azure utilise l’URI suivant : https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json. L’administrateur de cloud doit configurer un point de terminaison similaire pour Azure Stack avec les images disponibles dans la Place de marché Azure Stack.

## <a name="connect-to-azure-stack"></a>Se connecter à Azure Stack

Suivez les étapes ci-dessous pour vous connecter à Azure Stack :

1. Inscrivez votre environnement Azure Stack en exécutant la commande az cloud register.
   
   a. Pour inscrire l’environnement **administrateur de cloud**, utilisez :

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
   ```

   b. Pour inscrire l’environnement **utilisateur**, utilisez :

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
   ```

2. Définissez l’environnement actif à l’aide des commandes suivantes :

   a. Pour l’environnement **administrateur de cloud**, utilisez :

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   b. Pour l’environnement **utilisateur**, utilisez :

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. Mettez à jour la configuration de votre environnement pour utiliser le profil de version des API propre à Azure Stack. Pour mettre à jour la configuration, exécutez la commande suivante :

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. Connectez-vous à votre environnement Azure Stack avec la commande **az login**. Vous pouvez vous connecter à l’environnement Azure Stack en tant qu’utilisateur ou que [principal de service](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects). 

   * Connexion en tant **qu’utilisateur** : vous pouvez spécifier directement le nom d’utilisateur et le mot de passe dans la commande az login ou vous authentifier avec un navigateur. Vous devez choisir cette dernière solution si l’authentification multifacteur est activée sur votre compte.

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > Si l’authentification multifacteur est activée sur votre compte d’utilisateur, vous pouvez utiliser la commande az login sans fournir le paramètre -u. Elle vous donne une URL et un code qui vous permettent de vous authentifier.
   
   * Connexion en tant que **principal de service** : avant de vous connecter, [créez un principal de service avec le portail Azure](azure-stack-create-service-principals.md) ou l’interface CLI et attribuez-lui un rôle. Ensuite, connectez-vous avec la commande suivante :

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of the Service Principal> \
     -p <Key generated for the Service Principal>
   ```

## <a name="test-the-connectivity"></a>Tester la connectivité

Maintenant que tout est configuré, nous allons utiliser l’interface CLI pour créer des ressources dans Azure Stack. Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle. Utilisez la commande suivante pour créer le groupe de ressources nommé « myResourceGroup » :

```azurecli
az group create \
  -n MyResourceGroup -l local
```

Si la création du groupe de ressources réussit, la commande précédente affiche les propriétés suivantes pour la ressource créée :

![Sortie de la création du groupe de ressources](media/azure-stack-connect-cli/image1.png)

## <a name="next-steps"></a>Étapes suivantes

[Déployer des modèles avec l’interface de ligne de commande Azure](azure-stack-deploy-template-command-line.md)

[Gérer les autorisations utilisateur](azure-stack-manage-permissions.md)

