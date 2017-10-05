---
title: "Exemple de script Azure PowerShell - Affecter un domaine personnalisé à une application web | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Affecter un domaine personnalisé à une application web"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="aa4d8-103">Affecter un domaine personnalisé à une application web</span><span class="sxs-lookup"><span data-stu-id="aa4d8-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="aa4d8-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis la mappe à `www.<yourdomain>`.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="aa4d8-105">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="aa4d8-106">Vous devez également avoir accès à la page de configuration DNS du bureau d’enregistrement de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="aa4d8-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="aa4d8-107">Sample script</span></span>

<span data-ttu-id="aa4d8-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Affecter un domaine personnalisé à une application web")]</span><span class="sxs-lookup"><span data-stu-id="aa4d8-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="aa4d8-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="aa4d8-109">Clean up deployment</span></span> 

<span data-ttu-id="aa4d8-110">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="aa4d8-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="aa4d8-111">Script explanation</span></span>

<span data-ttu-id="aa4d8-112">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-112">This script uses the following commands.</span></span> <span data-ttu-id="aa4d8-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="aa4d8-114">Commande</span><span class="sxs-lookup"><span data-stu-id="aa4d8-114">Command</span></span> | <span data-ttu-id="aa4d8-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="aa4d8-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aa4d8-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="aa4d8-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="aa4d8-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="aa4d8-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="aa4d8-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="aa4d8-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="aa4d8-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="aa4d8-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="aa4d8-121">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-121">Creates a web app.</span></span> |
| [<span data-ttu-id="aa4d8-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="aa4d8-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="aa4d8-123">Modifie le niveau tarifaire d’un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="aa4d8-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="aa4d8-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="aa4d8-125">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="aa4d8-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aa4d8-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa4d8-126">Next steps</span></span>

<span data-ttu-id="aa4d8-127">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aa4d8-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="aa4d8-128">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="aa4d8-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
