---
title: "Exemple PowerShell - Groupe de basculement de géoréplication d’une instance unique Azure SQL Database | Microsoft Docs"
description: "Exemple de script Azure PowerShell permettant de configurer la géoréplication active pour une base de données SQL Azure unique"
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
ms.openlocfilehash: 8db8540d9c4caeb53ea8f34d45d9498496d2b8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="97846-103">Utiliser PowerShell pour configurer un groupe de basculement de géoréplication active pour une base de données SQL Azure unique</span><span class="sxs-lookup"><span data-stu-id="97846-103">Use PowerShell to configure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="97846-104">Cet exemple de script PowerShell configure le groupe de basculement de géoréplication active pour une base de données SQL Azure unique et la fait basculer vers le réplica secondaire de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="97846-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="97846-105">Exemples de scripts</span><span class="sxs-lookup"><span data-stu-id="97846-105">Sample scripts</span></span>

<span data-ttu-id="97846-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Permet de configurer le groupe de basculement pour une base de données unique")]</span><span class="sxs-lookup"><span data-stu-id="97846-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="97846-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="97846-107">Clean up deployment</span></span>

<span data-ttu-id="97846-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="97846-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="97846-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="97846-109">Script explanation</span></span>

<span data-ttu-id="97846-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="97846-110">This script uses the following commands.</span></span> <span data-ttu-id="97846-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="97846-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="97846-112">Commande</span><span class="sxs-lookup"><span data-stu-id="97846-112">Command</span></span> | <span data-ttu-id="97846-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="97846-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="97846-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="97846-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="97846-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="97846-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="97846-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="97846-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="97846-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="97846-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="97846-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="97846-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="97846-119">Crée un pool élastique au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="97846-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="97846-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="97846-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="97846-121">Met à jour les propriétés de la base de données ou déplace une base de données vers, hors ou entre des pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="97846-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="97846-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="97846-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="97846-123">Crée une base de données secondaire pour une base de données existante puis lance la réplication des données.</span><span class="sxs-lookup"><span data-stu-id="97846-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="97846-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="97846-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="97846-125">Obtient une ou plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="97846-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="97846-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="97846-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="97846-127">Bascule d’une base de données secondaire à une base de données principale afin de lancer le basculement.</span><span class="sxs-lookup"><span data-stu-id="97846-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="97846-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="97846-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="97846-129">Obtient les liens de géo-réplication entre une base de données SQL Azure et un groupe de ressources ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="97846-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="97846-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="97846-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="97846-131">Met fin à une réplication de données entre une base de données SQL et la base de données secondaire spécifiée.</span><span class="sxs-lookup"><span data-stu-id="97846-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="97846-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="97846-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="97846-133">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="97846-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="97846-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="97846-134">Next steps</span></span>

<span data-ttu-id="97846-135">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="97846-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="97846-136">Vous trouverez des exemples supplémentaires de scripts SQL Database PowerShell sur la page [Scripts PowerShell Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="97846-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
