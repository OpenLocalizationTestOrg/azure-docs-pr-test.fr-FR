---
title: "Créer un serveur Azure Analysis Services à l’aide de PowerShell | Microsoft Docs"
description: "Découvrir comment se connecter à un serveur Azure Analysis Services à l’aide de PowerShell"
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
ms.openlocfilehash: cb42fd3ed51364cf478848cc51ebbb2f175e96d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="6f925-103">Créer un serveur Azure Analysis Services à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f925-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="6f925-104">Ce démarrage rapide décrit comment utiliser PowerShell à partir d’une ligne de commande pour créer un serveur Azure Analysis Services dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6f925-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="6f925-105">Cette tâche requiert le module Azure PowerShell version 4.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6f925-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="6f925-106">Pour connaître la version de l’interface, exécutez ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="6f925-106">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="6f925-107">Pour installer ou mettre à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6f925-107">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="6f925-108">La création d’un serveur peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="6f925-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="6f925-109">Pour en savoir plus, consultez [Tarification d’Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="6f925-109">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f925-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6f925-110">Prerequisites</span></span>
<span data-ttu-id="6f925-111">Pour effectuer ce démarrage rapide, les éléments suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="6f925-111">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="6f925-112">**Abonnement Azure** : visitez [version d’évaluation gratuite d’Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) pour créer un compte.</span><span class="sxs-lookup"><span data-stu-id="6f925-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="6f925-113">**Azure Active Directory** : votre abonnement doit être associé à un client Azure Active Directory et vous devez disposer d’un compte dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="6f925-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="6f925-114">Pour en savoir plus, consultez [Authentification et autorisations utilisateur](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="6f925-114">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="6f925-115">Importer le module de AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="6f925-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="6f925-116">Pour créer un serveur dans votre abonnement, vous utilisez le module de composant [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices).</span><span class="sxs-lookup"><span data-stu-id="6f925-116">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="6f925-117">Chargez le module AzureRm.AnalysisServices dans votre session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f925-117">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a><span data-ttu-id="6f925-118">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="6f925-118">Sign in to Azure</span></span>

<span data-ttu-id="6f925-119">Connectez-vous à votre abonnement Azure à l’aide de la commande [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount).</span><span class="sxs-lookup"><span data-stu-id="6f925-119">Sign in to your Azure subscription by using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="6f925-120">Suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="6f925-120">Follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="6f925-121">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6f925-121">Create a resource group</span></span>
 
<span data-ttu-id="6f925-122">Un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="6f925-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="6f925-123">Lorsque vous créez votre serveur, vous devez spécifier un groupe de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6f925-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="6f925-124">Si vous ne disposez pas d’un groupe de ressources, créez-en un à l’aide de la commande [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="6f925-124">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="6f925-125">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` dans la région États-Unis de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="6f925-125">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="6f925-126">Créer un serveur</span><span class="sxs-lookup"><span data-stu-id="6f925-126">Create a server</span></span>

<span data-ttu-id="6f925-127">Créer un nouveau serveur à l’aide de la commande [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="6f925-127">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="6f925-128">L’exemple suivant crée un serveur nommé myServer dans myResourceGroup, dans la région États-Unis de l’Ouest, au niveau D1, et spécifie philipc@adventureworks.com en tant qu’administrateur de serveur.</span><span class="sxs-lookup"><span data-stu-id="6f925-128">The following example creates a server named myServer in myResourceGroup, in the West US region, at the D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="6f925-129">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="6f925-129">Clean up resources</span></span>

<span data-ttu-id="6f925-130">Vous pouvez supprimer le serveur à partir de votre abonnement à l’aide de la commande [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="6f925-130">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="6f925-131">Si vous continuez avec d’autres démarrages rapides et didacticiels de cette collection, ne supprimez pas votre serveur.</span><span class="sxs-lookup"><span data-stu-id="6f925-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="6f925-132">L’exemple suivant supprime le serveur créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="6f925-132">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="6f925-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f925-133">Next steps</span></span>
<span data-ttu-id="6f925-134">[Gérer Azure Analysis Services avec PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="6f925-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="6f925-135">[Déployer un modèle à partir de SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="6f925-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="6f925-136">Créer un modèle dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6f925-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)