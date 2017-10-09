---
title: "clé du compte de base de données PowerShell Script-Regenerate Azure Cosmos aaaAzure | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Régénérer une clé de compte Azure Cosmos DB"
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
ms.openlocfilehash: 7ac1749a75a12ba7f8ff68e8106c29693490151a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-powershell"></a><span data-ttu-id="b86cc-103">Régénérer une clé de compte Azure Cosmos DB à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b86cc-103">Regenerate an Azure Cosmos DB account key using PowerShell</span></span>

<span data-ttu-id="b86cc-104">Cet exemple régénère n’importe quel type de clé de compte de base de données Azure Cosmos à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b86cc-104">This sample regenerates any kind of Azure Cosmos DB account key using hello Azure CLI.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b86cc-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="b86cc-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/regenerate-account-keys/regenerate-account-keys.ps1?highlight=36-41 "Regenerate Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b86cc-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="b86cc-106">Clean up deployment</span></span>

<span data-ttu-id="b86cc-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b86cc-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b86cc-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b86cc-108">Script explanation</span></span>

<span data-ttu-id="b86cc-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="b86cc-109">This script uses hello following commands.</span></span> <span data-ttu-id="b86cc-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="b86cc-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b86cc-111">Commande</span><span class="sxs-lookup"><span data-stu-id="b86cc-111">Command</span></span> | <span data-ttu-id="b86cc-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="b86cc-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b86cc-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b86cc-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="b86cc-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="b86cc-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b86cc-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b86cc-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="b86cc-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="b86cc-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b86cc-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="b86cc-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="b86cc-118">Appelle une action sur hello Azure CosmosDB compte.</span><span class="sxs-lookup"><span data-stu-id="b86cc-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="b86cc-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b86cc-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="b86cc-120">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="b86cc-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b86cc-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b86cc-121">Next steps</span></span>

<span data-ttu-id="b86cc-122">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="b86cc-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="b86cc-123">Vous trouverez des exemples supplémentaires de script PowerShell de base de données Azure Cosmos Bonjour [des scripts PowerShell de base de données Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b86cc-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
