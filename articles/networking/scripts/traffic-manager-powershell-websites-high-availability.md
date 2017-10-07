---
title: "Exemple de Script PowerShell - acheminer le trafic pour la haute disponibilité des applications d’aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="fcfc5-103">Acheminer le trafic pour la haute disponibilité des applications</span><span class="sxs-lookup"><span data-stu-id="fcfc5-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="fcfc5-104">Ce script crée un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="fcfc5-105">Traffic Manager dirige application toohello au trafic dans une région en tant que zone principale de hello et la région secondaire toohello lors de l’application hello dans la région principale de hello n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="fcfc5-106">Avant d’exécuter le script de hello, vous devez modifier hello MyWebApp, MyWebAppL1 et MyWebAppL2 valeurs toounique valeurs sur Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="fcfc5-107">Après avoir exécuté le script de hello, vous pouvez accéder à application hello dans la région principale de hello avec hello URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="fcfc5-108">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fcfc5-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="fcfc5-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="fcfc5-110">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="fcfc5-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="fcfc5-111">Script explanation</span></span>

<span data-ttu-id="fcfc5-112">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’application web, le profil traffic manager, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="fcfc5-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fcfc5-114">Commande</span><span class="sxs-lookup"><span data-stu-id="fcfc5-114">Command</span></span> | <span data-ttu-id="fcfc5-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="fcfc5-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fcfc5-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fcfc5-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="fcfc5-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fcfc5-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="fcfc5-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="fcfc5-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-119">Creates an App Service plan.</span></span> <span data-ttu-id="fcfc5-120">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="fcfc5-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="fcfc5-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="fcfc5-122">Crée une application web Azure dans hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="fcfc5-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="fcfc5-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="fcfc5-124">Crée une application web Azure dans hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="fcfc5-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="fcfc5-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="fcfc5-126">Crée un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="fcfc5-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="fcfc5-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="fcfc5-128">Ajoute un point de terminaison de tooan profil Traffic Manager de Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc5-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fcfc5-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcfc5-129">Next steps</span></span>

<span data-ttu-id="fcfc5-130">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fcfc5-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="fcfc5-131">Vous trouverez des exemples de script PowerShell mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fcfc5-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
