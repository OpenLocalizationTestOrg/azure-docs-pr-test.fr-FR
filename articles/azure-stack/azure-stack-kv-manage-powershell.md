---
title: "aaaManage le coffre de clés dans la pile de Azure à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toomanage le coffre de clés dans la pile de Azure à l’aide de PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 37adddf8da02766559f4d61134a9d5ce47377da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a>Gérer Key Vault dans Azure Stack à l’aide de PowerShell

Cet article vous aidera à obtenir toocreate démarrée et gérer le coffre de clés dans la pile d’Azure à l’aide de PowerShell. applets de commande PowerShell de coffre de clé Hello décrits dans cet article sont disponibles dans le cadre de hello Kit de développement logiciel Azure PowerShell. Hello sections suivantes décrivent des hello applets de commande PowerShell sont requis toocreate un coffre, stocker et gérer les clés de chiffrement et les clés secrètes ainsi autoriser des utilisateurs ou des applications opérations tooinvoke dans le coffre hello. 

## <a name="prerequisites"></a>Composants requis
* [Installer PowerShell pour Azure Stack.](azure-stack-powershell-install.md)  
* Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés hello.  
* Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello. 
* [Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a>Activer votre abonnement de locataire pour les opérations de coffre

Avant de pouvoir émettre des opérations sur un coffre de clés, vous devez tooensure votre abonnement client est activée pour les opérations de coffre. tooverify, exécutez hello de commande suivante :

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
**Sortie**

Si votre abonnement est activé pour les opérations d’archivage, sortie de hello affiche « RegistrationState » est égal à « Enregistré » pour tous les types de ressources d’un coffre de clés.

![état de l’inscription](media/azure-stack-kv-manage-powershell/image1.png)

Si tel n’est pas le cas de hello, appelez hello suivant du service de coffre de clés commande tooregister hello dans votre abonnement :

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

**Sortie**

Si l’inscription de hello a réussi, hello sortie suivante est retournée :

![inscription](media/azure-stack-kv-manage-powershell/image2.png)

Hello sections suivantes supposent service Key Vault est enregistré au sein de l’abonnement d’utilisateur hello. Lors de l’appel des commandes de coffre de clés, si vous obtenez une erreur s’affiche : « abonnement de hello n’est pas un espace de noms toouse inscrit ' Microsoft.KeyVault », confirmez que vous avez [activé le fournisseur de ressources de coffre de clés hello](#enable-your-tenant-subscription-for-vault-operations) conformément aux instructions indiqué précédemment.

## <a name="create-a-key-vault"></a>Création d’un coffre de clés 

Avant de créer un coffre de clés, créez un groupe de ressources pour que toutes les ressources associées au coffre de clés existent dans un groupe de ressources. Utilisez hello suivant commande toocreate un groupe de ressources :

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

**Sortie**

![new resource group](media/azure-stack-kv-manage-powershell/image3.png)

À présent, utiliser hello **New-AzureRMKeyVault** commande toocreate un coffre de clés dans le groupe de ressources hello que vous avez créé précédemment. Cette commande lit trois paramètres obligatoires : le nom du groupe de ressources, le nom du coffre de clés et l’emplacement géographique. 

Exécutez hello suivant commande toocreate un coffre de clés :

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
**Sortie**

![nouveau coffre de clés](media/azure-stack-kv-manage-powershell/image4.png)

sortie Hello de cette commande affiche les propriétés de hello de coffre de clés hello que vous avez créé. Lorsqu’une application accède à ce coffre, elle utilise hello **coffre URI** propriété indiquée dans la sortie de hello. Par exemple, le coffre hello URI ici est **https://vault01.vault.local.azurestack.external**. Les applications qui interagissent avec ce coffre de clés par le biais de l’API REST doivent utiliser cet URI.

Dans les déploiements AD FS, quand vous créez un coffre de clés à l’aide de PowerShell, vous pouvez recevoir un avertissement indiquant que la stratégie d’accès n’est pas définie Aucun utilisateur ou l’application n’a accès autorisation toouse cet archivage ». tooresolve ce problème, définissez une stratégie d’accès pour l’archivage hello par à l’aide de hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) commande :

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a>Gérer les clés et les secrets

Après avoir créé un coffre, hello suivant les étapes toocreate et gérer les clés et les secrets dans le coffre hello.

### <a name="create-a-key"></a>Créer une clé

Hello d’utilisation **Add-AzureKeyVaultKey** commande toocreate ou importer une clé protégée de logiciel dans un coffre de clés. 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
Hello **Destination** sert de paramètre toospecify cette clé hello est protégé par un logiciel. Lors de la clé de hello est correctement créé, commande hello renvoie les détails de hello Hello crée de la clé.

**Sortie**

![Nouvelle clé](media/azure-stack-kv-manage-powershell/image5.png)

Vous pouvez maintenant référencer hello créé de la clé à l’aide de son URI. Si vous créez ou importez une clé qui a le même nom qu’une clé existante, la clé d’origine de hello est mise à jour avec les valeurs hello qui sont spécifiés dans la nouvelle clé de hello.  Vous pouvez accéder à version précédente de hello à l’aide spécifique à la version hello URI de clé de hello. Par exemple, 

* Utilisez **https://vault10.vault.local.azurestack.external:443/clés/key01** tooalways obtenir la version actuelle de hello  
* Utilisez **https://vault010.vault.local.azurestack.external:443/clés/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget cette version spécifique

### <a name="get-a-key"></a>Obtenir une clé

Hello d’utilisation **Get-AzureKeyVaultKey** commande tooread une clé et ses détails.

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a>Créer un secret

Hello d’utilisation **Set-AzureKeyVaultSecret** toocreate de commande ou de mettre à jour une clé secrète dans un coffre. Une clé secrète est créée si elle n’existe pas déjà, et une nouvelle version du secret de hello est créée s’il existe déjà.

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

**Sortie**

![créer un secret](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a>Obtenir un secret

Hello d’utilisation **Get-AzureKeyVaultSecret** commande tooread une clé secrète dans un coffre de clés. Cette commande peut retourner toutes les versions ou des versions spécifiques d’un secret. 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

Après avoir créé les clés et les clés secrètes, vous pouvez autoriser des applications externes toouse les.

## <a name="authorize-an-application-toouse-a-key-or-secret"></a>Autoriser un toouse application une clé ou une clé secrète

tooauthorize un tooaccess application une clé ou au secret dans hello clé de coffre, utilisez hello **Set-AzureRmKeyVaultAccessPolicy** commande.
Par exemple, si le nom de votre coffre est ContosoKeyVault et hello application souhaité tooauthorize a l’ID Client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed. Exécutez hello après application de commande tooauthorize hello. Vous pouvez éventuellement spécifier hello **PermissionsToKeys** paramètre tooset autorisations pour un utilisateur, application ou un groupe de sécurité :

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

Si vous souhaitez tooauthorize de ce même secrets de tooread application dans le coffre, exécutez hello suivant l’applet de commande :

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a>Étapes suivantes
* [Déployer une machine virtuelle avec un mot de passe stocké dans un coffre de clés](azure-stack-kv-deploy-vm-with-secret.md)  
* [Déployer une machine virtuelle avec un certificat stocké dans un coffre de clés](azure-stack-kv-push-secret-into-vm.md) 
