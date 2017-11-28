---
title: "Portail Azure : géoréplication SQL Database | Microsoft Docs"
description: "Configurer la géoréplication pour Azure SQL Database dans le portail Azure et initier le basculement"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="01d95-103">Configurer la géoréplication active pour Azure SQL Database dans le portail Azure et initier le basculement</span><span class="sxs-lookup"><span data-stu-id="01d95-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="01d95-104">Cet article montre comment configurer la géoréplication active pour SQL Database dans le [portail Azure](http://portal.azure.com) et initier le basculement.</span><span class="sxs-lookup"><span data-stu-id="01d95-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="01d95-105">Pour lancer un basculement avec le portail Azure, consultez [Lancer un basculement planifié ou non planifié pour une base de données SQL Azure avec le portail Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="01d95-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="01d95-106">Pour configurer la géo-réplication active à l’aide du portail Azure, vous devez disposer des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="01d95-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="01d95-107">Une Azure SQL Database : la base de données primaire que vous souhaitez répliquer vers une autre région géographique.</span><span class="sxs-lookup"><span data-stu-id="01d95-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="01d95-108">La géo-réplication active doit être entre des bases de données au sein du même abonnement.</span><span class="sxs-lookup"><span data-stu-id="01d95-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="01d95-109">Ajout d'une base de données secondaire</span><span class="sxs-lookup"><span data-stu-id="01d95-109">Add a secondary database</span></span>
<span data-ttu-id="01d95-110">Les étapes suivantes créent une nouvelle base de données secondaire dans un partenariat géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="01d95-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="01d95-111">Pour ajouter une base de données secondaire, vous devez être le propriétaire ou copropriétaire de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="01d95-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="01d95-112">La base de données secondaire a le même nom que la base de données primaire et, par défaut, le même niveau de service.</span><span class="sxs-lookup"><span data-stu-id="01d95-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="01d95-113">La base de données secondaire peut être une base de données autonome ou une base de données dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="01d95-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="01d95-114">Pour en savoir plus, consultez [Niveaux de service](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="01d95-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="01d95-115">Une fois la base de données secondaire créée et amorcée, une réplication des données de la base de données primaire vers la base de données secondaire commence.</span><span class="sxs-lookup"><span data-stu-id="01d95-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="01d95-116">Si la base de données partenaire existe déjà (par exemple, suite à l’arrêt d’une relation de géo-réplication précédente), la commande échoue.</span><span class="sxs-lookup"><span data-stu-id="01d95-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="01d95-117">Dans le [portail Azure](http://portal.azure.com), accédez à la base de données que vous souhaitez configurer pour la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="01d95-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="01d95-118">Dans la page SQL Database, sélectionnez **Géoréplication**, puis choisissez la région dans laquelle créer la base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="01d95-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="01d95-119">Bien que vous puissiez sélectionner n’importe quelle région autre que la région qui héberge la base de données primaire, nous vous recommandons de sélectionner la [région jumelée](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="01d95-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configuration de la géo-réplication](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="01d95-121">Sélectionnez ou configurez le serveur et le niveau tarifaire pour la base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="01d95-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Configuration de la base de données secondaire](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="01d95-123">Si vous le souhaitez, vous pouvez ajouter une base de données secondaire à un pool données élastique.</span><span class="sxs-lookup"><span data-stu-id="01d95-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="01d95-124">Pour créer la base de données secondaire dans un pool, cliquez sur **Pool élastique**, puis sélectionnez un pool sur le serveur cible.</span><span class="sxs-lookup"><span data-stu-id="01d95-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="01d95-125">Un pool doit déjà exister sur le serveur cible.</span><span class="sxs-lookup"><span data-stu-id="01d95-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="01d95-126">Ce workflow ne crée pas un pool.</span><span class="sxs-lookup"><span data-stu-id="01d95-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="01d95-127">Cliquez sur **créer** pour ajouter la base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="01d95-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="01d95-128">La base de données secondaire est créée et le processus d’amorçage commence.</span><span class="sxs-lookup"><span data-stu-id="01d95-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![Configuration de la base de données secondaire](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="01d95-130">Lorsque le processus d’amorçage est terminé, la base de données secondaire affiche son état.</span><span class="sxs-lookup"><span data-stu-id="01d95-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Amorçage terminé](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="01d95-132">Initialisation d’un basculement</span><span class="sxs-lookup"><span data-stu-id="01d95-132">Initiate a failover</span></span>

<span data-ttu-id="01d95-133">La base de données secondaire peut être basculée en base de données primaire.</span><span class="sxs-lookup"><span data-stu-id="01d95-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="01d95-134">Dans le [portail Azure](http://portal.azure.com), accédez à la base de données primaire dans le partenariat de géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="01d95-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="01d95-135">Dans le panneau SQL Database, sélectionnez **Tous les paramètres** > **Géoréplication**.</span><span class="sxs-lookup"><span data-stu-id="01d95-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="01d95-136">Dans la liste **SECONDAIRES**, sélectionnez la base de données qui doit devenir la nouvelle base primaire et cliquez sur **Basculement**.</span><span class="sxs-lookup"><span data-stu-id="01d95-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![Basculement](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="01d95-138">Cliquez sur **Oui** pour commencer le basculement.</span><span class="sxs-lookup"><span data-stu-id="01d95-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="01d95-139">La commande fait immédiatement basculer la base de données secondaire vers le rôle primaire.</span><span class="sxs-lookup"><span data-stu-id="01d95-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="01d95-140">Il existe une courte période pendant laquelle les deux bases de données ne sont pas disponibles (de l’ordre de 0 à 25 secondes) pendant que les rôles sont activés.</span><span class="sxs-lookup"><span data-stu-id="01d95-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="01d95-141">Si la base de données primaire comporte plusieurs bases de données secondaires, la commande reconfigure automatiquement les autres bases de données secondaires pour qu’elles se connectent à la nouvelle base de données primaire.</span><span class="sxs-lookup"><span data-stu-id="01d95-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="01d95-142">Toute l’opération devrait prendre moins d’une minute pour se terminer dans des circonstances normales.</span><span class="sxs-lookup"><span data-stu-id="01d95-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="01d95-143">Cette commande est conçue pour récupérer rapidement la base de données en cas de panne.</span><span class="sxs-lookup"><span data-stu-id="01d95-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="01d95-144">Elle déclenche un basculement sans synchronisation des données (basculement forcé).</span><span class="sxs-lookup"><span data-stu-id="01d95-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="01d95-145">Si la base de données primaire est en ligne et valide des transactions lorsque la commande est émise, une perte de données peut se produire.</span><span class="sxs-lookup"><span data-stu-id="01d95-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="01d95-146">Supprimer une base de données secondaire</span><span class="sxs-lookup"><span data-stu-id="01d95-146">Remove secondary database</span></span>
<span data-ttu-id="01d95-147">Cette opération arrête définitivement la réplication vers la base de données secondaire et modifie le rôle de la base de données secondaire en une base de données normale accessible en lecture et en écriture.</span><span class="sxs-lookup"><span data-stu-id="01d95-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="01d95-148">Si la connectivité à la base de données secondaire est interrompue, la commande aboutit, mais la base de données secondaire ne passe pas en mode lecture-écriture une fois la connectivité rétablie.</span><span class="sxs-lookup"><span data-stu-id="01d95-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="01d95-149">Dans le [portail Azure](http://portal.azure.com), accédez à la base de données primaire dans le partenariat de géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="01d95-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="01d95-150">Dans la page SQL Database, sélectionnez **Géoréplication**.</span><span class="sxs-lookup"><span data-stu-id="01d95-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="01d95-151">Dans la liste des bases de données **SECONDAIRES**, sélectionnez la base de données que vous souhaitez supprimer du partenariat de géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="01d95-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="01d95-152">Cliquez sur **Arrêter la réplication**.</span><span class="sxs-lookup"><span data-stu-id="01d95-152">Click **Stop Replication**.</span></span>
   
    ![Suppression de la base de données secondaire](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="01d95-154">Une fenêtre de confirmation s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="01d95-154">A confirmation window opens.</span></span> <span data-ttu-id="01d95-155">Cliquez sur **Oui** pour supprimer la base de données de partenariat de géo-réplication</span><span class="sxs-lookup"><span data-stu-id="01d95-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="01d95-156">(définissez-la sur une base de données en lecture-écriture ne faisant pas partie d’une réplication).</span><span class="sxs-lookup"><span data-stu-id="01d95-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="01d95-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01d95-157">Next steps</span></span>
* <span data-ttu-id="01d95-158">Pour plus d’informations sur la géoréplication active, voir [Géoréplication active](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01d95-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="01d95-159">Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="01d95-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

