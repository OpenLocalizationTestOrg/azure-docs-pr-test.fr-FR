---
title: "Script Azure PowerShell - Réplication multirégion Azure Cosmos DB | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Réplication multirégion Azure Cosmos DB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 3a469ba43e6c601f5eb0e13d588cd0bd4a0f8683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="a0fe1-103">Répliquer un compte de base de données Azure Cosmos DB dans plusieurs régions et configurer les priorités de basculement avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0fe1-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="a0fe1-104">Cet exemple réplique tout type de compte de base de données Azure Cosmos DB dans plusieurs régions et configure les priorités de basculement à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="a0fe1-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a0fe1-105">Sample script</span></span>

<span data-ttu-id="a0fe1-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Répliquer un compte de Azure Cosmos DB à travers plusieurs régions")]</span><span class="sxs-lookup"><span data-stu-id="a0fe1-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a0fe1-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a0fe1-107">Clean up deployment</span></span>

<span data-ttu-id="a0fe1-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a0fe1-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a0fe1-109">Script explanation</span></span>

<span data-ttu-id="a0fe1-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-110">This script uses the following commands.</span></span> <span data-ttu-id="a0fe1-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a0fe1-112">Commande</span><span class="sxs-lookup"><span data-stu-id="a0fe1-112">Command</span></span> | <span data-ttu-id="a0fe1-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="a0fe1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a0fe1-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a0fe1-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="a0fe1-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a0fe1-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="a0fe1-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="a0fe1-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a0fe1-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="a0fe1-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="a0fe1-119">Modifie le compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="a0fe1-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a0fe1-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="a0fe1-121">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="a0fe1-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a0fe1-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0fe1-122">Next steps</span></span>

<span data-ttu-id="a0fe1-123">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="a0fe1-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="a0fe1-124">Vous trouverez des exemples supplémentaires de scripts Azure Cosmos DB PowerShell sur la page [Scripts PowerShell Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a0fe1-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>