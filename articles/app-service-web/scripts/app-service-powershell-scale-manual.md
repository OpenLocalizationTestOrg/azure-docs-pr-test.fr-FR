---
title: "Exemple de script Azure PowerShell - Mettre manuellement à l’échelle une application | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Mettre manuellement à l’échelle une application"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="1a581-103">Mettre manuellement à l’échelle une application web</span><span class="sxs-lookup"><span data-stu-id="1a581-103">Scale a web app manually</span></span>

<span data-ttu-id="1a581-104">Dans ce scénario, vous allez apprendre à créer un groupe de ressources, un plan App Service et une application web.</span><span class="sxs-lookup"><span data-stu-id="1a581-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="1a581-105">Vous ferez ensuite évoluer le plan App Service d’une instance unique à plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="1a581-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="1a581-106">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="1a581-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1a581-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="1a581-107">Sample script</span></span>

<span data-ttu-id="1a581-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Mettre manuellement à l’échelle une application web")]</span><span class="sxs-lookup"><span data-stu-id="1a581-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1a581-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="1a581-109">Clean up deployment</span></span> 

<span data-ttu-id="1a581-110">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="1a581-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1a581-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="1a581-111">Script explanation</span></span>

<span data-ttu-id="1a581-112">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="1a581-112">This script uses the following commands.</span></span> <span data-ttu-id="1a581-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="1a581-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1a581-114">Commande</span><span class="sxs-lookup"><span data-stu-id="1a581-114">Command</span></span> | <span data-ttu-id="1a581-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="1a581-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a581-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a581-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1a581-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="1a581-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a581-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="1a581-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1a581-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="1a581-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1a581-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1a581-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1a581-121">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="1a581-121">Creates a web app.</span></span> |
| [<span data-ttu-id="1a581-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1a581-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="1a581-123">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="1a581-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a581-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a581-124">Next steps</span></span>

<span data-ttu-id="1a581-125">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a581-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a581-126">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1a581-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
