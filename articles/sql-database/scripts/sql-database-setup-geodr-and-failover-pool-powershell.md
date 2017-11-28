---
title: "base de données SQL Azure regroupées géo-réplication active de l’exemple aaaPowerShell | Documents Microsoft"
description: "Azure tooset de script d’exemple PowerShell de géo-réplication active pour une base de données SQL Azure"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="20fe4-103">Utilisez PowerShell tooconfigure géo-réplication active pour une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="20fe4-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="20fe4-104">Cet exemple de script PowerShell configure géo-réplication active pour une base de données SQL Azure dans un pool élastique et elle bascule toohello le réplica de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="20fe4-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="20fe4-105">Exemples de scripts</span><span class="sxs-lookup"><span data-stu-id="20fe4-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="20fe4-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="20fe4-106">Clean up deployment</span></span>

<span data-ttu-id="20fe4-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="20fe4-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="20fe4-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="20fe4-108">Script explanation</span></span>

<span data-ttu-id="20fe4-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="20fe4-109">This script uses hello following commands.</span></span> <span data-ttu-id="20fe4-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="20fe4-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="20fe4-111">Commande</span><span class="sxs-lookup"><span data-stu-id="20fe4-111">Command</span></span> | <span data-ttu-id="20fe4-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="20fe4-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="20fe4-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20fe4-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="20fe4-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="20fe4-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="20fe4-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="20fe4-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="20fe4-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="20fe4-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="20fe4-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="20fe4-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="20fe4-118">Crée un pool élastique au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="20fe4-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="20fe4-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="20fe4-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="20fe4-120">Crée une base de données au sein d’un serveur logique en tant que base de données unique ou regroupée.</span><span class="sxs-lookup"><span data-stu-id="20fe4-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="20fe4-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="20fe4-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="20fe4-122">Met à jour les propriétés de la base de données ou déplace une base de données vers, hors ou entre des pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="20fe4-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="20fe4-123">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="20fe4-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="20fe4-124">Crée une base de données secondaire pour une base de données existante puis lance la réplication des données.</span><span class="sxs-lookup"><span data-stu-id="20fe4-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="20fe4-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="20fe4-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="20fe4-126">Obtient une ou plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="20fe4-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="20fe4-127">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="20fe4-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="20fe4-128">Commutateurs toobe principal de base de données secondaire dans l’ordre de basculement tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="20fe4-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="20fe4-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="20fe4-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="20fe4-130">Obtient les liens de géo-réplication hello entre une base de données SQL Azure et un groupe de ressources ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="20fe4-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="20fe4-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20fe4-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="20fe4-132">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="20fe4-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="20fe4-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="20fe4-133">Next steps</span></span>

<span data-ttu-id="20fe4-134">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20fe4-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="20fe4-135">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20fe4-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
