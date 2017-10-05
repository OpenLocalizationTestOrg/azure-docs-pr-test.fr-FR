---
title: "Exemple PowerShell-surveiller-mettre à l’échelle-pool élastique SQL-Azure SQL Database | Microsoft Docs"
description: "Exemple de script Azure PowerShell pour surveiller et mettre à l’échelle un pool élastique SQL dans Azure SQL Database"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="9a8d7-103">Utiliser PowerShell pour surveiller et mettre à l’échelle un pool élastique SQL dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9a8d7-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="9a8d7-104">Cet exemple de script PowerShell surveille les mesures de performances d’un pool élastique, l’adapte à un niveau de performances supérieur et crée une règle d’alerte sur l’une des mesures de performances.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="9a8d7-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="9a8d7-105">Sample script</span></span>

<span data-ttu-id="9a8d7-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Surveillance et mise à l’échelle d’une instance SQL Database unique")]</span><span class="sxs-lookup"><span data-stu-id="9a8d7-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9a8d7-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="9a8d7-107">Clean up deployment</span></span>

<span data-ttu-id="9a8d7-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="9a8d7-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="9a8d7-109">Script explanation</span></span>

<span data-ttu-id="9a8d7-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-110">This script uses the following commands.</span></span> <span data-ttu-id="9a8d7-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9a8d7-112">Commande</span><span class="sxs-lookup"><span data-stu-id="9a8d7-112">Command</span></span> | <span data-ttu-id="9a8d7-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="9a8d7-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="9a8d7-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9a8d7-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9a8d7-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9a8d7-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="9a8d7-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="9a8d7-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="9a8d7-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="9a8d7-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="9a8d7-119">Crée un pool élastique au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="9a8d7-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="9a8d7-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="9a8d7-121">Crée une base de données au sein d’un serveur logique en tant que base de données unique ou regroupée.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="9a8d7-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="9a8d7-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="9a8d7-123">Affiche les données de taille de la base de données.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="9a8d7-124">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="9a8d7-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="9a8d7-125">Ajoute ou met à jour une règle d’alerte basée sur une mesure.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="9a8d7-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="9a8d7-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="9a8d7-127">Met à jour les propriétés du pool élastique</span><span class="sxs-lookup"><span data-stu-id="9a8d7-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="9a8d7-128">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="9a8d7-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="9a8d7-129">Définit une règle d’alerte pour surveiller automatiquement les DTU à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="9a8d7-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9a8d7-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9a8d7-131">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="9a8d7-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="9a8d7-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a8d7-132">Next steps</span></span>

<span data-ttu-id="9a8d7-133">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a8d7-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9a8d7-134">Vous trouverez des exemples supplémentaires de scripts SQL Database PowerShell sur la page [Scripts PowerShell Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9a8d7-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
