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
# <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="812d5-103">Installer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="812d5-103">Install PowerShell for Azure Stack</span></span>  

<span data-ttu-id="812d5-104">Les modules Azure PowerShell compatibles pile Azure sont requis toowork avec la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="812d5-104">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="812d5-105">Dans ce guide, nous vous guident hello étapes tooinstall requis PowerShell pour Azure pile.</span><span class="sxs-lookup"><span data-stu-id="812d5-105">In this guide, we walk you through hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="812d5-106">Vous pouvez utiliser les étapes de hello décrits dans cet article hello Kit de développement Azure pile ou d’un client externe basé sur Windows, si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="812d5-106">You can use hello steps described in this article either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="812d5-107">Cet article détaille tooinstall d’instructions PowerShell pour Azure pile.</span><span class="sxs-lookup"><span data-stu-id="812d5-107">This article has detailed instructions tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="812d5-108">Toutefois, si vous souhaitez tooquickly installer et configurez PowerShell, vous pouvez utiliser script hello fourni Bonjour [obtenir en cours d’exécution avec PowerShell](azure-stack-powershell-configure-quickstart.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="812d5-108">However, if you want tooquickly install and configure PowerShell, you can use hello script that is provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

> [!NOTE]
> <span data-ttu-id="812d5-109">Hello suit nécessite PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="812d5-109">hello following steps require PowerShell 5.0.</span></span> <span data-ttu-id="812d5-110">toocheck votre version, l’exécution $PSVersionTable.PSVersion et comparer hello » « version principale.</span><span class="sxs-lookup"><span data-stu-id="812d5-110">toocheck your version, run $PSVersionTable.PSVersion and compare hello "Major" version.</span></span>

<span data-ttu-id="812d5-111">Commandes PowerShell pour Azure pile sont installés via la galerie de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="812d5-111">PowerShell commands for Azure Stack are installed through hello PowerShell gallery.</span></span> <span data-ttu-id="812d5-112">tooregiser hello PSGallery référentiel, ouvrez une session PowerShell avec élévation de privilèges à partir du kit de développement hello ou à partir d’un client externe Windows si vous êtes connecté via VPN et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="812d5-112">tooregiser hello PSGallery repository, open an elevated PowerShell session from hello development kit or from a Windows-based external client if you are connected through VPN and run hello following command:</span></span>

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a><span data-ttu-id="812d5-113">Désinstaller les versions existantes de PowerShell</span><span class="sxs-lookup"><span data-stu-id="812d5-113">Uninstall existing versions of PowerShell</span></span>

<span data-ttu-id="812d5-114">Avant d’installer la version requise de hello, assurez-vous que vous avez désinstallé tous les modules Azure PowerShell existants.</span><span class="sxs-lookup"><span data-stu-id="812d5-114">Before installing hello required version, make sure that you uninstall any existing Azure PowerShell modules.</span></span> <span data-ttu-id="812d5-115">Vous pouvez les désinstaller à l’aide d’une des deux méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="812d5-115">You can uninstall them by using one of hello following two methods:</span></span>

* <span data-ttu-id="812d5-116">toouninstall hello des modules PowerShell existants, connectez-vous de kit de développement toohello ou toohello basé sur Windows des clients externes si vous prévoyez de tooestablish une connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="812d5-116">toouninstall hello existing PowerShell modules, sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="812d5-117">Fermez toutes les sessions de PowerShell actives hello et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="812d5-117">Close all hello active PowerShell sessions and run hello following command:</span></span> 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* <span data-ttu-id="812d5-118">Se connecter dans le kit de développement toohello ou toohello basé sur Windows des clients externes si vous prévoyez de tooestablish une connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="812d5-118">Sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="812d5-119">Supprimez tous les dossiers hello qui commencent par « Azure » à partir de hello `C:\Program Files (x86)\WindowsPowerShell\Modules` et `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` dossiers.</span><span class="sxs-lookup"><span data-stu-id="812d5-119">Delete all hello folders that start with "Azure" from hello `C:\Program Files (x86)\WindowsPowerShell\Modules` and `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` folders.</span></span> <span data-ttu-id="812d5-120">Suppression de ces dossiers supprime tous les modules PowerShell existants à partir de hello « AzureStackAdmin » et les étendues de l’utilisateur « globaux ».</span><span class="sxs-lookup"><span data-stu-id="812d5-120">Deleting these folders removes any existing PowerShell modules from hello "AzureStackAdmin" and "global" user scopes.</span></span> 

<span data-ttu-id="812d5-121">Hello sections suivantes décrivent hello étapes tooinstall requis PowerShell pour Azure pile.</span><span class="sxs-lookup"><span data-stu-id="812d5-121">hello following sections describe hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="812d5-122">Vous pouvez installer PowerShell sur Azure Stack exploité dans un scénario connecté, partiellement connecté ou déconnecté.</span><span class="sxs-lookup"><span data-stu-id="812d5-122">PowerShell can be installed on Azure Stack that is operated in connected, partially connected, or in a disconnected scenario.</span></span> 

## <a name="install-powershell-in-a-connected-scenario"></a><span data-ttu-id="812d5-123">Installer PowerShell dans un scénario connecté</span><span class="sxs-lookup"><span data-stu-id="812d5-123">Install PowerShell in a connected scenario</span></span> 

<span data-ttu-id="812d5-124">Les modules AzureRM compatibles avec Azure Stack sont installés par le biais de profils de version d’API.</span><span class="sxs-lookup"><span data-stu-id="812d5-124">Azure Stack compatible AzureRM modules are installed through API version profiles.</span></span> <span data-ttu-id="812d5-125">Pile Azure nécessite hello **2017-03-09-profil** profil de version de l’API, qui est disponible en installant le module de AzureRM.Bootstrapper hello.</span><span class="sxs-lookup"><span data-stu-id="812d5-125">Azure Stack requires hello **2017-03-09-profile** API version profile, which is available by installing hello AzureRM.Bootstrapper module.</span></span> <span data-ttu-id="812d5-126">toolearn sur les profils de version d’API et applets de commande hello fournies par celles-ci, consultez toohello [gérer les profils de version d’API](azure-stack-version-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="812d5-126">toolearn about API version profiles and hello cmdlets provided by them, refer toohello [manage API version profiles](azure-stack-version-profiles.md).</span></span> <span data-ttu-id="812d5-127">Dans les modules plus toohello Azure Resource Manager, vous devez également installer des modules de pile spécifique Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="812d5-127">In addition toohello AzureRM modules, you should also install hello Azure Stack-specific PowerShell modules.</span></span> <span data-ttu-id="812d5-128">Hello suivant tooinstall de script PowerShell, exécutez ces modules sur votre station de travail de développement :</span><span class="sxs-lookup"><span data-stu-id="812d5-128">Run hello following PowerShell script tooinstall these modules on your development workstation:</span></span>

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

<span data-ttu-id="812d5-129">tooconfirm hello, réexécutez l’installation Bonjour de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="812d5-129">tooconfirm hello installation, run hello following command:</span></span>

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  <span data-ttu-id="812d5-130">Si l’installation de hello est réussie, hello Azure Resource Manager et les modules AzureStack sont affichés dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="812d5-130">If hello installation is successful, hello AzureRM and AzureStack modules are displayed in hello output.</span></span>

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a><span data-ttu-id="812d5-131">Installer PowerShell dans un scénario déconnecté ou partiellement connecté</span><span class="sxs-lookup"><span data-stu-id="812d5-131">Install PowerShell in a disconnected or in a partially connected scenario</span></span>

<span data-ttu-id="812d5-132">Dans un scénario déconnecté, vous devez d’abord télécharger hello PowerShell modules tooa ordinateur qui possède une connexion internet et les transférer toohello Kit de développement de pile Azure pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="812d5-132">In a disconnected scenario, you must first download hello PowerShell modules tooa machine that has internet connectivity, and then transfer them toohello Azure Stack Development Kit for installation.</span></span>

1. <span data-ttu-id="812d5-133">La connexion tooa ordinateur sur lequel vous avez une connexion internet et que vous utilisez hello suivant hello toodownload de script Azure Resource Manager, et les packages AzureStack sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="812d5-133">Sign in tooa computer where you have internet connectivity and use hello following script toodownload hello AzureRM, and AzureStack packages onto your local computer:</span></span>

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

2. <span data-ttu-id="812d5-134">Hello de copie de packages téléchargés sur un périphérique USB tooa.</span><span class="sxs-lookup"><span data-stu-id="812d5-134">Copy hello downloaded packages over tooa USB device.</span></span>

3. <span data-ttu-id="812d5-135">Connectez-vous au kit de développement toohello et copier les packages de hello d’emplacement de tooa l’appareil USB hello sur le kit de développement hello.</span><span class="sxs-lookup"><span data-stu-id="812d5-135">Sign in toohello development kit and copy hello packages from hello USB device tooa location on hello development kit.</span></span> 

4. <span data-ttu-id="812d5-136">Maintenant, vous devez inscrire cet emplacement en tant que référentiel par défaut de hello et installer hello Azure Resource Manager et les modules AzureStack à partir de ce référentiel :</span><span class="sxs-lookup"><span data-stu-id="812d5-136">Now you must register this location as hello default repository and install hello AzureRM and AzureStack modules from this repository:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="812d5-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="812d5-137">Next steps</span></span>

* [<span data-ttu-id="812d5-138">Télécharger les outils Azure Stack à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="812d5-138">Download Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)
* [<span data-ttu-id="812d5-139">Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="812d5-139">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
* [<span data-ttu-id="812d5-140">Configurer l’environnement de l’opérateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="812d5-140">Configure hello Azure Stack operator's PowerShell environment</span></span>](azure-stack-powershell-configure-admin.md) 
* [<span data-ttu-id="812d5-141">Gérer les profils de version des API dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="812d5-141">Manage API version profiles in Azure Stack</span></span>](azure-stack-version-profiles.md)  
