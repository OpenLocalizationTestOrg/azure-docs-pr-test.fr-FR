---
title: "aaaDesired Configuration d’état pour une vue d’ensemble de Azure | Documents Microsoft"
description: "Vue d’ensemble pour l’utilisation du Gestionnaire d’extensions Microsoft Azure hello pour la Configuration d’état souhaité PowerShell. Cela inclut les conditions préalables, l’architecture, les applets de commande, etc."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Gestionnaire d’extensions Azure DSC introduction toohello
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello Agent de machine virtuelle Azure et les Extensions associées font partie de hello Services d’Infrastructure Microsoft Azure. Extensions de machine virtuelle sont des composants logiciels étendant les fonctionnalités de machine virtuelle de hello et simplifient plusieurs opérations de gestion de machine virtuelle. Par exemple, hello extension VMAccess peut être utilisé tooreset un mot de passe administrateur ou hello Script personnalisé peut être utilisé tooexecute un script sur hello machine virtuelle.

Cet article présente hello Extension de Configuration d’état souhaité (DSC) PowerShell pour les machines virtuelles Azure dans le cadre de hello Kit de développement logiciel Azure PowerShell. Vous pouvez utiliser les nouvelles applets de commande tooupload et appliquer une configuration DSC PowerShell sur une machine virtuelle de Azure activée avec hello extension PowerShell DSC. appels d’extension PowerShell DSC Hello en hello tooenact de DSC PowerShell a reçu la configuration DSC sur hello machine virtuelle. Cette fonctionnalité est également disponible via hello portail Azure.

## <a name="prerequisites"></a>Composants requis
**Ordinateur local** toointeract avec hello extension de machine virtuelle Azure, vous devez toouse soit hello portail Azure hello du Kit de développement logiciel Azure PowerShell. 

