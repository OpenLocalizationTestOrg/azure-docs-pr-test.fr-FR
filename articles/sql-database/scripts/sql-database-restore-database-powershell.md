---
title: "base de données SQL aaaPowerShell exemple restauration sauvegarde Azure | Documents Microsoft"
description: "Azure PowerShell exemple script toorestore une base de données SQL Azure à partir de sauvegardes géo-redondant"
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="5510e-103">Utilisez PowerShell toorestore une base de données SQL Azure à partir de sauvegardes</span><span class="sxs-lookup"><span data-stu-id="5510e-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="5510e-104">Cet exemple de script PowerShell restaure une base de données SQL Azure à partir d’une sauvegarde géo-redondant, restaure un supprimé SQL Azure de base de données tooits dernière sauvegarde et restaure un point spécifique de tooa de base de données de SQL Azure dans le temps.</span><span class="sxs-lookup"><span data-stu-id="5510e-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="5510e-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="5510e-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5510e-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="5510e-106">Clean up deployment</span></span>

<span data-ttu-id="5510e-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="5510e-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5510e-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="5510e-108">Script explanation</span></span>

<span data-ttu-id="5510e-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="5510e-109">This script uses hello following commands.</span></span> <span data-ttu-id="5510e-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="5510e-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5510e-111">Commande</span><span class="sxs-lookup"><span data-stu-id="5510e-111">Command</span></span> | <span data-ttu-id="5510e-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="5510e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5510e-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5510e-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="5510e-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="5510e-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="5510e-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="5510e-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="5510e-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="5510e-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="5510e-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5510e-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="5510e-118">Crée une base de données au sein d’un serveur logique en tant que base de données unique ou regroupée.</span><span class="sxs-lookup"><span data-stu-id="5510e-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="5510e-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="5510e-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="5510e-120">Obtient une sauvegarde géo-redondante d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="5510e-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="5510e-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5510e-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="5510e-122">Restaure une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="5510e-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="5510e-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5510e-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="5510e-124">Supprime une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5510e-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="5510e-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="5510e-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="5510e-126">Obtient une base de données supprimée que vous pouvez restaurer.</span><span class="sxs-lookup"><span data-stu-id="5510e-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="5510e-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5510e-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5510e-128">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="5510e-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5510e-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5510e-129">Next steps</span></span>

<span data-ttu-id="5510e-130">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5510e-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5510e-131">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5510e-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
