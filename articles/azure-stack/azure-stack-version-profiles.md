---
title: profils de version aaaUsing API dans la pile de Azure | Documents Microsoft
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
ms.openlocfilehash: cb54a683054f08fd123bcb6245d88aaa30c29882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a><span data-ttu-id="7571b-103">Gérer les profils de version des API dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7571b-103">Manage API version profiles in Azure Stack</span></span>

<span data-ttu-id="7571b-104">Profils de version d’API fournissent une toomanage de façon les différences de version entre Azure et de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="7571b-104">API version profiles provide a way toomanage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="7571b-105">Un profil de version d’API est un ensemble de modules PowerShell AzureRM avec des versions d’API spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7571b-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="7571b-106">Chaque plateforme cloud a un ensemble de profils de version d’API pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7571b-106">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="7571b-107">Par exemple, Azure pile prend en charge une version de profil ayant une date spécifique tel que **2017-03-09-profil**et prend en charge Azure hello **dernière** profil de version d’API.</span><span class="sxs-lookup"><span data-stu-id="7571b-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports hello **latest** API version profile.</span></span> <span data-ttu-id="7571b-108">Lorsque vous installez un profil, hello modules AzureRM PowerShell qui correspondent toohello spécifié profil sont installés.</span><span class="sxs-lookup"><span data-stu-id="7571b-108">When you install a profile, hello AzureRM PowerShell modules that correspond toohello specified profile are installed.</span></span>

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a><span data-ttu-id="7571b-109">Installer des profils de version hello PowerShell module requis toouse API</span><span class="sxs-lookup"><span data-stu-id="7571b-109">Install hello PowerShell module required toouse API version profiles</span></span>

<span data-ttu-id="7571b-110">Hello **AzureRM.Bootstrapper** module qui est disponible via hello PowerShell Gallery fournit les applets de commande PowerShell qui sont requis toowork avec des profils de version d’API.</span><span class="sxs-lookup"><span data-stu-id="7571b-110">hello **AzureRM.Bootstrapper** module that is available through hello PowerShell Gallery provides PowerShell cmdlets that are required toowork with API version profiles.</span></span> <span data-ttu-id="7571b-111">Utilisez hello suivant du module de AzureRM.Bootstrapper hello applet de commande tooinstall :</span><span class="sxs-lookup"><span data-stu-id="7571b-111">Use hello following cmdlet tooinstall hello AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
<span data-ttu-id="7571b-112">module de AzureRM.Bootstrapper Hello est en version préliminaire ; détails et les fonctionnalités sont toochange de sujet.</span><span class="sxs-lookup"><span data-stu-id="7571b-112">hello AzureRM.Bootstrapper module is in preview; details and functionality are subject toochange.</span></span> <span data-ttu-id="7571b-113">toodownload et installez hello version la plus récente de ce module de hello PowerShell Gallery, exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="7571b-113">toodownload and install hello latest version of this module from hello PowerShell Gallery, run hello following cmdlet:</span></span>

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a><span data-ttu-id="7571b-114">Installer un profil</span><span class="sxs-lookup"><span data-stu-id="7571b-114">Install a profile</span></span>

