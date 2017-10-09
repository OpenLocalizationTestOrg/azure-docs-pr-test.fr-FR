---
title: "aaaDownload pile d’Azure tools à partir de GitHub | Documents Microsoft"
description: "Découvrez comment les outils toodownload requis toowork avec la pile de Azure."
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
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="3dc5e-103">Télécharger les outils Azure Stack à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="3dc5e-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="3dc5e-104">AzureStack-Tools est un référentiel GitHub qui héberge des modules PowerShell que vous pouvez utiliser toomanage et déployer des ressources tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use toomanage and deploy resources tooAzure Stack.</span></span> <span data-ttu-id="3dc5e-105">Vous pouvez télécharger et utiliser ces PowerShell modules toohello Kit de développement Azure pile ou tooa basé sur windows externe client si vous envisagez de connectivité VPN de tooestablish.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-105">You can download and use these PowerShell modules toohello Azure Stack Development Kit, or tooa windows-based external client if you are planning tooestablish VPN connectivity.</span></span> <span data-ttu-id="3dc5e-106">tooobtain ces outils, cloner le référentiel GitHub de hello ou hello AzureStack-outils dossier de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-106">tooobtain these tools, clone hello GitHub repository or download hello AzureStack-Tools folder.</span></span> 

<span data-ttu-id="3dc5e-107">référentiel de hello tooclone, téléchargez [Git](https://git-scm.com/download/win) pour Windows, ouvrez une fenêtre d’invite de commandes et exécutez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="3dc5e-107">tooclone hello repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

<span data-ttu-id="3dc5e-108">dossier d’outils hello toodownload, exécutez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="3dc5e-108">toodownload hello tools folder, run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a><span data-ttu-id="3dc5e-109">Fonctionnalités fournies par les modules de hello</span><span class="sxs-lookup"><span data-stu-id="3dc5e-109">Functionalities provided by hello modules</span></span>

<span data-ttu-id="3dc5e-110">référentiel de Hello AzureStack-Tools contient des modules PowerShell qui prennent en charge hello suivant de fonctionnalités pour la pile de Azure :</span><span class="sxs-lookup"><span data-stu-id="3dc5e-110">hello AzureStack-Tools repository contains PowerShell modules that support hello following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="3dc5e-111">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="3dc5e-111">Functionality</span></span> | <span data-ttu-id="3dc5e-112">Description</span><span class="sxs-lookup"><span data-stu-id="3dc5e-112">Description</span></span> | <span data-ttu-id="3dc5e-113">Qui peut utiliser ce module ?</span><span class="sxs-lookup"><span data-stu-id="3dc5e-113">who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3dc5e-114">Fonctionnalités de cloud</span><span class="sxs-lookup"><span data-stu-id="3dc5e-114">Cloud capabilities</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="3dc5e-115">Utilisez cette fonctionnalités de cloud de module tooget hello d’un cloud.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-115">Use this module tooget hello cloud capabilities of a cloud.</span></span> <span data-ttu-id="3dc5e-116">Par exemple, vous pouvez obtenir les capacités du cloud hello telles que la version de l’API, les ressources d’Azure Resource Manager, les extensions de machine virtuelle etc. pour la pile d’Azure et Azure cloud à l’aide de ce module.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-116">For example, you can get hello cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span></span> | <span data-ttu-id="3dc5e-117">Les administrateurs et les utilisateurs de cloud</span><span class="sxs-lookup"><span data-stu-id="3dc5e-117">Cloud administrators and users.</span></span> |
| [<span data-ttu-id="3dc5e-118">Administration de calcul Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3dc5e-118">Azure Stack compute administration</span></span>](azure-stack-add-vm-image.md) | <span data-ttu-id="3dc5e-119">Utilisez cette tooadd module ou supprimer une image de machine virtuelle à partir du marketplace d’Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-119">Use this module tooadd or remove a VM image from hello Azure Stack marketplace.</span></span> | <span data-ttu-id="3dc5e-120">Administrateurs de cloud.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-120">Cloud administrators.</span></span> |
| [<span data-ttu-id="3dc5e-121">Administration de l’infrastructure Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3dc5e-121">Azure Stack Infrastructure administration</span></span>](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | <span data-ttu-id="3dc5e-122">Utilisez cette infrastructure de pile de Azure module toomanage machines virtuelles, des alertes, etc. les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-122">Use this module toomanage Azure Stack infrastructure VMs, alerts, updates etc.</span></span> |  <span data-ttu-id="3dc5e-123">Administrateurs de cloud.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-123">Cloud administrators.</span></span>|
| [<span data-ttu-id="3dc5e-124">Stratégie Resource Manager pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3dc5e-124">Resource Manager policy for Azure Stack</span></span>](azure-stack-policy-module.md) | <span data-ttu-id="3dc5e-125">Utiliser ce module de tooconfigure un abonnement Azure ou une ressource Azure de groupe avec hello même le contrôle de version et le service de disponibilité en tant que pile d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-125">Use this module tooconfigure an Azure subscription or an Azure resource group with hello same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="3dc5e-126">Les administrateurs et les utilisateurs de cloud</span><span class="sxs-lookup"><span data-stu-id="3dc5e-126">Cloud administrators and users</span></span> |
| [<span data-ttu-id="3dc5e-127">Inscription auprès d’Azure</span><span class="sxs-lookup"><span data-stu-id="3dc5e-127">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="3dc5e-128">Utilisez cette tooregister module votre instance de kit de développement avec Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-128">Use this module tooregister your development kit instance with Azure.</span></span> <span data-ttu-id="3dc5e-129">Une fois inscrit, vous pouvez télécharger des éléments du marketplace hello à partir d’Azure et les utiliser dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-129">After registering, you can download hello marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="3dc5e-130">Administrateurs de cloud</span><span class="sxs-lookup"><span data-stu-id="3dc5e-130">Cloud administrators</span></span> |
| [<span data-ttu-id="3dc5e-131">Déploiement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3dc5e-131">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="3dc5e-132">Utilisez cet ordinateur toodeploy de module tooprepare hello Azure pile hôte et redéployer l’aide de l’image de Disk(VHD) de disque dur virtuel de la pile Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-132">Use this module tooprepare hello Azure Stack host computer toodeploy and redeploy by using hello Azure Stack Virtual Hard Disk(VHD) image.</span></span> | <span data-ttu-id="3dc5e-133">Administrateurs de cloud.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-133">Cloud administrators.</span></span> |
| [<span data-ttu-id="3dc5e-134">Connexion tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="3dc5e-134">Connecting tooAzure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="3dc5e-135">Utilisez cette instance d’Azure pile module tooconnect tooan via PowerShell et tooconfigure tooAzure de connectivité VPN pile.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-135">Use this module tooconnect tooan Azure Stack instance through PowerShell and tooconfigure VPN connectivity tooAzure Stack.</span></span> | <span data-ttu-id="3dc5e-136">Les administrateurs et les utilisateurs de cloud</span><span class="sxs-lookup"><span data-stu-id="3dc5e-136">Cloud administrators and users</span></span> |
| [<span data-ttu-id="3dc5e-137">Administration des services Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3dc5e-137">Azure Stack service administration</span></span>](azure-stack-create-offer.md) | <span data-ttu-id="3dc5e-138">Azure pile les administrateurs peuvent utiliser cette toocreate module offrent d’un client par défaut avec un quota illimité dans les services de calcul, stockage, réseau et le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-138">Azure Stack administrators can use this module toocreate a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span></span>   | <span data-ttu-id="3dc5e-139">Administrateurs de cloud.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-139">Cloud administrators.</span></span>|
| [<span data-ttu-id="3dc5e-140">Validateur de modèle</span><span class="sxs-lookup"><span data-stu-id="3dc5e-140">Template validator</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="3dc5e-141">Utilisez cette tooverify module si un existant ou un nouveau modèle peut être déployé tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="3dc5e-141">Use this module tooverify if an existing or a new template can be deployed tooAzure Stack.</span></span> | <span data-ttu-id="3dc5e-142">Les administrateurs et les utilisateurs de cloud</span><span class="sxs-lookup"><span data-stu-id="3dc5e-142">Cloud administrators and users</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3dc5e-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3dc5e-143">Next steps</span></span>
* [<span data-ttu-id="3dc5e-144">Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dc5e-144">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)   
* [<span data-ttu-id="3dc5e-145">Se connecter tooAzure Kit de développement de pile sur un réseau privé virtuel</span><span class="sxs-lookup"><span data-stu-id="3dc5e-145">Connect tooAzure Stack Development Kit over a VPN</span></span>](azure-stack-connect-azure-stack.md)  
