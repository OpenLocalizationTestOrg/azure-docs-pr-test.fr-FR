---
title: "aaaPowerShell exemple analyse échelle SQL élastique pool Azure base de données SQL | Documents Microsoft"
description: "Exemple de PowerShell Azure toomonitor de script et l’échelle d’un pool élastique SQL dans la base de données SQL Azure"
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
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="b7467-103">Utilisez PowerShell toomonitor et mettre à l’échelle d’un pool élastique SQL dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b7467-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="b7467-104">Cet exemple de script PowerShell moniteurs hello métriques de performances d’un pool élastique, il ajuste le niveau de performance supérieur tooa et crée une règle d’alerte sur l’un des métriques de performances hello.</span><span class="sxs-lookup"><span data-stu-id="b7467-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b7467-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="b7467-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b7467-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="b7467-106">Clean up deployment</span></span>

<span data-ttu-id="b7467-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b7467-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b7467-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b7467-108">Script explanation</span></span>

<span data-ttu-id="b7467-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="b7467-109">This script uses hello following commands.</span></span> <span data-ttu-id="b7467-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="b7467-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b7467-111">Commande</span><span class="sxs-lookup"><span data-stu-id="b7467-111">Command</span></span> | <span data-ttu-id="b7467-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="b7467-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="b7467-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b7467-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b7467-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="b7467-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b7467-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b7467-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b7467-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="b7467-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b7467-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b7467-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="b7467-118">Crée un pool élastique au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="b7467-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="b7467-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b7467-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="b7467-120">Crée une base de données au sein d’un serveur logique en tant que base de données unique ou regroupée.</span><span class="sxs-lookup"><span data-stu-id="b7467-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="b7467-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="b7467-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="b7467-122">Affiche des informations d’utilisation de taille hello pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b7467-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="b7467-123">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="b7467-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="b7467-124">Ajoute ou met à jour une règle d’alerte basée sur une mesure.</span><span class="sxs-lookup"><span data-stu-id="b7467-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="b7467-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b7467-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="b7467-126">Met à jour les propriétés du pool élastique</span><span class="sxs-lookup"><span data-stu-id="b7467-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="b7467-127">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="b7467-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="b7467-128">Définit une règle d’alerte tooautomatically analyse dtu Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="b7467-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="b7467-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b7467-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b7467-130">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="b7467-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b7467-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7467-131">Next steps</span></span>

<span data-ttu-id="b7467-132">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7467-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b7467-133">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b7467-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
