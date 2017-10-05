---
title: "Script Azure PowerShell - Obtenir les clés de compte pour cosmosdb | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Obtenir les clés de compte pour cosmosdb"
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
ms.openlocfilehash: 912e1af684c90cd84b6b00bacbc7dd8d4434c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-powershell"></a><span data-ttu-id="9dbde-103">Obtenir les clés de compte pour Azure Cosmos DB avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dbde-103">Get account keys for Azure Cosmos DB using PowerShell</span></span>

<span data-ttu-id="9dbde-104">Cet exemple obtient les clés de compte de n’importe quel type de compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9dbde-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="9dbde-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="9dbde-105">Sample script</span></span>

<span data-ttu-id="9dbde-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Obtenir les clés pour un compte Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="9dbde-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Get the keys for an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9dbde-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="9dbde-107">Clean up deployment</span></span>

<span data-ttu-id="9dbde-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="9dbde-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="9dbde-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="9dbde-109">Script explanation</span></span>

<span data-ttu-id="9dbde-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="9dbde-110">This script uses the following commands.</span></span> <span data-ttu-id="9dbde-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="9dbde-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9dbde-112">Commande</span><span class="sxs-lookup"><span data-stu-id="9dbde-112">Command</span></span> | <span data-ttu-id="9dbde-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="9dbde-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9dbde-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9dbde-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="9dbde-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="9dbde-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9dbde-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9dbde-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="9dbde-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="9dbde-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="9dbde-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="9dbde-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="9dbde-119">Appelle une action sur le compte Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="9dbde-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="9dbde-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9dbde-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="9dbde-121">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="9dbde-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="9dbde-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9dbde-122">Next steps</span></span>

<span data-ttu-id="9dbde-123">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="9dbde-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="9dbde-124">Vous trouverez des exemples supplémentaires de scripts Azure Cosmos DB PowerShell sur la page [Scripts PowerShell Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9dbde-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>