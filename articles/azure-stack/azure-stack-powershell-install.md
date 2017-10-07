---
title: aaaInstall PowerShell pour Azure pile | Documents Microsoft
description: "Découvrez comment tooinstall PowerShell pour Azure pile."
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
ms.openlocfilehash: 60995af2168348638e2513ab941a4125ca5c624a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-powershell-for-azure-stack"></a>Installer PowerShell pour Azure Stack  

Les modules Azure PowerShell compatibles pile Azure sont requis toowork avec la pile de Azure. Dans ce guide, nous vous guident hello étapes tooinstall requis PowerShell pour Azure pile. Vous pouvez utiliser les étapes de hello décrits dans cet article hello Kit de développement Azure pile ou d’un client externe basé sur Windows, si vous êtes connecté via VPN.

Cet article détaille tooinstall d’instructions PowerShell pour Azure pile. Toutefois, si vous souhaitez tooquickly installer et configurez PowerShell, vous pouvez utiliser script hello fourni Bonjour [obtenir en cours d’exécution avec PowerShell](azure-stack-powershell-configure-quickstart.md) rubrique. 

> [!NOTE]
> Hello suit nécessite PowerShell 5.0. toocheck votre version, l’exécution $PSVersionTable.PSVersion et comparer hello » « version principale.

Commandes PowerShell pour Azure pile sont installés via la galerie de PowerShell hello. tooregiser hello PSGallery référentiel, ouvrez une session PowerShell avec élévation de privilèges à partir du kit de développement hello ou à partir d’un client externe Windows si vous êtes connecté via VPN et exécutez hello de commande suivante :

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a>Désinstaller les versions existantes de PowerShell

Avant d’installer la version requise de hello, assurez-vous que vous avez désinstallé tous les modules Azure PowerShell existants. Vous pouvez les désinstaller à l’aide d’une des deux méthodes suivantes de hello :

* toouninstall hello des modules PowerShell existants, connectez-vous de kit de développement toohello ou toohello basé sur Windows des clients externes si vous prévoyez de tooestablish une connexion VPN. Fermez toutes les sessions de PowerShell actives hello et exécution hello commande suivante : 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* Se connecter dans le kit de développement toohello ou toohello basé sur Windows des clients externes si vous prévoyez de tooestablish une connexion VPN. Supprimez tous les dossiers hello qui commencent par « Azure » à partir de hello `C:\Program Files (x86)\WindowsPowerShell\Modules` et `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` dossiers. Suppression de ces dossiers supprime tous les modules PowerShell existants à partir de hello « AzureStackAdmin » et les étendues de l’utilisateur « globaux ». 

Hello sections suivantes décrivent hello étapes tooinstall requis PowerShell pour Azure pile. Vous pouvez installer PowerShell sur Azure Stack exploité dans un scénario connecté, partiellement connecté ou déconnecté. 

## <a name="install-powershell-in-a-connected-scenario"></a>Installer PowerShell dans un scénario connecté 

Les modules AzureRM compatibles avec Azure Stack sont installés par le biais de profils de version d’API. Pile Azure nécessite hello **2017-03-09-profil** profil de version de l’API, qui est disponible en installant le module de AzureRM.Bootstrapper hello. toolearn sur les profils de version d’API et applets de commande hello fournies par celles-ci, consultez toohello [gérer les profils de version d’API](azure-stack-version-profiles.md). Dans les modules plus toohello Azure Resource Manager, vous devez également installer des modules de pile spécifique Azure PowerShell hello. Hello suivant tooinstall de script PowerShell, exécutez ces modules sur votre station de travail de développement :

  ```powershell
  # Install hello AzureRM.Bootstrapper module. Select Yes when prompted tooinstall NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import hello API Version Profile required by Azure Stack into hello current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.10
  ```

tooconfirm hello, réexécutez l’installation Bonjour de commande suivante :

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  Si l’installation de hello est réussie, hello Azure Resource Manager et les modules AzureStack sont affichés dans la sortie de hello.

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a>Installer PowerShell dans un scénario déconnecté ou partiellement connecté

Dans un scénario déconnecté, vous devez d’abord télécharger hello PowerShell modules tooa ordinateur qui possède une connexion internet et les transférer toohello Kit de développement de pile Azure pour l’installation.

1. La connexion tooa ordinateur sur lequel vous avez une connexion internet et que vous utilisez hello suivant hello toodownload de script Azure Resource Manager, et les packages AzureStack sur votre ordinateur local :

   ```powershell
   $Path = "<Path that is used toosave hello packages>"

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

2. Hello de copie de packages téléchargés sur un périphérique USB tooa.

3. Connectez-vous au kit de développement toohello et copier les packages de hello d’emplacement de tooa l’appareil USB hello sur le kit de développement hello. 

4. Maintenant, vous devez inscrire cet emplacement en tant que référentiel par défaut de hello et installer hello Azure Resource Manager et les modules AzureStack à partir de ce référentiel :

   ```powershell
   $SourceLocation = "<Location on hello development kit that contains hello PowerShell packages>"
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
* [Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md)  
* [Configurer l’environnement de l’opérateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-admin.md) 
* [Gérer les profils de version des API dans Azure Stack](azure-stack-version-profiles.md)  
