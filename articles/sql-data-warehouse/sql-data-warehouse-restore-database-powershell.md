---
title: "aaaRestore un entrepôt de données SQL Azure (PowerShell) | Documents Microsoft"
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
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="084ab-103">Restauration d’un Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="084ab-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="084ab-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="084ab-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="084ab-105">[Portail][Portal]</span><span class="sxs-lookup"><span data-stu-id="084ab-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="084ab-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="084ab-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="084ab-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="084ab-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="084ab-108">Dans cet article, vous allez apprendre comment toorestore un Azure SQL Data Warehouse à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="084ab-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="084ab-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="084ab-109">Before you begin</span></span>
<span data-ttu-id="084ab-110">**Vérifiez votre capacité de DTU.**</span><span class="sxs-lookup"><span data-stu-id="084ab-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="084ab-111">Chaque SQL Data Warehouse est hébergé par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota DTU par défaut.</span><span class="sxs-lookup"><span data-stu-id="084ab-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="084ab-112">Avant de pouvoir restaurer un entrepôt de données SQL, vérifiez que hello que votre SQL server dispose d’assez restantes du quota UDBD pour base de données hello en cours de restauration.</span><span class="sxs-lookup"><span data-stu-id="084ab-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="084ab-113">toolearn comment toocalculate DTU nécessaire ou toorequest plus DTU, consultez [demander une modification du quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="084ab-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="084ab-114">Installer PowerShell</span><span class="sxs-lookup"><span data-stu-id="084ab-114">Install PowerShell</span></span>
<span data-ttu-id="084ab-115">Dans l’ordre toouse Azure PowerShell avec l’entrepôt de données SQL, vous devez tooinstall Azure PowerShell version 1.0 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="084ab-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="084ab-116">Vous pouvez vérifier la version en exécutant **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="084ab-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="084ab-117">version la plus récente Hello peut être installée à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="084ab-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="084ab-118">Pour plus d’informations sur l’installation de version la plus récente hello, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="084ab-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="084ab-119">Restauration d’une base de données active ou en pause</span><span class="sxs-lookup"><span data-stu-id="084ab-119">Restore an active or paused database</span></span>
<span data-ttu-id="084ab-120">une base de données à partir d’un instantané de toorestore utiliser hello [restauration-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="084ab-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="084ab-121">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="084ab-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="084ab-122">Se connecter tooyour compte Azure et répertorier tous les abonnements hello associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="084ab-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="084ab-123">Sélectionnez l’abonnement hello contenant hello toobe de base de données restaurée.</span><span class="sxs-lookup"><span data-stu-id="084ab-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="084ab-124">Hello de la liste des points de la base de données hello de restauration.</span><span class="sxs-lookup"><span data-stu-id="084ab-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="084ab-125">Choisissez un point de restauration hello souhaité à l’aide de hello RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="084ab-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="084ab-126">Point de restauration toohello souhaité hello de base de données de restauration.</span><span class="sxs-lookup"><span data-stu-id="084ab-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="084ab-127">Vérifiez que cette base de données hello restaurée est en ligne.</span><span class="sxs-lookup"><span data-stu-id="084ab-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="084ab-128">Une fois la restauration de hello est terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="084ab-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="084ab-129">restauration d’une base de données supprimée.</span><span class="sxs-lookup"><span data-stu-id="084ab-129">Restore a deleted database</span></span>
<span data-ttu-id="084ab-130">toorestore une base de données supprimée, utilisez hello [restauration-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] applet de commande.</span><span class="sxs-lookup"><span data-stu-id="084ab-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="084ab-131">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="084ab-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="084ab-132">Se connecter tooyour compte Azure et répertorier tous les abonnements hello associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="084ab-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="084ab-133">Sélectionnez l’abonnement hello contenant hello supprimé toobe de base de données restaurée.</span><span class="sxs-lookup"><span data-stu-id="084ab-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="084ab-134">Obtenir de la base de données spécifique de hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="084ab-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="084ab-135">Restaurer la base de données de hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="084ab-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="084ab-136">Vérifiez que cette base de données hello restaurée est en ligne.</span><span class="sxs-lookup"><span data-stu-id="084ab-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="084ab-137">Une fois la restauration de hello est terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="084ab-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="084ab-138">Restauration à partir d’une région géographique Azure</span><span class="sxs-lookup"><span data-stu-id="084ab-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="084ab-139">toorecover une base de données, utilisez hello [restauration-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] applet de commande.</span><span class="sxs-lookup"><span data-stu-id="084ab-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="084ab-140">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="084ab-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="084ab-141">Se connecter tooyour compte Azure et répertorier tous les abonnements hello associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="084ab-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="084ab-142">Sélectionnez l’abonnement hello contenant hello toobe de base de données restaurée.</span><span class="sxs-lookup"><span data-stu-id="084ab-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="084ab-143">Obtenir des toorecover hello base de données.</span><span class="sxs-lookup"><span data-stu-id="084ab-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="084ab-144">Créer la demande de récupération hello pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="084ab-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="084ab-145">Vérifiez l’état hello de base de données de géo-restauration hello.</span><span class="sxs-lookup"><span data-stu-id="084ab-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="084ab-146">consultez de votre base de données après restauration de hello, tooconfigure [configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="084ab-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="084ab-147">base de données récupérée Hello sera activée de chiffrement transparent des données à si la base de données source hello est activé de chiffrement transparent des données.</span><span class="sxs-lookup"><span data-stu-id="084ab-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="084ab-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="084ab-148">Next steps</span></span>
<span data-ttu-id="084ab-149">toolearn sur les fonctionnalités de continuité d’activité d’entreprise hello des éditions de base de données SQL Azure, lisez hello [vue d’ensemble de base de données SQL Azure business la continuité des activités][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="084ab-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
