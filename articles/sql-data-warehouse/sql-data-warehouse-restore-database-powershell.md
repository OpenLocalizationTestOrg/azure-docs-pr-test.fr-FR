---
title: "Restauration d’un entrepôt de données Azure SQL Data Warehouse (PowerShell) | Microsoft Docs"
description: "Tâches PowerShell permettant de restaurer un Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="49d44-103">Restauration d’un Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="49d44-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="49d44-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="49d44-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="49d44-105">[Portail][Portal]</span><span class="sxs-lookup"><span data-stu-id="49d44-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="49d44-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="49d44-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="49d44-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="49d44-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="49d44-108">Dans cet article, vous allez apprendre à restaurer un Azure SQL Data Warehouse à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49d44-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="49d44-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="49d44-109">Before you begin</span></span>
<span data-ttu-id="49d44-110">**Vérifiez votre capacité de DTU.**</span><span class="sxs-lookup"><span data-stu-id="49d44-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="49d44-111">Chaque SQL Data Warehouse est hébergé par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota DTU par défaut.</span><span class="sxs-lookup"><span data-stu-id="49d44-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="49d44-112">Avant de pouvoir restaurer un SQL Data Warehouse, vérifiez que le quota DTU restant sur le serveur SQL est suffisant pour la base de données en cours de restauration.</span><span class="sxs-lookup"><span data-stu-id="49d44-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="49d44-113">Pour savoir comment calculer la capacité DTU nécessaire ou pour demander davantage de capacité DTU, consultez la rubrique [Demander une modification du quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="49d44-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="49d44-114">Installer PowerShell</span><span class="sxs-lookup"><span data-stu-id="49d44-114">Install PowerShell</span></span>
<span data-ttu-id="49d44-115">Pour utiliser Azure PowerShell avec SQL Data Warehouse, vous devez installer Azure PowerShell version 1.0 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="49d44-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="49d44-116">Vous pouvez vérifier la version en exécutant **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="49d44-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="49d44-117">La version la plus récente peut être installée à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="49d44-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="49d44-118">Pour plus d’informations sur l’installation de la dernière version, consultez la page [Installation et configuration d’Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="49d44-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="49d44-119">Restauration d’une base de données active ou en pause</span><span class="sxs-lookup"><span data-stu-id="49d44-119">Restore an active or paused database</span></span>
<span data-ttu-id="49d44-120">Pour restaurer une base de données à partir d’un instantané, utilisez l’applet de commande PowerShell [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="49d44-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="49d44-121">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49d44-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="49d44-122">Connectez-vous à votre compte Azure et répertoriez tous les abonnements associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="49d44-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="49d44-123">Sélectionnez l’abonnement contenant la base de données à restaurer.</span><span class="sxs-lookup"><span data-stu-id="49d44-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="49d44-124">Répertoriez les points de restauration pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="49d44-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="49d44-125">Sélectionnez le point de restauration souhaité à l’aide de l’élément RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="49d44-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="49d44-126">Restaurez la base de données au niveau du point de restauration souhaité.</span><span class="sxs-lookup"><span data-stu-id="49d44-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="49d44-127">Vérifiez que la base de données restaurée est en ligne.</span><span class="sxs-lookup"><span data-stu-id="49d44-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="49d44-128">Une fois la restauration terminée, vous pouvez configurer votre base de données restaurée en suivant les instructions de la section [Configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="49d44-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="49d44-129">restauration d’une base de données supprimée.</span><span class="sxs-lookup"><span data-stu-id="49d44-129">Restore a deleted database</span></span>
<span data-ttu-id="49d44-130">Pour restaurer une base de données supprimée, utilisez l’applet de commande [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="49d44-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="49d44-131">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49d44-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="49d44-132">Connectez-vous à votre compte Azure et répertoriez tous les abonnements associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="49d44-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="49d44-133">Sélectionnez l’abonnement contenant la base de données supprimée à restaurer.</span><span class="sxs-lookup"><span data-stu-id="49d44-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="49d44-134">Accédez à la base de données supprimée.</span><span class="sxs-lookup"><span data-stu-id="49d44-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="49d44-135">Restaurez la base de données supprimée.</span><span class="sxs-lookup"><span data-stu-id="49d44-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="49d44-136">Vérifiez que la base de données restaurée est en ligne.</span><span class="sxs-lookup"><span data-stu-id="49d44-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="49d44-137">Une fois la restauration terminée, vous pouvez configurer votre base de données restaurée en suivant les instructions de la section [Configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="49d44-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="49d44-138">Restauration à partir d’une région géographique Azure</span><span class="sxs-lookup"><span data-stu-id="49d44-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="49d44-139">Pour récupérer une base de données, utilisez l’applet de commande [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="49d44-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="49d44-140">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49d44-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="49d44-141">Connectez-vous à votre compte Azure et répertoriez tous les abonnements associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="49d44-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="49d44-142">Sélectionnez l’abonnement contenant la base de données à restaurer.</span><span class="sxs-lookup"><span data-stu-id="49d44-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="49d44-143">Obtenez la base de données à récupérer.</span><span class="sxs-lookup"><span data-stu-id="49d44-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="49d44-144">Créez la demande de récupération de la base de données.</span><span class="sxs-lookup"><span data-stu-id="49d44-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="49d44-145">Vérifiez l’état de la base de données affectée par la géo-restauration.</span><span class="sxs-lookup"><span data-stu-id="49d44-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="49d44-146">Pour configurer votre base de données une fois la restauration terminée, consultez la page [Configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="49d44-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="49d44-147">La base de données récupérée sera compatible avec le chiffrement transparent des données si la base de données source l’est aussi.</span><span class="sxs-lookup"><span data-stu-id="49d44-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49d44-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49d44-148">Next steps</span></span>
<span data-ttu-id="49d44-149">Pour plus d’informations sur les fonctionnalités de continuité d’activité des éditions d’Azure SQL Database, consultez la rubrique [Vue d’ensemble de la continuité des activités Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="49d44-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
