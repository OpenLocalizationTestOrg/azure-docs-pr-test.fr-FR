---
title: Installer PowerShell pour Azure Stack | Microsoft Docs
description: "Découvrez comment installer PowerShell pour Azure Stack."
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
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: a3b25dd6d7b9ba7a3040dee3196ec25463fe85ef
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="install-powershell-for-azure-stack"></a>Installer PowerShell pour Azure Stack  

Des modules Azure PowerShell compatibles avec Azure Stack sont nécessaires pour utiliser Azure Stack. Dans ce guide, vous allez découvrir les étapes nécessaires à l’installation de PowerShell pour Azure Stack. Vous pouvez effectuer les étapes décrites dans cet article à partir du Kit de développement Azure Stack ou à partir d’un client externe Windows si vous êtes connecté par le biais d’un VPN.

Cet article contient des instructions détaillées sur l’installation de PowerShell pour Azure Stack. Toutefois, si vous souhaitez installer et configurer rapidement PowerShell, vous pouvez utiliser le script fourni dans la rubrique « Devenir rapidement opérationnel avec PowerShell ». 

> [!NOTE]
> Les étapes suivantes nécessitent PowerShell 5.0. Pour vérifier votre version, exécutez $PSVersionTable.PSVersion et comparez la version « Major ».

Les commandes PowerShell pour Azure Stack sont installées par le biais de PowerShell Gallery. Pour inscrire le dépôt PSGallery, ouvrez une session PowerShell avec élévation de privilèges à partir du Kit de développement, ou d’un client externe Windows si vous êtes connecté par le biais d’un réseau privé virtuel, et exécutez la commande suivante :

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a>Désinstaller les versions existantes de PowerShell

Avant d’installer la version requise, vérifiez que vous avez désinstallé tous les modules Azure PowerShell existants. Vous pouvez les désinstaller en appliquant l’une des deux méthodes suivantes :

* Pour désinstaller les modules PowerShell existants, connectez-vous au Kit de développement, ou au client externe Windows si vous prévoyez d’établir une connexion VPN. Fermez toutes les sessions PowerShell actives et exécutez la commande suivante : 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* Connectez-vous au Kit de développement, ou au client externe Windows si vous prévoyez d’établir une connexion VPN. Supprimez des dossiers `C:\Program Files (x86)\WindowsPowerShell\Modules` et `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` tous les dossiers qui commencent par « Azure ». La suppression de ces dossiers supprime tous les modules PowerShell existants des portées utilisateur « global » et « AzureStackAdmin ». 

Les sections suivantes décrivent les étapes nécessaires pour installer PowerShell pour Azure Stack. Vous pouvez installer PowerShell sur Azure Stack exploité dans un scénario connecté, partiellement connecté ou déconnecté. 

## <a name="install-powershell-in-a-connected-scenario"></a>Installer PowerShell dans un scénario connecté 

Les modules AzureRM compatibles avec Azure Stack sont installés par le biais de profils de version d’API. Azure Stack nécessite la version d’API **2017-03-09-profile**, qui est disponible en installant le module AzureRM.Bootstrapper. Pour en savoir plus sur les profils de version d’API et les applets de commande fournies par ces derniers, consultez la page [Gérer les profils de version d’API](azure-stack-version-profiles.md). Outre les modules AzureRM, vous devez également installer les modules Azure PowerShell propres à Azure Stack. Exécutez le script PowerShell suivant pour installer ces modules sur votre station de travail de développement :

  ```powershell
  # Install the AzureRM.Bootstrapper module. Select Yes when prompted to install NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import the API Version Profile required by Azure Stack into the current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.10
  ```

Pour confirmer l’installation, exécutez la commande suivante :

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  Si l’installation réussit, les modules AzureRM et AzureStack sont affichés dans la sortie.

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a>Installer PowerShell dans un scénario déconnecté ou partiellement connecté

Dans un scénario déconnecté, vous devez tout d’abord télécharger les modules PowerShell sur un ordinateur qui dispose d’une connexion Internet, puis les transférer vers le Kit de développement Azure Stack pour l’installation.

1. Connectez-vous à un ordinateur où vous avez une connexion Internet et utilisez le script suivant pour télécharger les packages AzureRM et AzureStack sur votre ordinateur local :

   ```powershell
   $Path = "<Path that is used to save the packages>"

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureRM `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureStack `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10 
   ```

2. Copiez les packages téléchargés vers un périphérique USB.

3. Connectez-vous au Kit de développement et copiez les packages du périphérique USB vers un emplacement sur le Kit de développement. 

4. Vous devez maintenant inscrire cet emplacement comme dépôt par défaut et installer les modules AzureRM et AzureStack à partir de ce dépôt :

   ```powershell
   $SourceLocation = "<Location on the development kit that contains the PowerShell packages>"
   $RepoName = "MyNuGetSource"

   Register-PSRepository `
     -Name $RepoName `
     -SourceLocation $SourceLocation `
     -InstallationPolicy Trusted

   ```powershell
   Install-Module AzureRM `
     -Repository $RepoName

   Install-Module AzureStack `
     -Repository $RepoName 
   ```

## <a name="next-steps"></a>Étapes suivantes

* [Télécharger les outils Azure Stack à partir de GitHub](azure-stack-powershell-download.md)
* [Configurez l’environnement PowerShell de l’utilisateur Azure Stack.](azure-stack-powershell-configure-user.md)  
* [Gérer les profils de version des API dans Azure Stack](azure-stack-version-profiles.md)  
