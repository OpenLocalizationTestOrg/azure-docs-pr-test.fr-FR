---
title: "Script PowerShell Azure - Obtenir la chaîne de connexion à Azure Cosmos DB pour les applications MongoDB | Microsoft Docs"
description: "Exemple de script PowerShell Azure - Obtenir la chaîne de connexion à Azure Cosmos DB pour les applications MongoDB"
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
ms.openlocfilehash: e44e35cc7d11db48cd82e470ce8226b3c8cc220a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="75a99-103">Obtenir une chaîne de connexion Azure Cosmos DB pour les applications MongoDB à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="75a99-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="75a99-104">Cet exemple obtient une chaîne de connexion Azure Cosmos DB pour les applications MongoDB à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="75a99-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="75a99-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="75a99-105">Sample script</span></span>

<span data-ttu-id="75a99-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Obtenir la chaîne de connexion MongoDB à partir d’un compte Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="75a99-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get the MongoDB connection string from an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="75a99-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="75a99-107">Clean up deployment</span></span>

<span data-ttu-id="75a99-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="75a99-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="75a99-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="75a99-109">Script explanation</span></span>

<span data-ttu-id="75a99-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="75a99-110">This script uses the following commands.</span></span> <span data-ttu-id="75a99-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="75a99-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="75a99-112">Commande</span><span class="sxs-lookup"><span data-stu-id="75a99-112">Command</span></span> | <span data-ttu-id="75a99-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="75a99-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="75a99-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75a99-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="75a99-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="75a99-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="75a99-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="75a99-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="75a99-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="75a99-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="75a99-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="75a99-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="75a99-119">Appelle une action sur le compte Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="75a99-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="75a99-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75a99-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="75a99-121">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="75a99-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="75a99-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="75a99-122">Next steps</span></span>

<span data-ttu-id="75a99-123">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="75a99-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="75a99-124">Vous trouverez des exemples supplémentaires de scripts Azure Cosmos DB PowerShell sur la page [Scripts PowerShell Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="75a99-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>