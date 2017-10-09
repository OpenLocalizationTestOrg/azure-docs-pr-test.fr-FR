---
title: "aaaAzure exemple de Script PowerShell - mise à l’échelle une application web dans le monde entier avec une architecture haute disponibilité | Documents Microsoft"
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
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="c8479-103">Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="c8479-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="c8479-104">Dans ce scénario, vous créez un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="c8479-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="c8479-105">Une fois terminée l’exercice de hello avoir une disponibilité architecture qui permet de fournit une disponibilité globale de votre application web en fonction de la latence réseau la plus faible de hello.</span><span class="sxs-lookup"><span data-stu-id="c8479-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="c8479-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="c8479-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c8479-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c8479-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c8479-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c8479-108">Clean up deployment</span></span> 

<span data-ttu-id="c8479-109">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="c8479-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c8479-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c8479-110">Script explanation</span></span>

<span data-ttu-id="c8479-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="c8479-111">This script uses hello following commands.</span></span> <span data-ttu-id="c8479-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="c8479-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c8479-113">Commande</span><span class="sxs-lookup"><span data-stu-id="c8479-113">Command</span></span> | <span data-ttu-id="c8479-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="c8479-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c8479-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c8479-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c8479-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c8479-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c8479-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="c8479-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="c8479-118">Crée un profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="c8479-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="c8479-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c8479-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c8479-120">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="c8479-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c8479-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c8479-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c8479-122">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="c8479-122">Creates a web app.</span></span> |
| [<span data-ttu-id="c8479-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="c8479-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="c8479-124">Crée un point de terminaison dans un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="c8479-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c8479-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8479-125">Next steps</span></span>

<span data-ttu-id="c8479-126">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c8479-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c8479-127">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c8479-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
