---
title: "Script Azure PowerShell - Créer un pare-feu pour Azure Cosmos DB | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Créer un pare-feu pour Azure Cosmos DB"
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
ms.openlocfilehash: caad9212649dd3dc47ddb21555b5b8496c3d2da1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="5caba-103">Azure Cosmos DB : Créer un pare-feu à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5caba-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="5caba-104">Cet exemple de script PowerShell crée un pare-feu pour tous types de comptes d’API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5caba-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="5caba-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="5caba-105">Sample script</span></span>

<span data-ttu-id="5caba-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Créer un pare-feu pour Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="5caba-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5caba-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="5caba-107">Clean up deployment</span></span>

<span data-ttu-id="5caba-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="5caba-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5caba-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="5caba-109">Script explanation</span></span>

<span data-ttu-id="5caba-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="5caba-110">This script uses the following commands.</span></span> <span data-ttu-id="5caba-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="5caba-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5caba-112">Commande</span><span class="sxs-lookup"><span data-stu-id="5caba-112">Command</span></span> | <span data-ttu-id="5caba-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="5caba-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5caba-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5caba-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="5caba-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="5caba-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5caba-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5caba-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="5caba-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="5caba-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5caba-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="5caba-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="5caba-119">Modifie le compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="5caba-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="5caba-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5caba-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="5caba-121">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="5caba-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5caba-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5caba-122">Next steps</span></span>

<span data-ttu-id="5caba-123">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="5caba-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="5caba-124">Vous trouverez des exemples supplémentaires de scripts Azure Cosmos DB PowerShell sur la page [Scripts PowerShell Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5caba-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>