**L’Agent invité** hello machine virtuelle Azure qui est configuré par configuration de hello DSC doit toobe un système d’exploitation qui prend en charge de Windows Management Framework (WMF) 4.0 ou 5.0. la liste complète des versions de système d’exploitation pris en charge Hello trouverez hello [historique de Version d’Extension DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Termes et concepts
Ce guide suppose que vous êtes familiarisé avec hello suivant concepts :

Configuration : document de configuration DSC. 

Nœud : cible d’une configuration DSC. Dans ce document, « nœud » fait toujours référence tooan machine virtuelle Azure.

Données de configuration : fichier .psd1 contenant les données d’environnement d’une configuration.

## <a name="architectural-overview"></a>Présentation de l’architecture
Hello extensions Azure DSC utilise toodeliver de framework hello Agent de machine virtuelle Azure, les promulgue et sur les configurations DSC en cours d’exécution sur des machines virtuelles Azure. Hello extension DSC attend un fichier .zip contenant au moins un document de configuration, et un ensemble de paramètres fournis par le biais hello Kit de développement logiciel Azure PowerShell ou hello portail Azure.

Lors de l’extension de hello est appelée pour hello la première fois, il exécute un processus d’installation. Ce processus installe une version de hello Windows Management Framework (WMF) à l’aide de hello suivant logique :

1. Si hello système d’exploitation de la machine virtuelle Azure est Windows Server 2016, aucune action n’est effectuée. Windows Server 2016 a déjà la version la plus récente de PowerShell installée hello.
2. Si hello `wmfVersion` propriété est spécifiée, cette version de hello WMF est installée, sauf si elle est incompatible avec du système d’exploitation la machine virtuelle hello.
3. Si aucun `wmfVersion` propriété est spécifiée, hello version plus récente applicable de hello WMF est installée.

Installation de hello WMF requiert un redémarrage. Après le redémarrage, extension de hello télécharge le fichier .zip de hello spécifié dans hello `modulesUrl` propriété. Si cet emplacement est dans le stockage blob Azure, un jeton SAS peut être spécifié dans hello `sasToken` propriété tooaccess hello fichier. Une fois hello .zip est téléchargé et décompressé, hello fonction de configuration définie dans `configurationFunction` est exécuté fichier MOF de hello toogenerate. extension de Hello exécute ensuite `Start-DscConfiguration -Force` hello généré dans le fichier MOF. extension de Hello capture la sortie et l’écrit dans toohello Azure état du canal. À ce stade, hello DSC de façon gère l’analyse et la correction comme d’habitude. 

## <a name="powershell-cmdlets"></a>Applets de commande PowerShell
Applets de commande PowerShell peut être utilisé avec le Gestionnaire de ressources Azure ou hello toopackage de modèle de déploiement classique, publier et surveiller les déploiements d’extension DSC. Hello applets de commande suivantes sont des modules de déploiement classique de hello, mais « Azure » peut être remplacé par modèle de « AzureRm » toouse hello Azure Resource Manager. Par exemple, `Publish-AzureVMDscConfiguration` utilise hello modèle de déploiement classique, où `Publish-AzureRmVMDscConfiguration` utilise Azure Resource Manager. 

`Publish-AzureVMDscConfiguration`récupère dans un fichier de configuration, l’analyse pour les ressources DSC dépendantes et crée un fichier .zip contenant hello et configuration de hello de tooenact nécessaires de ressources DSC. Il peut également créer le package hello localement à l’aide de hello `-ConfigurationArchivePath` paramètre. Sinon, elle publie le stockage d’objets blob hello .zip fichier tooAzure et sécurise à l’aide d’un jeton SAS.

fichier .zip de Hello créé par cette applet de commande a un script de configuration .ps1 hello au niveau racine de hello du dossier d’archive hello. Les ressources ont un dossier de module hello placé dans le dossier d’archive hello. 

`Set-AzureVMDscExtension`injecte les paramètres de hello requis par hello extension PowerShell DSC dans un objet de configuration d’ordinateur virtuel. Dans le modèle de déploiement classique de hello, modifications de machine virtuelle hello doivent être appliqué tooan machine virtuelle Azure avec `Update-AzureVM`. 

`Get-AzureVMDscExtension`Récupère l’état de l’extension DSC hello d’une machine virtuelle particulière. 

`Get-AzureVMDscExtensionStatus`Récupère l’état hello de configuration DSC de hello imposée par le Gestionnaire d’extensions DSC hello. Cette action peut être effectuée sur une seule machine virtuelle ou sur un groupe de machines virtuelles.

`Remove-AzureVMDscExtension`Supprime le Gestionnaire d’extensions hello à partir d’un ordinateur virtuel spécifié. Cette applet de commande **pas** supprimer la configuration de hello, désinstaller hello WMF ou modifier les paramètres de hello appliqué sur l’ordinateur virtuel de hello. Il supprime uniquement le Gestionnaire d’extensions hello. 

**Principales différences dans les applets de commande ASM et Azure Resource Manager**

* Les applets de commande Azure Resource Manager sont synchrones. alors que les applets de commande ARM sont asynchrones.
* Les éléments ResourceGroupName, VMName, ArchiveStorageAccountName, Version et Location sont tous des paramètres requis dans Azure Resource Manager.
* L’élément ArchiveResourceGroupName est un nouveau paramètre facultatif pour Azure Resource Manager. Vous pouvez spécifier ce paramètre lorsque votre compte de stockage appartient le groupe de ressources différent tooa que hello une où la machine virtuelle de hello est créé.
* L’élément ConfigurationArchive est appelé ArchiveBlobName dans Azure Resource Manager.
* L’élément ContainerName est appelé ArchiveContainerName dans Azure Resource Manager.
* L’élément StorageEndpointSuffix est appelé ArchiveStorageEndpointSuffix dans Azure Resource Manager.
* commutateur de mise à jour automatique Hello a été ajouté tooAzure tooenable du Gestionnaire de ressources automatique de mise à jour de hello Gestionnaire toohello dernière version de l’extension en tant qu’et lorsqu’il est disponible. Notez que ce paramètre a toocause potentielle de hello redémarre sur hello VM lorsqu’une nouvelle version de hello que WMF est libérée. 

## <a name="azure-portal-functionality"></a>Fonctionnalités du portail Azure
Parcourir tooa machine virtuelle. Sous Paramètres -> Général, cliquez sur Extensions. Un volet est créé. Cliquez sur « Ajouter » et sélectionnez PowerShell DSC.

portail de Hello requiert une entrée.
**Script ou modules de configuration**: ce champ est obligatoire. Nécessite un fichier .ps1 contenant un script de configuration ou un fichier .zip avec un script de configuration .ps1 à racine de hello et toutes les ressources dépendantes dans des dossiers de module dans hello .zip. Il peut être créé par hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` applet de commande inclus dans hello Kit de développement logiciel Azure PowerShell. fichier .zip de Hello est téléchargé dans votre stockage d’objets blob utilisateur sécurisé par un jeton SAP. 

**Fichier PSD1 de données de configuration**: ce champ est facultatif. Si votre configuration nécessite un fichier de données de configuration dans .psd1, utilisez cette tooselect champ il puis chargez-le de stockage d’objets blob utilisateur tooyour, où il est sécurisé par un jeton SAP. 

**Nom de configuration qualifié du module**: les fichiers .ps1 peuvent avoir plusieurs fonctions de configuration. Entrez les nom hello de hello configuration .ps1 script de suivi d’un '\' et le nom de hello de fonction de configuration hello. Par exemple, si votre script .ps1 a hello nom « configuration.ps1 », et la configuration de hello est « IisInstall », entrez :`configuration.ps1\IisInstall`

**Arguments de la configuration**: si la fonction de configuration hello accepte des arguments, les entrer ici au format de hello `argumentName1=value1,argumentName2=value2`. Il s’agit d’un format d’argument de configuration différent de celui qui est accepté via les applets de commande PowerShell ou les modèles Resource Manager. 

## <a name="getting-started"></a>Prise en main
Hello extensions Azure DSC prend dans les documents de configuration DSC et les applique sur les machines virtuelles Azure. Voici un exemple simple de configuration. Enregistrez-le en local, sous le nom « IisInstall.ps1 » :

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

Hello suivant les étapes sur place hello IisInstall.ps1 script de hello spécifié de machine virtuelle, exécuter la configuration de hello et rapport sur l’état.
###<a name="classic-model"></a>Modèle classique
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Modèle Azure Resource Manager

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Journalisation
Les journaux sont placés dans le répertoire suivant :

C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[numéro de version]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur PowerShell DSC, [visitez le centre de documentation PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Examinez hello [modèle Azure Resource Manager pour l’extension de hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Vous pouvez gérer avec PowerShell DSC, des fonctionnalités supplémentaires toofind [parcourir la galerie PowerShell de hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) pour plus de ressources DSC.

Pour plus d’informations sur le passage de paramètres sensibles dans des configurations, consultez [gérer les informations d’identification en toute sécurité avec le Gestionnaire d’extensions hello DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

