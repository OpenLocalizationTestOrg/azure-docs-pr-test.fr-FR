---
title: "aaaPowerShell exemple-copy-Azure SQL server nouvelle base de données | Documents Microsoft"
description: "Azure PowerShell exemple script toocopy un serveur de nouveau tooa de base de données SQL"
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
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="e8e74-103">Utilisez PowerShell toocopy un serveur de nouveau tooa de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="e8e74-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="e8e74-104">Cet exemple de script PowerShell crée une copie d’une base de données existante dans un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="e8e74-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="e8e74-105">Copier un tooa nouveau serveur de base de données</span><span class="sxs-lookup"><span data-stu-id="e8e74-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e8e74-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="e8e74-106">Clean up deployment</span></span>

<span data-ttu-id="e8e74-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e8e74-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="e8e74-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e8e74-108">Script explanation</span></span>

<span data-ttu-id="e8e74-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="e8e74-109">This script uses hello following commands.</span></span> <span data-ttu-id="e8e74-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e8e74-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e8e74-111">Commande</span><span class="sxs-lookup"><span data-stu-id="e8e74-111">Command</span></span> | <span data-ttu-id="e8e74-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="e8e74-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8e74-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e8e74-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e8e74-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e8e74-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e8e74-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="e8e74-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="e8e74-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="e8e74-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="e8e74-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="e8e74-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="e8e74-118">Crée une base de données unique ou mise en pool au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="e8e74-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="e8e74-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="e8e74-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="e8e74-120">Crée une copie de base de données utilise la capture instantanée de hello en hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="e8e74-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="e8e74-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e8e74-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e8e74-122">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="e8e74-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="e8e74-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8e74-123">Next steps</span></span>

<span data-ttu-id="e8e74-124">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8e74-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e8e74-125">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e8e74-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