<span data-ttu-id="7571b-115">Hello d’utilisation **Install-AzureRmProfile** applet de commande avec hello **2017-03-09-profil** API version profil tooinstall hello Azure Resource Manager modules requis par la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="7571b-115">Use hello **Install-AzureRmProfile** cmdlet with hello **2017-03-09-profile** API version profile tooinstall hello AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="7571b-116">Notez que les modules hello Azure pile cloud administrateur ne sont pas installés avec ce profil de la version API, et ils doivent être installés séparément comme spécifié dans hello étape 3 de hello [installer PowerShell pour Azure pile](azure-stack-powershell-install.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="7571b-116">Note that hello Azure Stack cloud administrator modules are not installed with this API version profile, and they should be installed separately as specified in hello Step 3 of hello [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="7571b-117">Installer et importer des modules dans un profil</span><span class="sxs-lookup"><span data-stu-id="7571b-117">Install and import modules in a profile</span></span>

<span data-ttu-id="7571b-118">Hello d’utilisation **AzureRmProfile-utilisez** applet de commande tooinstall et importer les modules qui sont associés à un profil de la version API.</span><span class="sxs-lookup"><span data-stu-id="7571b-118">Use hello **Use-AzureRmProfile** cmdlet tooinstall and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="7571b-119">Vous pouvez importer un seul profil de version d’API dans une session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7571b-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="7571b-120">profil de version tooimport une autre API, vous devez ouvrir une nouvelle session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7571b-120">tooimport a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="7571b-121">applet de commande Hello utilisation-AzureRMProfile exécute hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7571b-121">hello Use-AzureRMProfile cmdlet runs hello following tasks:</span></span>  
1. <span data-ttu-id="7571b-122">Vérifie si les modules PowerShell hello associés hello spécifié le profil de version d’API est installés dans l’étendue actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-122">Checks if hello PowerShell modules associated with hello specified API version profile are installed in hello current scope.</span></span>  
2. <span data-ttu-id="7571b-123">Télécharge et installe les modules hello s’ils ne sont pas déjà installés.</span><span class="sxs-lookup"><span data-stu-id="7571b-123">Downloads and installs hello modules if they are not already installed.</span></span>   
3. <span data-ttu-id="7571b-124">Importations hello modules dans la session PowerShell en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-124">Imports hello modules into hello current PowerShell session.</span></span> 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="7571b-125">tooinstall et importation sélectionné les modules Azure Resource Manager à partir d’un profil de version d’API, exécuter l’applet de commande hello AzureRMProfile à l’utilisation par hello **Module** paramètre :</span><span class="sxs-lookup"><span data-stu-id="7571b-125">tooinstall and import selected AzureRM modules from an API version profile, run hello Use-AzureRMProfile cmdlet with hello **Module** parameter:</span></span>

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a><span data-ttu-id="7571b-126">Obtenir les profils de hello installé</span><span class="sxs-lookup"><span data-stu-id="7571b-126">Get hello installed profiles</span></span>

<span data-ttu-id="7571b-127">Hello d’utilisation **Get-AzureRmProfile** applet de commande tooget hello liste API version profils disponibles :</span><span class="sxs-lookup"><span data-stu-id="7571b-127">Use hello **Get-AzureRmProfile** cmdlet tooget hello list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="7571b-128">Mettre à jour des profils</span><span class="sxs-lookup"><span data-stu-id="7571b-128">Update profiles</span></span>

<span data-ttu-id="7571b-129">Hello d’utilisation **AzureRmProfile de mise à jour** modules de hello tooupdate applet de commande dans une version profil toohello dernière version de l’API des modules qui sont disponibles dans hello PSGallery.</span><span class="sxs-lookup"><span data-stu-id="7571b-129">Use hello **Update-AzureRmProfile** cmdlet tooupdate hello modules in an API version profile toohello latest version of modules that are available in hello PSGallery.</span></span> <span data-ttu-id="7571b-130">Il est recommandé de tooalways exécuter hello **AzureRmProfile de mise à jour** applet de commande dans une nouvelle tooavoid de session PowerShell est en conflit lors de l’importation de modules.</span><span class="sxs-lookup"><span data-stu-id="7571b-130">It's recommended tooalways run hello **Update-AzureRmProfile** cmdlet in a new PowerShell session tooavoid conflicts when importing modules.</span></span> <span data-ttu-id="7571b-131">applet de commande Hello AzureRmProfile de mise à jour s’exécute hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7571b-131">hello Update-AzureRmProfile cmdlet runs hello following tasks:</span></span>

1. <span data-ttu-id="7571b-132">Vérifie si hello dernières versions des modules sont installées dans hello donnée de profil de version d’API pour l’étendue actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-132">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="7571b-133">Vous invite tooinstall s’ils ne sont pas déjà installés.</span><span class="sxs-lookup"><span data-stu-id="7571b-133">Prompts you tooinstall if they are not already installed.</span></span>  
3. <span data-ttu-id="7571b-134">Installe et importe les modules de hello mis à jour dans la session PowerShell en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-134">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="7571b-135">tooremove les versions hello précédemment installé des modules hello avant la mise à jour toohello version la plus récente, utiliser l’applet de commande hello AzureRmProfile de mise à jour en même temps que hello **- RemovePreviousVersions** paramètre :</span><span class="sxs-lookup"><span data-stu-id="7571b-135">tooremove hello previously installed versions of hello modules before updating toohello latest available version, use hello Update-AzureRmProfile cmdlet along with hello **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="7571b-136">Cette applet de commande exécute hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7571b-136">This cmdlet runs hello following tasks:</span></span>  

1. <span data-ttu-id="7571b-137">Vérifie si hello dernières versions des modules sont installées dans hello donnée de profil de version d’API pour l’étendue actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-137">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="7571b-138">Supprime hello anciennes versions de modules à partir du profil de version API hello actuel et dans la session PowerShell en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-138">Removes hello older versions of modules from hello current API version profile and in hello current PowerShell session.</span></span>  
4. <span data-ttu-id="7571b-139">vous demande la version la plus récente tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-139">prompts you tooinstall hello latest version.</span></span>  
5. <span data-ttu-id="7571b-140">Installe et importe les modules de hello mis à jour dans la session PowerShell en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="7571b-140">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="7571b-141">Désinstaller des profils</span><span class="sxs-lookup"><span data-stu-id="7571b-141">Uninstall profiles</span></span>

<span data-ttu-id="7571b-142">Hello d’utilisation **AzureRmProfile de désinstallation** applet de commande toouninstall hello spécifié le profil de version d’API.</span><span class="sxs-lookup"><span data-stu-id="7571b-142">Use hello **Uninstall-AzureRmProfile** cmdlet toouninstall hello specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="7571b-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7571b-143">Next steps</span></span>
* [<span data-ttu-id="7571b-144">Installer PowerShell pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7571b-144">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="7571b-145">Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7571b-145">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
