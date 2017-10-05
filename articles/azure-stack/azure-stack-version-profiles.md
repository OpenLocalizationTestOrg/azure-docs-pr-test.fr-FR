---
title: "Utilisation de profils de version des API dans Azure Stack | Microsoft Docs"
description: "En savoir plus sur les profils de version des API dans Azure Stack."
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
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: b70f8a392fdddade31383fc5cc9496cb39d73fd4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a><span data-ttu-id="53378-103">Gérer les profils de version des API dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="53378-103">Manage API version profiles in Azure Stack</span></span>

<span data-ttu-id="53378-104">Les profils de version des API permettent de gérer les différences de version entre Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="53378-104">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="53378-105">Un profil de version d’API est un ensemble de modules PowerShell AzureRM avec des versions d’API spécifiques.</span><span class="sxs-lookup"><span data-stu-id="53378-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="53378-106">Chaque plateforme cloud a un ensemble de profils de version d’API pris en charge.</span><span class="sxs-lookup"><span data-stu-id="53378-106">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="53378-107">Par exemple, Azure Stack prend en charge une version de profil ayant une date spécifique telle que **2017-03-09-profile**, et Azure prend en charge le profil de version d’API **la plus récente**.</span><span class="sxs-lookup"><span data-stu-id="53378-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile.</span></span> <span data-ttu-id="53378-108">Quand vous installez un profil, les modules PowerShell AzureRM qui correspondent au profil spécifié sont installés.</span><span class="sxs-lookup"><span data-stu-id="53378-108">When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.</span></span>

## <a name="install-the-powershell-module-required-to-use-api-version-profiles"></a><span data-ttu-id="53378-109">Installer le module PowerShell nécessaire pour utiliser des profils de version d’API</span><span class="sxs-lookup"><span data-stu-id="53378-109">Install the PowerShell module required to use API version profiles</span></span>

<span data-ttu-id="53378-110">Le module **AzureRM.Bootstrapper** qui est disponible par le biais de PowerShell Gallery fournit des applets de commande PowerShell nécessaires pour utiliser des profils de version d’API.</span><span class="sxs-lookup"><span data-stu-id="53378-110">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span></span> <span data-ttu-id="53378-111">Utilisez l’applet de commande suivante pour installer le module AzureRM.Bootstrapper :</span><span class="sxs-lookup"><span data-stu-id="53378-111">Use the following cmdlet to install the AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
<span data-ttu-id="53378-112">Le module AzureRM.Bootstrapper est en préversion ; les détails et les fonctionnalités sont susceptibles d’être modifiés.</span><span class="sxs-lookup"><span data-stu-id="53378-112">The AzureRM.Bootstrapper module is in preview; details and functionality are subject to change.</span></span> <span data-ttu-id="53378-113">Pour télécharger et installer la version la plus récente de ce module à partir de PowerShell Gallery, exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="53378-113">To download and install the latest version of this module from the PowerShell Gallery, run the following cmdlet:</span></span>

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a><span data-ttu-id="53378-114">Installer un profil</span><span class="sxs-lookup"><span data-stu-id="53378-114">Install a profile</span></span>

