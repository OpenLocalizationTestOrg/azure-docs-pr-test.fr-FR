---
title: "Exemple PowerShell -sauvegarder et restaurer une base de données SQL Azure | Microsoft Docs"
description: "Exemple de script Azure PowerShell pour restaurer une base de données SQL Azure à partir de sauvegardes géo-redondantes"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae1d0c828ae1e7e1e7e07dcc7d6157187a3859d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="6daf8-103">Utiliser PowerShell pour restaurer une base de données SQL Azure à partir de sauvegardes</span><span class="sxs-lookup"><span data-stu-id="6daf8-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="6daf8-104">Cet exemple de script PowerShell restaure une base de données SQL Azure à partir d’une sauvegarde géoredondante, restaure une base de données SQL Azure supprimée à l’aide de sa dernière sauvegarde et restaure une base de données Azure SQL à un point précis dans le temps.</span><span class="sxs-lookup"><span data-stu-id="6daf8-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="6daf8-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="6daf8-105">Sample script</span></span>

<span data-ttu-id="6daf8-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Créer une instance SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="6daf8-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6daf8-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="6daf8-107">Clean up deployment</span></span>

<span data-ttu-id="6daf8-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="6daf8-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="6daf8-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="6daf8-109">Script explanation</span></span>

<span data-ttu-id="6daf8-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="6daf8-110">This script uses the following commands.</span></span> <span data-ttu-id="6daf8-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="6daf8-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6daf8-112">Commande</span><span class="sxs-lookup"><span data-stu-id="6daf8-112">Command</span></span> | <span data-ttu-id="6daf8-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="6daf8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6daf8-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6daf8-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="6daf8-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="6daf8-115">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="6daf8-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="6daf8-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="6daf8-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="6daf8-117">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="6daf8-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="6daf8-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="6daf8-119">Crée une base de données au sein d’un serveur logique en tant que base de données unique ou regroupée.</span><span class="sxs-lookup"><span data-stu-id="6daf8-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="6daf8-120">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="6daf8-120">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="6daf8-121">Obtient une sauvegarde géo-redondante d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="6daf8-121">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="6daf8-122">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="6daf8-122">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="6daf8-123">Restaure une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="6daf8-123">Restores a SQL database.</span></span> |
|[<span data-ttu-id="6daf8-124">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="6daf8-124">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="6daf8-125">Supprime une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6daf8-125">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="6daf8-126">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="6daf8-126">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="6daf8-127">Obtient une base de données supprimée que vous pouvez restaurer.</span><span class="sxs-lookup"><span data-stu-id="6daf8-127">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="6daf8-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6daf8-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="6daf8-129">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="6daf8-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6daf8-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6daf8-130">Next steps</span></span>

<span data-ttu-id="6daf8-131">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6daf8-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6daf8-132">Vous trouverez des exemples supplémentaires de scripts SQL Database PowerShell sur la page [Scripts PowerShell Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6daf8-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
