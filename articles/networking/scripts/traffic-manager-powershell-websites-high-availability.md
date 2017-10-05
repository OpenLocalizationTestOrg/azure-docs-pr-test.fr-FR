---
title: "Exemple de script Azure PowerShell - Acheminer le trafic pour la haute disponibilité des applications | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Acheminer le trafic pour la haute disponibilité des applications"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="5670c-103">Acheminer le trafic pour la haute disponibilité des applications</span><span class="sxs-lookup"><span data-stu-id="5670c-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="5670c-104">Ce script crée un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="5670c-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="5670c-105">Traffic Manager dirige le trafic vers l’application d’une région considérée comme région principale et d’une région secondaire lorsque l’application de la région principale n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="5670c-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="5670c-106">Avant d’exécuter le script, veillez à modifier les valeurs MyWebApp, MyWebAppL1 et MyWebAppL2 pour leur attribuer des valeurs uniques dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5670c-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="5670c-107">Après avoir exécuté le script, vous pouvez accéder à l’application de la région principale avec l’URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="5670c-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="5670c-108">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="5670c-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5670c-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="5670c-109">Sample script</span></span>

<span data-ttu-id="5670c-110">[!code-powershell[principal](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Acheminer le trafic pour la haute disponibilité")]</span><span class="sxs-lookup"><span data-stu-id="5670c-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="5670c-111">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="5670c-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="5670c-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="5670c-112">Script explanation</span></span>

<span data-ttu-id="5670c-113">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web, un profil Traffic Manager et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="5670c-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="5670c-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="5670c-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5670c-115">Commande</span><span class="sxs-lookup"><span data-stu-id="5670c-115">Command</span></span> | <span data-ttu-id="5670c-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="5670c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5670c-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5670c-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="5670c-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="5670c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5670c-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5670c-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5670c-120">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="5670c-120">Creates an App Service plan.</span></span> <span data-ttu-id="5670c-121">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="5670c-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5670c-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5670c-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5670c-123">Crée une application web Azure dans le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="5670c-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="5670c-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5670c-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="5670c-125">Crée une application web Azure dans le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="5670c-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="5670c-126">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="5670c-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="5670c-127">Crée un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="5670c-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="5670c-128">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="5670c-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="5670c-129">Ajoute un point de terminaison à un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="5670c-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5670c-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5670c-130">Next steps</span></span>

<span data-ttu-id="5670c-131">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5670c-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="5670c-132">Vous pouvez trouver des exemples supplémentaires de scripts PowerShell de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5670c-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>