---
title: "aaaPowerShell exemple-géo-réplication basculement unique du groupe de base de données SQL Azure | Documents Microsoft"
description: "Azure tooset de script d’exemple PowerShell de géo-réplication active pour une base de données SQL Azure"
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
ms.openlocfilehash: 0ea7afb1125b95370811ef7f80cb9eb7391b2443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="b1f7e-103">Utilisez PowerShell tooconfigure un groupe de basculement de géo-réplication active pour une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b1f7e-103">Use PowerShell tooconfigure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="b1f7e-104">Cet exemple de script PowerShell configure un groupe de basculement de géo-réplication active pour une base de données SQL Azure et elle bascule tooa le réplica de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="b1f7e-105">Exemples de scripts</span><span class="sxs-lookup"><span data-stu-id="b1f7e-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b1f7e-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="b1f7e-106">Clean up deployment</span></span>

<span data-ttu-id="b1f7e-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b1f7e-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b1f7e-108">Script explanation</span></span>

<span data-ttu-id="b1f7e-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-109">This script uses hello following commands.</span></span> <span data-ttu-id="b1f7e-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b1f7e-111">Commande</span><span class="sxs-lookup"><span data-stu-id="b1f7e-111">Command</span></span> | <span data-ttu-id="b1f7e-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="b1f7e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b1f7e-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b1f7e-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b1f7e-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b1f7e-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b1f7e-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b1f7e-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b1f7e-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b1f7e-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="b1f7e-118">Crée un pool élastique au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="b1f7e-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b1f7e-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="b1f7e-120">Met à jour les propriétés de la base de données ou déplace une base de données vers, hors ou entre des pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="b1f7e-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b1f7e-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="b1f7e-122">Crée une base de données secondaire pour une base de données existante puis lance la réplication des données.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="b1f7e-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b1f7e-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="b1f7e-124">Obtient une ou plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="b1f7e-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b1f7e-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="b1f7e-126">Bascule un basculement de principal tooinitiate toobe base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="b1f7e-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="b1f7e-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="b1f7e-128">Obtient les liens de géo-réplication hello entre une base de données SQL Azure et un groupe de ressources ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="b1f7e-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b1f7e-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="b1f7e-130">Met fin à la réplication des données entre une base de données SQL et de la base de données secondaire hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="b1f7e-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b1f7e-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b1f7e-132">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="b1f7e-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b1f7e-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1f7e-133">Next steps</span></span>

<span data-ttu-id="b1f7e-134">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b1f7e-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b1f7e-135">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b1f7e-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
