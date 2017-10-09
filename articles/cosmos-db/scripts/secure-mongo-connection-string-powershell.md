---
title: "aaaAzure chaîne de connexion de base de données Cosmos PowerShell Get-Script Azure pour les applications de MongoDB | Documents Microsoft"
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
ms.openlocfilehash: d04502b8f59bb6f3cb8bec696595f962b479fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="c508a-103">Obtenir une chaîne de connexion Azure Cosmos DB pour les applications MongoDB à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c508a-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="c508a-104">Cet exemple obtient une chaîne de connexion Azure Cosmos DB pour les applications MongoDB à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c508a-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c508a-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c508a-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get hello MongoDB connection string from an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c508a-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c508a-106">Clean up deployment</span></span>

<span data-ttu-id="c508a-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="c508a-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c508a-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c508a-108">Script explanation</span></span>

<span data-ttu-id="c508a-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="c508a-109">This script uses hello following commands.</span></span> <span data-ttu-id="c508a-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="c508a-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c508a-111">Commande</span><span class="sxs-lookup"><span data-stu-id="c508a-111">Command</span></span> | <span data-ttu-id="c508a-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="c508a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c508a-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c508a-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="c508a-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c508a-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c508a-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c508a-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="c508a-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="c508a-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c508a-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="c508a-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="c508a-118">Appelle une action sur hello Azure CosmosDB compte.</span><span class="sxs-lookup"><span data-stu-id="c508a-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="c508a-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c508a-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="c508a-120">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c508a-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c508a-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c508a-121">Next steps</span></span>

<span data-ttu-id="c508a-122">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="c508a-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="c508a-123">Vous trouverez des exemples supplémentaires de script PowerShell de base de données Azure Cosmos Bonjour [des scripts PowerShell de base de données Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c508a-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
