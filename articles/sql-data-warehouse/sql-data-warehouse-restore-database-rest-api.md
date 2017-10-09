---
title: "aaaRestore un entrepôt de données SQL Azure (API REST) | Documents Microsoft"
description: "Tâches d’API REST permettant de restaurer un Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="d9a45-103">Restauration d’un Azure SQL Data Warehouse (API REST)</span><span class="sxs-lookup"><span data-stu-id="d9a45-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="d9a45-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="d9a45-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="d9a45-105">[Portail][Portal]</span><span class="sxs-lookup"><span data-stu-id="d9a45-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="d9a45-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="d9a45-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="d9a45-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="d9a45-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="d9a45-108">Dans cet article, vous allez apprendre comment toorestore un à l’aide de l’entrepôt de données SQL Azure hello API REST.</span><span class="sxs-lookup"><span data-stu-id="d9a45-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d9a45-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d9a45-109">Before you begin</span></span>
<span data-ttu-id="d9a45-110">**Vérifiez votre capacité de DTU.**</span><span class="sxs-lookup"><span data-stu-id="d9a45-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="d9a45-111">Chaque SQL Data Warehouse est hébergé par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota DTU par défaut.</span><span class="sxs-lookup"><span data-stu-id="d9a45-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="d9a45-112">Avant de pouvoir restaurer un entrepôt de données SQL, vérifiez que hello que votre SQL server dispose d’assez restantes du quota UDBD pour base de données hello en cours de restauration.</span><span class="sxs-lookup"><span data-stu-id="d9a45-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="d9a45-113">toolearn comment toocalculate DTU nécessaire ou toorequest plus DTU, consultez [demander une modification du quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="d9a45-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="d9a45-114">Restauration d’une base de données active ou en pause</span><span class="sxs-lookup"><span data-stu-id="d9a45-114">Restore an active or paused database</span></span>
<span data-ttu-id="d9a45-115">toorestore une base de données :</span><span class="sxs-lookup"><span data-stu-id="d9a45-115">toorestore a database:</span></span>

1. <span data-ttu-id="d9a45-116">Obtenir la liste de hello des points de restauration de base de données à l’aide d’opération de Points de restauration de base de données de Get hello.</span><span class="sxs-lookup"><span data-stu-id="d9a45-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="d9a45-117">Commencer la restauration à l’aide de hello [demande de restauration de base de données de création] [ Create database restore request] opération.</span><span class="sxs-lookup"><span data-stu-id="d9a45-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="d9a45-118">Suivi hello de la restauration à l’aide de hello [état de l’opération de base de données] [ Database operation status] opération.</span><span class="sxs-lookup"><span data-stu-id="d9a45-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="d9a45-119">Une fois la restauration de hello est terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="d9a45-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="d9a45-120">restauration d’une base de données supprimée.</span><span class="sxs-lookup"><span data-stu-id="d9a45-120">Restore a deleted database</span></span>
<span data-ttu-id="d9a45-121">toorestore une base de données supprimée :</span><span class="sxs-lookup"><span data-stu-id="d9a45-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="d9a45-122">Répertorier toutes les bases de données supprimées pouvant être restaurée à l’aide de hello [pouvant être restaurée de la liste des bases de données supprimées] [ List restorable dropped databases] opération.</span><span class="sxs-lookup"><span data-stu-id="d9a45-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="d9a45-123">Obtenir les détails de hello pour hello supprimé base de données toorestore à l’aide de hello [Get peuvent être restaurée supprimé la base de données] [ Get restorable dropped database] opération.</span><span class="sxs-lookup"><span data-stu-id="d9a45-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="d9a45-124">Commencer la restauration à l’aide de hello [demande de restauration de base de données de création] [ Create database restore request] opération.</span><span class="sxs-lookup"><span data-stu-id="d9a45-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="d9a45-125">Suivi hello de la restauration à l’aide de hello [état de l’opération de base de données] [ Database operation status] opération.</span><span class="sxs-lookup"><span data-stu-id="d9a45-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="d9a45-126">consultez de votre base de données après restauration de hello, tooconfigure [configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="d9a45-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d9a45-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9a45-127">Next steps</span></span>
<span data-ttu-id="d9a45-128">toolearn sur les fonctionnalités de continuité d’activité d’entreprise hello des éditions de base de données SQL Azure, lisez hello [vue d’ensemble de base de données SQL Azure business la continuité des activités][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="d9a45-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
