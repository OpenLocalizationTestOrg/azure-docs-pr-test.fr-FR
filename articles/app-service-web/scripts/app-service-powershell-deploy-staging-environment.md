---
title: "Exemple de script Azure PowerShell - Créer une application web et déployer du code dans un environnement intermédiaire | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Créer une application web et déployer du code dans un environnement intermédiaire"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 55adc13350eb0f4711efa3c901f6e4e7755dfb27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="f98a4-103">Créer une application web et déployer du code dans un environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="f98a4-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="f98a4-104">Cet exemple de script crée une application web dans App Service avec un emplacement de déploiement supplémentaire appelé « intermédiaire », puis déploie un exemple d’application à l’emplacement « intermédiaire ».</span><span class="sxs-lookup"><span data-stu-id="f98a4-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="f98a4-105">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="f98a4-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f98a4-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="f98a4-106">Sample script</span></span>

<span data-ttu-id="f98a4-107">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Créer une application web et déployer du code dans un environnement intermédiaire")]</span><span class="sxs-lookup"><span data-stu-id="f98a4-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f98a4-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="f98a4-108">Clean up deployment</span></span> 

<span data-ttu-id="f98a4-109">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="f98a4-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f98a4-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="f98a4-110">Script explanation</span></span>

<span data-ttu-id="f98a4-111">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="f98a4-111">This script uses the following commands.</span></span> <span data-ttu-id="f98a4-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="f98a4-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f98a4-113">Commande</span><span class="sxs-lookup"><span data-stu-id="f98a4-113">Command</span></span> | <span data-ttu-id="f98a4-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="f98a4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f98a4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f98a4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f98a4-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="f98a4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f98a4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f98a4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f98a4-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="f98a4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f98a4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f98a4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f98a4-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="f98a4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="f98a4-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f98a4-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="f98a4-122">Modifie le niveau tarifaire d’un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="f98a4-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="f98a4-123">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="f98a4-123">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="f98a4-124">Crée un emplacement de déploiement pour une application web.</span><span class="sxs-lookup"><span data-stu-id="f98a4-124">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="f98a4-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f98a4-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="f98a4-126">Modifie une ressource dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f98a4-126">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="f98a4-127">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="f98a4-127">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="f98a4-128">Bascule un déploiement d’application web en production.</span><span class="sxs-lookup"><span data-stu-id="f98a4-128">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f98a4-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f98a4-129">Next steps</span></span>

<span data-ttu-id="f98a4-130">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f98a4-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f98a4-131">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="f98a4-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
