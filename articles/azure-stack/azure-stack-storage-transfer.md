---
title: aaaTools pour le stockage de la pile de Azure
description: "En savoir plus sur les outils de transfert de données du stockage Azure Stack"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/16/2017
ms.author: xiaofmao
ms.openlocfilehash: 184a1a51b4267e913aae823df31df3704d8e7b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tools-for-azure-stack-storage"></a>Outils du stockage Azure Stack

Pile de Microsoft Azure fournit un ensemble de services de stockage hello pour les disques, les objets BLOB, les tables, les files d’attente et les fonctionnalités de gestion de compte. Vous pouvez utiliser un ensemble d’outils de stockage Azure si vous souhaitez toomanage ou déplacez des données tooor depuis le stockage Azure pile. Cet article fournit une vue d’ensemble rapide des outils hello disponibles.

outil Hello qui vous convient le mieux varie selon vos besoins :
* [AZCopy](#azcopy)

    Utilitaire de ligne de commande spécifiques au stockage que vous pouvez télécharger les données toocopy à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage.

* [Azure PowerShell](#azure-powershell)

    Interpréteur de ligne de commande basé sur les tâches et langage de génération de scripts conçu spécialement pour l’administration de systèmes.

* [Interface de ligne de commande Azure](#azure-cli)

    Un outil open source, multiplateforme qui fournit un ensemble de commandes pour travailler avec les plateformes d’Azure et Azure pile hello.

* [Explorateur Stockage Microsoft (préversion)](#microsoft-azure-storage-explorer)

    Une application autonome toouse simple avec une interface utilisateur.

En raison de différences de services toohello stockage entre Azure et Azure pile, il peut y avoir certaines exigences de chaque outil décrit dans les sections suivantes de hello. Pour une comparaison entre le stockage Azure et le stockage Azure Stack, consultez [Stockage Azure Stack : Différences et considérations](azure-stack-acs-differences.md).


## <a name="azcopy"></a>AzCopy
AzCopy est un tooand de données toocopy utilitaire de ligne de commande conçu à partir du stockage d’objets Blob Microsoft Azure et de Table à l’aide de commandes simples avec des performances optimales. Vous pouvez copier des données à partir d’un objet tooanother dans votre compte de stockage, ou entre des comptes de stockage. Il existe deux versions de hello AzCopy : AzCopy sur Windows et AzCopy sur Linux. Pile Azure prend uniquement en charge la version de Windows hello. 
 
### <a name="download-and-install-azcopy"></a>Téléchargement et installation d’AzCopy 
[Télécharger](https://aka.ms/azcopyforazurestack) version de Windows hello pris en charge de AzCopy pour la pile de Azure. Vous pouvez installer et utiliser AzCopy sur hello de pile de Azure comme Azure. toolearn, voir [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](../storage/common/storage-use-azcopy.md). 

### <a name="azcopy-command-examples-for-data-transfer"></a>Exemples de commandes AzCopy pour le transfert de données
Hello suivant exemples montrent quelques scénarios classiques pour la copie des données tooand à partir de la pile d’Azure BLOB. toolearn, voir [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](../storage/storage-use-azcopy.md). 
#### <a name="download-all-blobs-toolocal-disk"></a>Téléchargez le disque de toolocal tous les objets BLOB
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a>Téléchargement de fichier unique toovirtual Active 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a>Déplacer des données entre le stockage Azure et Azure Stack 
Le transfert de données asynchrone entre le stockage Azure et Azure Stack n’est pas pris en charge. vous avez besoin de transfert de hello toospecify avec hello `/SyncCopy` option. 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a>Problèmes connus d’AzCopy
* Toute opération AzCopy sur le stockage Fichier n’est pas disponible, car le stockage Fichier n’est pas encore disponible dans Azure Stack.
* Le transfert de données asynchrone entre le stockage Azure et Azure Stack n’est pas pris en charge. Vous pouvez spécifier hello transfert avec hello `/SyncCopy` option toocopy les données de salutation.
* version de Linux Hello de Azcopy n’est pas prise en charge pour le stockage Azure pile. 

## <a name="azure-powershell"></a>Azure PowerShell
Le module Azure PowerShell fournit des applets de commande pour gérer des services sur Azure et Azure Stack. Il s’agit d’un interpréteur en ligne de commande basé sur les tâches et d’un langage de génération de scripts conçu spécialement pour l’administration de systèmes.

### <a name="install-and-configure-powershell-for-azure-stack"></a>Installer et configurer PowerShell pour Azure Stack
Les modules Azure PowerShell compatibles pile Azure sont requis toowork avec la pile de Azure. Pour plus d’informations, consultez [installer PowerShell pour Azure pile](azure-stack-powershell-install.md) et [configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md) toolearn plus.

### <a name="powershell-sample-script-for-azure-stack"></a>Exemple de script PowerShell pour Azure Stack 
Cet exemple suppose que vous avez [installé PowerShell pour Azure Stack](azure-stack-powershell-install.md). Ce script vous permet de configuration de hello conplete et demandez à que votre client Azure pile des informations d’identification tooadd votre environnement de PowerShell compte toohello local. Ensuite, hello script définir la valeur par défaut de hello abonnement Azure, créez un compte de stockage dans Azure, créer un nouveau conteneur dans ce nouveau compte de stockage et télécharger un conteneur de toothat (blob) de fichier image existant. Une fois le script de hello répertorie tous les objets BLOB dans le conteneur, elle crée un nouveau répertoire de destination dans votre ordinateur local et télécharger le fichier d’image hello.

1. Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).  
2. Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).  
3. Ouvrez **Windows PowerShell ISE** et **exécuter en tant qu’administrateur**, cliquez sur **fichier** > **nouveau** toocreate un fichier de script.
4. Copiez le script ci-dessous hello et collez le nouveau fichier de script toohello.
5. Mettre à jour les variables de script hello en fonction de vos paramètres de configuration. 
6. Remarque : ce script a toobe s’exécutent sous la racine hello téléchargé **AzureStack_Tools**. 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with hello name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name tooyour new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name tooyour new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name tooyour new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import hello Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure hello PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set hello GraphEndpointResourceId value
Set-AzureRmEnvironment -Name $ARMEvnName -GraphEndpoint $GraphAudiance

# Login
$TenantID = Get-AzsDirectoryTenantId -AADTenantName $AADTenantName -EnvironmentName $ARMEvnName
Login-AzureRmAccount -EnvironmentName $ARMEvnName -TenantId $TenantID 

# Set a default Azure subscription.
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Create a new Resource Group 
New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

# Create a new storage account.
New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS

# Set a default storage account.
Set-AzureRmCurrentStorageAccount -StorageAccountName $StorageAccountName -ResourceGroupName $ResourceGroupName 

# Create a new container.
New-AzureStorageContainer -Name $ContainerName -Permission Off

# Upload a blob into a container.
Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload

# List all blobs in a container.
Get-AzureStorageBlob -Container $ContainerName

# Download blobs from hello container:
# Get a reference tooa list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create hello destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into hello local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a>Problèmes connus de PowerShell 
Hello actuel compatible Azure PowerShell version du module pour la pile de Azure est 1.2.10. Il est différent de la version la plus récente d’Azure PowerShell hello. Cette différence impacte le fonctionnement des services de stockage :

* format de valeur de retour Hello de `Get-AzureRmStorageAccountKey` dans la version 1.2.10 a deux propriétés : `Key1` et `Key2`, alors que la version de Microsoft Azure actuel hello retourne un tableau contenant toutes les clés de compte hello.
   ```
   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.4, and later versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Value[0]

   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.3.2, and previous versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Key1

   ```
   Pour plus d’informations, consultez [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).

## <a name="azure-cli"></a>Interface de ligne de commande Azure
Hello CLI d’Azure est de Azure en ligne de commande pour la gestion des ressources Azure. Vous pouvez l’installer sur Windows, Linux et macOS et exécutez-le à partir de la ligne de commande hello. 

CLI Azure est optimisé pour gérer et administrer les ressources Azure à partir de la ligne de commande hello et de créer des scripts d’automatisation qui fonctionnent sur hello Azure Resource Manager. Il fournit un grand nombre de hello mêmes fonctions trouvées dans le portail Azure pile hello, y compris l’accès aux données enrichi.

Azure Stack nécessite la version 2.0 d’Azure CLI. Pour plus d’informations sur l’installation et la configuration d’Azure CLI avec Azure Stack, consultez [Installer et configurer Azure Stack CLI](azure-stack-connect-cli.md). Pour plus d’informations sur comment toouse hello Azure CLI 2.0 tooperform plusieurs tâches, utilisation des ressources dans votre compte de stockage de pile d’Azure, consultez [Using hello CLI2.0 Azure avec le stockage Azure](../storage/storage-azure-cli.md)

### <a name="azure-cli-sample-script-for-azure-stack"></a>Exemple de script Azure CLI pour Azure Stack 
Après avoir terminé l’installation du CLI hello et la configuration, vous pouvez essayer hello suivant toowork étapes avec un toointeract de script shell petit exemple avec les ressources de stockage de pile Azure. script de Hello crée d’abord un nouveau conteneur dans votre compte de stockage, puis télécharge un conteneur existant pour le fichier (comme un objet blob) toothat répertorie tous les objets BLOB dans le conteneur de hello et enfin, télécharge destination de tooa hello fichier sur votre ordinateur local que vous spécifiez. Avant d’exécuter ce script, assurez-vous que vous êtes connecté et connexion toohello cible Azure pile. 
1. Ouvrez l’éditeur de texte, puis copier- coller hello précédant le script dans l’éditeur de hello.
2. Mettre à jour tooreflect de variables de script hello vos paramètres de configuration. 
3. Une fois que vous avez mis à jour les variables nécessaires hello, enregistrer le script de hello et quittez l’éditeur. les étapes suivantes Hello supposent que vous avez nommé votre my_storage_sample.sh de script.
4. Marquer le script hello en tant que fichier exécutable, si nécessaire :`chmod +x my_storage_sample.sh`
5. Exécuter le script de hello. Par exemple, dans Bash : `./my_storage_sample.sh`

```bash
#!/bin/bash
# A simple Azure Stack Storage example script

export AZURESTACK_RESOURCE_GROUP=<resource_group_name>
export AZURESTACK_RG_LOCATION="local"
export AZURESTACK_STORAGE_ACCOUNT_NAME=<storage_account_name>
export AZURESTACK_STORAGE_CONTAINER_NAME=<container_name>
export AZURESTACK_STORAGE_BLOB_NAME=<blob_name>
export FILE_TO_UPLOAD=<file_to_upload>
export DESTINATION_FILE=<destination_file>

echo "Creating hello resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating hello storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating hello blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading hello file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing hello blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading hello file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a>Explorateur Microsoft Azure Storage

L’Explorateur Stockage Microsoft Azure est une application autonome de Microsoft. Il vous permet de travail tooeasily avec les données de stockage Azure et Azure pile de stockage sur Windows, Mac OS et Linux. Si vous souhaitez un toomanage facilement les données de votre stockage de pile Azure, envisagez d’utiliser l’Explorateur de stockage Microsoft Azure.

Pour plus d’informations sur la configuration d’Azure Storage Explorer toowork avec la pile d’Azure, consultez [connecter l’Explorateur de stockage tooan abonnement de Azure pile](azure-stack-storage-connect-se.md).

Pour plus d’informations sur l’Explorateur Stockage Microsoft Azure, consultez [Bien démarrer avec l’Explorateur Stockage (préversion)](../vs-azure-tools-storage-manage-with-storage-explorer.md)

## <a name="next-steps"></a>Étapes suivantes
* [Connecter l’Explorateur de stockage tooan Azure pile abonnement](azure-stack-storage-connect-se.md)
* [Bien démarrer avec l’Explorateur Stockage (préversion)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Stockage Azure : Différences et considérations](azure-stack-acs-differences.md)
* [Introduction tooMicrosoft stockage Azure](../storage/common/storage-introduction.md)

