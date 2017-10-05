---
title: "Restauration d’un entrepôt Azure SQL Data Warehouse (API REST) | Microsoft Docs"
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
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="2c714-103">Restauration d’un Azure SQL Data Warehouse (API REST)</span><span class="sxs-lookup"><span data-stu-id="2c714-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2c714-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="2c714-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="2c714-105">[Portail][Portal]</span><span class="sxs-lookup"><span data-stu-id="2c714-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="2c714-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2c714-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="2c714-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="2c714-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="2c714-108">Dans cet article, vous allez apprendre à restaurer un Azure SQL Data Warehouse à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="2c714-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2c714-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2c714-109">Before you begin</span></span>
<span data-ttu-id="2c714-110">**Vérifiez votre capacité de DTU.**</span><span class="sxs-lookup"><span data-stu-id="2c714-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="2c714-111">Chaque SQL Data Warehouse est hébergé par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota DTU par défaut.</span><span class="sxs-lookup"><span data-stu-id="2c714-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="2c714-112">Avant de pouvoir restaurer un SQL Data Warehouse, vérifiez que le quota DTU restant sur le serveur SQL est suffisant pour la base de données en cours de restauration.</span><span class="sxs-lookup"><span data-stu-id="2c714-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="2c714-113">Pour savoir comment calculer la capacité DTU nécessaire ou pour demander davantage de capacité DTU, consultez la rubrique [Demander une modification du quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="2c714-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="2c714-114">Restauration d’une base de données active ou en pause</span><span class="sxs-lookup"><span data-stu-id="2c714-114">Restore an active or paused database</span></span>
<span data-ttu-id="2c714-115">Pour restaurer une base de données :</span><span class="sxs-lookup"><span data-stu-id="2c714-115">To restore a database:</span></span>

1. <span data-ttu-id="2c714-116">Suivez la procédure d’obtention de la liste des points de restauration de la base de données.</span><span class="sxs-lookup"><span data-stu-id="2c714-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="2c714-117">Lancez la restauration en suivant la procédure [Création d’une demande de restauration de base de données][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="2c714-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="2c714-118">Surveillez l’état de la restauration en suivant la procédure [Statut d’opération de base de données][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="2c714-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="2c714-119">Une fois la restauration terminée, vous pouvez configurer votre base de données restaurée en suivant les instructions de la section [Configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="2c714-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="2c714-120">restauration d’une base de données supprimée.</span><span class="sxs-lookup"><span data-stu-id="2c714-120">Restore a deleted database</span></span>
<span data-ttu-id="2c714-121">Pour restaurer une base de données supprimée :</span><span class="sxs-lookup"><span data-stu-id="2c714-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="2c714-122">Obtenez la liste de toutes vos bases de données supprimées pouvant être restaurées en suivant la procédure [Liste des bases de données supprimées pouvant être restaurées][List restorable dropped databases].</span><span class="sxs-lookup"><span data-stu-id="2c714-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="2c714-123">Obtenez des informations détaillées sur la base de données que vous voulez restaurer en suivant la procédure [Obtention de base de données supprimée pouvant être restaurée][Get restorable dropped database].</span><span class="sxs-lookup"><span data-stu-id="2c714-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="2c714-124">Lancez la restauration en suivant la procédure [Création d’une demande de restauration de base de données][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="2c714-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="2c714-125">Surveillez l’état de la restauration en suivant la procédure [Statut d’opération de base de données][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="2c714-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="2c714-126">Pour configurer votre base de données une fois la restauration terminée, consultez la page [Configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="2c714-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2c714-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c714-127">Next steps</span></span>
<span data-ttu-id="2c714-128">Pour plus d’informations sur les fonctionnalités de continuité d’activité des éditions d’Azure SQL Database, consultez la rubrique [Vue d’ensemble de la continuité des activités Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="2c714-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
