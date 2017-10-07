---
title: "aaaAzure exemple de Script PowerShell - affecter une application web de tooa domaine personnalisé | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - affecter une application web de tooa domaine personnalisé"
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
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="e3bab-103">Affecter une application web de tooa domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="e3bab-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="e3bab-104">Cet exemple de script crée une application web dans le Service d’applications avec ses ressources connexes et mappe ensuite `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="e3bab-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="e3bab-105">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bab-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="e3bab-106">En outre, vous devez page de configuration toohave accès tooyour domaine du bureau d’enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="e3bab-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e3bab-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e3bab-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e3bab-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="e3bab-108">Clean up deployment</span></span> 

<span data-ttu-id="e3bab-109">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="e3bab-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e3bab-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e3bab-110">Script explanation</span></span>

<span data-ttu-id="e3bab-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="e3bab-111">This script uses hello following commands.</span></span> <span data-ttu-id="e3bab-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e3bab-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e3bab-113">Commande</span><span class="sxs-lookup"><span data-stu-id="e3bab-113">Command</span></span> | <span data-ttu-id="e3bab-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="e3bab-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e3bab-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e3bab-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e3bab-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e3bab-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e3bab-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e3bab-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="e3bab-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="e3bab-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e3bab-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e3bab-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="e3bab-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="e3bab-120">Creates a web app.</span></span> |
| [<span data-ttu-id="e3bab-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e3bab-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="e3bab-122">Modifie un toochange du plan App Service à son niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="e3bab-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="e3bab-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e3bab-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="e3bab-124">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="e3bab-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e3bab-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3bab-125">Next steps</span></span>

<span data-ttu-id="e3bab-126">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e3bab-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e3bab-127">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e3bab-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
