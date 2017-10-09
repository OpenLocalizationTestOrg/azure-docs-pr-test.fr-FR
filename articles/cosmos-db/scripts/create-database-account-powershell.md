---
title: "aaaAzure PowerShell créer Script un compte Azure Cosmos DB DocumentDB API | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Créer un compte d’API DocumentDB Azure Cosmos DB"
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
ms.openlocfilehash: f0751faeca3c1de5906b675e736c58f3d5beaea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="c0b20-103">Azure Cosmos DB : Créer un compte d’API DocumentDB avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0b20-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="c0b20-104">Cet exemple de script PowerShell crée un compte d’API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c0b20-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c0b20-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c0b20-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c0b20-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c0b20-106">Clean up deployment</span></span>

<span data-ttu-id="c0b20-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="c0b20-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c0b20-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c0b20-108">Script explanation</span></span>

<span data-ttu-id="c0b20-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="c0b20-109">This script uses hello following commands.</span></span> <span data-ttu-id="c0b20-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="c0b20-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c0b20-111">Commande</span><span class="sxs-lookup"><span data-stu-id="c0b20-111">Command</span></span> | <span data-ttu-id="c0b20-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="c0b20-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c0b20-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0b20-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="c0b20-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c0b20-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c0b20-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c0b20-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="c0b20-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="c0b20-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c0b20-117">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0b20-117">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="c0b20-118">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c0b20-118">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c0b20-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0b20-119">Next steps</span></span>

<span data-ttu-id="c0b20-120">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="c0b20-120">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="c0b20-121">Vous trouverez des exemples supplémentaires de script PowerShell de base de données Azure Cosmos Bonjour [des scripts PowerShell de base de données Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c0b20-121">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
