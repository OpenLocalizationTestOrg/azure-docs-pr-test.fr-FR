---
title: "aaaAzure exemple de Script PowerShell - créer une application web et déployer le code à partir de GitHub | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Créer une application web et déployer du code à partir de GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="cde64-103">Créer une application web et déployer du code à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="cde64-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="cde64-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web dans un référentiel GitHub public (sans déploiement continu).</span><span class="sxs-lookup"><span data-stu-id="cde64-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="cde64-105">Pour le déploiement GitHub avec déploiement continu, consultez [Créer une application web avec un déploiement continu à partir de GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="cde64-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="cde64-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cde64-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="cde64-107">En outre, vous avez besoin d’un référentiel tooGitHub lien qui contient le code d’application web hello.</span><span class="sxs-lookup"><span data-stu-id="cde64-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="cde64-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="cde64-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cde64-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="cde64-109">Clean up deployment</span></span> 

<span data-ttu-id="cde64-110">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="cde64-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="cde64-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="cde64-111">Script explanation</span></span>

<span data-ttu-id="cde64-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="cde64-112">This script uses hello following commands.</span></span> <span data-ttu-id="cde64-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="cde64-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cde64-114">Commande</span><span class="sxs-lookup"><span data-stu-id="cde64-114">Command</span></span> | <span data-ttu-id="cde64-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="cde64-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cde64-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cde64-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="cde64-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="cde64-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cde64-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="cde64-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="cde64-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="cde64-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="cde64-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="cde64-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="cde64-121">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="cde64-121">Creates a web app.</span></span> |
| [<span data-ttu-id="cde64-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="cde64-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="cde64-123">Modifie une ressource dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cde64-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cde64-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cde64-124">Next steps</span></span>

<span data-ttu-id="cde64-125">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cde64-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cde64-126">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cde64-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
