---
title: "aaaAzure exemple de Script PowerShell - créer une application web et déployer tooa code environnement intermédiaire | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - créer une application web et déployer tooa code environnement intermédiaire"
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
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="24ae4-103">Créer une application web et de déployer tooa code environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="24ae4-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="24ae4-104">Cet exemple de script crée une application web dans le Service d’applications avec un emplacement de déploiement supplémentaire appelé « étape intermédiaire », puis déploie un toohello d’application exemple emplacement « intermédiaire ».</span><span class="sxs-lookup"><span data-stu-id="24ae4-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="24ae4-105">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="24ae4-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="24ae4-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="24ae4-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="24ae4-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="24ae4-107">Clean up deployment</span></span> 

<span data-ttu-id="24ae4-108">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="24ae4-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="24ae4-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="24ae4-109">Script explanation</span></span>

<span data-ttu-id="24ae4-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="24ae4-110">This script uses hello following commands.</span></span> <span data-ttu-id="24ae4-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="24ae4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="24ae4-112">Commande</span><span class="sxs-lookup"><span data-stu-id="24ae4-112">Command</span></span> | <span data-ttu-id="24ae4-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="24ae4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24ae4-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="24ae4-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="24ae4-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="24ae4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="24ae4-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="24ae4-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="24ae4-117">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="24ae4-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="24ae4-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="24ae4-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="24ae4-119">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="24ae4-119">Creates a web app.</span></span> |
| [<span data-ttu-id="24ae4-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="24ae4-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="24ae4-121">Modifie un toochange du plan App Service à son niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="24ae4-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="24ae4-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="24ae4-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="24ae4-123">Crée un emplacement de déploiement pour une application web.</span><span class="sxs-lookup"><span data-stu-id="24ae4-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="24ae4-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="24ae4-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="24ae4-125">Modifie une ressource dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="24ae4-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="24ae4-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="24ae4-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="24ae4-127">Bascule un déploiement d’application web en production.</span><span class="sxs-lookup"><span data-stu-id="24ae4-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="24ae4-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24ae4-128">Next steps</span></span>

<span data-ttu-id="24ae4-129">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24ae4-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="24ae4-130">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24ae4-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
