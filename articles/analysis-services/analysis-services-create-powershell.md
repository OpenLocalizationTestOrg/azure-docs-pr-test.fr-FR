---
title: "aaaCreate un serveur Azure Analysis Services à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate un Azure Analysis Services server à l’aide de PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="3521a-103">Créer un serveur Azure Analysis Services à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3521a-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="3521a-104">Ce démarrage rapide décrit à l’aide de PowerShell à partir de toocreate de ligne de commande hello un serveur Azure Analysis Services dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3521a-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="3521a-105">Cette tâche requiert le module Azure PowerShell version 4.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3521a-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="3521a-106">version de hello toofind, exécutez ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="3521a-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="3521a-107">tooinstall ou mise à niveau, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3521a-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="3521a-108">La création d’un serveur peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="3521a-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="3521a-109">toolearn, voir [Analysis Services tarification](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="3521a-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3521a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3521a-110">Prerequisites</span></span>
<span data-ttu-id="3521a-111">toocomplete ce démarrage rapide, vous devez :</span><span class="sxs-lookup"><span data-stu-id="3521a-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="3521a-112">**Abonnement Azure**: visitez [d’évaluation gratuite Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un compte.</span><span class="sxs-lookup"><span data-stu-id="3521a-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="3521a-113">**Azure Active Directory** : votre abonnement doit être associé à un client Azure Active Directory et vous devez disposer d’un compte dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="3521a-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="3521a-114">toolearn, voir [d’authentification et les autorisations utilisateur](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="3521a-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="3521a-115">Importer le module de AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="3521a-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="3521a-116">toocreate un serveur dans votre abonnement, vous utilisez hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) module de composant.</span><span class="sxs-lookup"><span data-stu-id="3521a-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="3521a-117">Charger le module AzureRm.AnalysisServices hello dans votre session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3521a-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="3521a-118">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="3521a-118">Sign in tooAzure</span></span>

<span data-ttu-id="3521a-119">Se connecter à l’aide de hello tooyour abonnement Azure [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) commande.</span><span class="sxs-lookup"><span data-stu-id="3521a-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="3521a-120">Suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="3521a-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3521a-121">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3521a-121">Create a resource group</span></span>
 
<span data-ttu-id="3521a-122">Un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="3521a-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="3521a-123">Lorsque vous créez votre serveur, vous devez spécifier un groupe de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3521a-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="3521a-124">Si vous n’avez pas déjà un groupe de ressources, vous pouvez créer un autre à l’aide de hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) commande.</span><span class="sxs-lookup"><span data-stu-id="3521a-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="3521a-125">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` dans la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="3521a-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="3521a-126">Créer un serveur</span><span class="sxs-lookup"><span data-stu-id="3521a-126">Create a server</span></span>

<span data-ttu-id="3521a-127">Créer un nouveau serveur à l’aide de hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) commande.</span><span class="sxs-lookup"><span data-stu-id="3521a-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="3521a-128">Hello exemple suivant crée un serveur nommé myServer dans myResourceGroup, dans la région ouest des États-Unis hello, au niveau de hello D1 et spécifie philipc@adventureworks.com en tant qu’un administrateur de serveur.</span><span class="sxs-lookup"><span data-stu-id="3521a-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="3521a-129">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="3521a-129">Clean up resources</span></span>

<span data-ttu-id="3521a-130">Vous pouvez supprimer le serveur de hello à partir de votre abonnement à l’aide de hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) commande.</span><span class="sxs-lookup"><span data-stu-id="3521a-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="3521a-131">Si vous continuez avec d’autres démarrages rapides et didacticiels de cette collection, ne supprimez pas votre serveur.</span><span class="sxs-lookup"><span data-stu-id="3521a-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="3521a-132">Hello exemple suivant supprime du serveur hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="3521a-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="3521a-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3521a-133">Next steps</span></span>
<span data-ttu-id="3521a-134">[Gérer Azure Analysis Services avec PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="3521a-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="3521a-135">[Déployer un modèle à partir de SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="3521a-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="3521a-136">Créer un modèle dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="3521a-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)