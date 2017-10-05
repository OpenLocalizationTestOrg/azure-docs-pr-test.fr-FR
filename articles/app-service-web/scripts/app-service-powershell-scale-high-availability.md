---
title: "Exemple de script Azure PowerShell - Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 9acd1cf4d1a5705811c4dedc545505ec0ac55fc7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="34dab-103">Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="34dab-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="34dab-104">Dans ce scénario, vous créez un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="34dab-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="34dab-105">Une fois cette procédure terminée, vous bénéficiez d’une architecture haute disponibilité qui offre une disponibilité globale de votre application web en fonction de la plus faible latence réseau.</span><span class="sxs-lookup"><span data-stu-id="34dab-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="34dab-106">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="34dab-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="34dab-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="34dab-107">Sample script</span></span>

<span data-ttu-id="34dab-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité")]</span><span class="sxs-lookup"><span data-stu-id="34dab-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="34dab-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="34dab-109">Clean up deployment</span></span> 

<span data-ttu-id="34dab-110">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="34dab-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="34dab-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="34dab-111">Script explanation</span></span>

<span data-ttu-id="34dab-112">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="34dab-112">This script uses the following commands.</span></span> <span data-ttu-id="34dab-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="34dab-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="34dab-114">Commande</span><span class="sxs-lookup"><span data-stu-id="34dab-114">Command</span></span> | <span data-ttu-id="34dab-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="34dab-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="34dab-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="34dab-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="34dab-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="34dab-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="34dab-118">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="34dab-118">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="34dab-119">Crée un profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="34dab-119">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="34dab-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="34dab-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="34dab-121">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="34dab-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="34dab-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="34dab-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="34dab-123">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="34dab-123">Creates a web app.</span></span> |
| [<span data-ttu-id="34dab-124">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="34dab-124">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="34dab-125">Crée un point de terminaison dans un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="34dab-125">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="34dab-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34dab-126">Next steps</span></span>

<span data-ttu-id="34dab-127">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="34dab-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="34dab-128">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="34dab-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
