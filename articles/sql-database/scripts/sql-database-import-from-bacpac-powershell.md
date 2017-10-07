---
title: fichier-Azure SQL database aaaPowerShell exemple-import-bacpac | Documents Microsoft
description: "Vignette d’un fichier bacpac tooimport de script Azure PowerShell exemple dans une base de données SQL"
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="84431-103">Utilisez PowerShell tooimport un fichier bacpac dans une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="84431-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="84431-104">Cet exemple de script PowerShell importe dans une base de données SQL Azure, la base de données contenue dans un fichier **Bacpac**.</span><span class="sxs-lookup"><span data-stu-id="84431-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="84431-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="84431-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="84431-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="84431-106">Clean up deployment</span></span>

<span data-ttu-id="84431-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="84431-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="84431-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="84431-108">Script explanation</span></span>

<span data-ttu-id="84431-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="84431-109">This script uses hello following commands.</span></span> <span data-ttu-id="84431-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="84431-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="84431-111">Commande</span><span class="sxs-lookup"><span data-stu-id="84431-111">Command</span></span> | <span data-ttu-id="84431-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="84431-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="84431-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84431-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="84431-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="84431-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="84431-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="84431-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="84431-116">Crée un serveur logique que les ordinateurs hôtes hello de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="84431-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="84431-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="84431-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="84431-118">Crée un tooall dans pare-feu règle tooallow accès aux bases de données SQL sur le serveur hello à partir de la plage d’adresses IP hello entré.</span><span class="sxs-lookup"><span data-stu-id="84431-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="84431-119">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="84431-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="84431-120">Importe un .bacpac fichiers et de créer une nouvelle base de données sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="84431-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="84431-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84431-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="84431-122">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="84431-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84431-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84431-123">Next steps</span></span>

<span data-ttu-id="84431-124">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="84431-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="84431-125">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="84431-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
