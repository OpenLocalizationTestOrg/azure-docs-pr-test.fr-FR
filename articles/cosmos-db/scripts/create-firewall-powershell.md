---
title: "aaaAzure PowerShell Script-création d’un pare-feu pour la base de données Azure Cosmos | Documents Microsoft"
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
ms.openlocfilehash: 00dd2dd847c7ed0e35f5555c2b87b90977f137f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="eb930-103">Azure Cosmos DB : Créer un pare-feu à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb930-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="eb930-104">Cet exemple de script PowerShell crée un pare-feu pour tous types de comptes d’API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eb930-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="eb930-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="eb930-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="eb930-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="eb930-106">Clean up deployment</span></span>

<span data-ttu-id="eb930-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="eb930-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="eb930-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="eb930-108">Script explanation</span></span>

<span data-ttu-id="eb930-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="eb930-109">This script uses hello following commands.</span></span> <span data-ttu-id="eb930-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="eb930-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="eb930-111">Commande</span><span class="sxs-lookup"><span data-stu-id="eb930-111">Command</span></span> | <span data-ttu-id="eb930-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="eb930-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eb930-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="eb930-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="eb930-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="eb930-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eb930-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="eb930-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="eb930-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="eb930-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="eb930-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="eb930-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="eb930-118">Modifie le compte de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="eb930-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="eb930-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="eb930-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="eb930-120">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="eb930-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="eb930-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb930-121">Next steps</span></span>

<span data-ttu-id="eb930-122">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="eb930-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="eb930-123">Vous trouverez des exemples supplémentaires de script PowerShell de base de données Azure Cosmos Bonjour [des scripts PowerShell de base de données Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eb930-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