<span data-ttu-id="53378-115">Utilisez l’applet de commande **Install-AzureRmProfile** avec le profil de version d’API **2017-03-09-profile** pour installer les modules AzureRM exigés par Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="53378-115">Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="53378-116">Notez que les modules d’administrateur de cloud Azure pile ne sont pas installés avec ce profil de version d’API, et ils doivent être installés séparément comme indiqué dans l’étape 3 de la [installer PowerShell pour Azure pile](azure-stack-powershell-install.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="53378-116">Note that the Azure Stack cloud administrator modules are not installed with this API version profile, and they should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="53378-117">Installer et importer des modules dans un profil</span><span class="sxs-lookup"><span data-stu-id="53378-117">Install and import modules in a profile</span></span>

<span data-ttu-id="53378-118">Utilisez l’applet de commande **Use-AzureRmProfile** pour installer et importer les modules associés à un profil de version d’API.</span><span class="sxs-lookup"><span data-stu-id="53378-118">Use the **Use-AzureRmProfile** cmdlet to install and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="53378-119">Vous pouvez importer un seul profil de version d’API dans une session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53378-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="53378-120">Pour importer un autre profil de version d’API, vous devez ouvrir une nouvelle session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53378-120">To import a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="53378-121">L’applet de commande Use-AzureRMProfile exécute les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="53378-121">The Use-AzureRMProfile cmdlet runs the following tasks:</span></span>  
1. <span data-ttu-id="53378-122">Vérifie si les modules PowerShell associés au profil de version d’API spécifié sont installés dans l’étendue actuelle.</span><span class="sxs-lookup"><span data-stu-id="53378-122">Checks if the PowerShell modules associated with the specified API version profile are installed in the current scope.</span></span>  
2. <span data-ttu-id="53378-123">Télécharge et installe les modules s’ils ne le sont pas déjà.</span><span class="sxs-lookup"><span data-stu-id="53378-123">Downloads and installs the modules if they are not already installed.</span></span>   
3. <span data-ttu-id="53378-124">Importe les modules dans la session PowerShell active.</span><span class="sxs-lookup"><span data-stu-id="53378-124">Imports the modules into the current PowerShell session.</span></span> 

```PowerShell
# Installs and imports the specified API version profile into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports the specified API version profile into the current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="53378-125">Pour installer et importer les modules AzureRM sélectionnés à partir d’un profil de version d’API, exécutez l’applet de commande Use-AzureRMProfile avec le paramètre **Module** :</span><span class="sxs-lookup"><span data-stu-id="53378-125">To install and import selected AzureRM modules from an API version profile, run the Use-AzureRMProfile cmdlet with the **Module** parameter:</span></span>

```PowerShell
# Installs and imports the compute, Storage and Network modules from the specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-the-installed-profiles"></a><span data-ttu-id="53378-126">Obtenir les profils installés</span><span class="sxs-lookup"><span data-stu-id="53378-126">Get the installed profiles</span></span>

<span data-ttu-id="53378-127">Utilisez l’applet de commande **Get-AzureRmProfile** pour obtenir la liste des profils de version d’API disponibles :</span><span class="sxs-lookup"><span data-stu-id="53378-127">Use the **Get-AzureRmProfile** cmdlet to get the list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by the AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists the API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="53378-128">Mettre à jour des profils</span><span class="sxs-lookup"><span data-stu-id="53378-128">Update profiles</span></span>

<span data-ttu-id="53378-129">Utilisez l’applet de commande **Update-AzureRmProfile** pour mettre à jour les modules d’un profil de version d’API vers la version la plus récente des modules disponibles dans PSGallery.</span><span class="sxs-lookup"><span data-stu-id="53378-129">Use the **Update-AzureRmProfile** cmdlet to update the modules in an API version profile to the latest version of modules that are available in the PSGallery.</span></span> <span data-ttu-id="53378-130">Il est recommandé de toujours exécuter l’applet de commande **Update-AzureRmProfile** dans une nouvelle session PowerShell pour éviter les conflits lors de l’importation de modules.</span><span class="sxs-lookup"><span data-stu-id="53378-130">It's recommended to always run the **Update-AzureRmProfile** cmdlet in a new PowerShell session to avoid conflicts when importing modules.</span></span> <span data-ttu-id="53378-131">L’applet de commande Update-AzureRmProfile exécute les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="53378-131">The Update-AzureRmProfile cmdlet runs the following tasks:</span></span>

1. <span data-ttu-id="53378-132">Vérifie si les versions les plus récentes des modules sont installées dans le profil de version d’API donné pour l’étendue actuelle.</span><span class="sxs-lookup"><span data-stu-id="53378-132">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="53378-133">Vous invite à les installer si elles ne le sont pas déjà.</span><span class="sxs-lookup"><span data-stu-id="53378-133">Prompts you to install if they are not already installed.</span></span>  
3. <span data-ttu-id="53378-134">Installe et importe les modules mis à jour dans la session PowerShell active.</span><span class="sxs-lookup"><span data-stu-id="53378-134">Installs and imports the updated modules into the current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="53378-135">Pour supprimer les versions précédemment installées des modules avant d’effectuer la mise à jour vers la version la plus récente disponible, utilisez l’applet de commande Update-AzureRmProfile avec le paramètre **-RemovePreviousVersions** :</span><span class="sxs-lookup"><span data-stu-id="53378-135">To remove the previously installed versions of the modules before updating to the latest available version, use the Update-AzureRmProfile cmdlet along with the **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="53378-136">Cette applet de commande exécute les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="53378-136">This cmdlet runs the following tasks:</span></span>  

1. <span data-ttu-id="53378-137">Vérifie si les versions les plus récentes des modules sont installées dans le profil de version d’API donné pour l’étendue actuelle.</span><span class="sxs-lookup"><span data-stu-id="53378-137">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="53378-138">Supprime du profil de version d’API actuel et de la session PowerShell active les versions antérieures des modules.</span><span class="sxs-lookup"><span data-stu-id="53378-138">Removes the older versions of modules from the current API version profile and in the current PowerShell session.</span></span>  
4. <span data-ttu-id="53378-139">Vous invite à installer la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="53378-139">prompts you to install the latest version.</span></span>  
5. <span data-ttu-id="53378-140">Installe et importe les modules mis à jour dans la session PowerShell active.</span><span class="sxs-lookup"><span data-stu-id="53378-140">Installs and imports the updated modules into the current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="53378-141">Désinstaller des profils</span><span class="sxs-lookup"><span data-stu-id="53378-141">Uninstall profiles</span></span>

<span data-ttu-id="53378-142">Utilisez l’applet de commande **Uninstall-AzureRmProfile** pour désinstaller le profil de version d’API spécifié.</span><span class="sxs-lookup"><span data-stu-id="53378-142">Use the **Uninstall-AzureRmProfile** cmdlet to uninstall the specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="53378-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53378-143">Next steps</span></span>
* [<span data-ttu-id="53378-144">Installer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="53378-144">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="53378-145">Configurer l’environnement PowerShell de l’utilisateur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="53378-145">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
