---
title: "Exemple Powershell-copier-base de données Azure SQL-nouveau serveur | Microsoft Docs"
description: "Exemple de script Azure PowerShell pour copier une base de données SQL sur un nouveau serveur"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="01435-103">Utiliser PowerShell pour copier une base de données SQL sur un nouveau serveur</span><span class="sxs-lookup"><span data-stu-id="01435-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="01435-104">Cet exemple de script PowerShell crée une copie d’une base de données existante dans un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="01435-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="01435-105">Copier une base de données sur un nouveau serveur</span><span class="sxs-lookup"><span data-stu-id="01435-105">Copy a database to a new server</span></span>

<span data-ttu-id="01435-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copier une base de données sur un nouveau serveur")]</span><span class="sxs-lookup"><span data-stu-id="01435-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="01435-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="01435-107">Clean up deployment</span></span>

<span data-ttu-id="01435-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="01435-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="01435-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="01435-109">Script explanation</span></span>

<span data-ttu-id="01435-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="01435-110">This script uses the following commands.</span></span> <span data-ttu-id="01435-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="01435-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="01435-112">Commande</span><span class="sxs-lookup"><span data-stu-id="01435-112">Command</span></span> | <span data-ttu-id="01435-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="01435-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01435-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01435-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="01435-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="01435-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01435-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="01435-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="01435-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="01435-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="01435-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="01435-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="01435-119">Crée une base de données unique ou mise en pool au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="01435-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="01435-120">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="01435-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="01435-121">Crée une copie d’une base de données qui utilise la capture instantanée à l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="01435-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="01435-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01435-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="01435-123">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="01435-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="01435-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01435-124">Next steps</span></span>

<span data-ttu-id="01435-125">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01435-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="01435-126">Vous trouverez des exemples supplémentaires de scripts SQL Database PowerShell sur la page [Scripts PowerShell Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="01435-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
