---
title: "Portail Azure : géoréplication SQL Database | Microsoft Docs"
description: "Configurer les géo-réplication pour la base de données SQL Azure dans hello portail Azure et de basculement de lancement"
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
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="64831-103">Configurer géo-réplication active pour base de données SQL Azure hello portail Azure et de basculement de lancement</span><span class="sxs-lookup"><span data-stu-id="64831-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="64831-104">Cet article vous montre comment tooconfigure géo-réplication active pour la base de données SQL dans hello [portail Azure](http://portal.azure.com) et tooinitiate le basculement.</span><span class="sxs-lookup"><span data-stu-id="64831-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="64831-105">basculement tooinitiate avec hello portail Azure, consultez [initier un basculement planifié ou non planifié pour la base de données SQL Azure avec hello portail Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64831-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="64831-106">tooconfigure géo-réplication active à l’aide de hello portail Azure, vous devez hello suivant de ressource :</span><span class="sxs-lookup"><span data-stu-id="64831-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="64831-107">Une base de données SQL Azure : base de données primaire hello que vous souhaitez tooa tooreplicate autre région géographique.</span><span class="sxs-lookup"><span data-stu-id="64831-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="64831-108">Géo-réplication Active doit être entre bases de données Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="64831-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="64831-109">Ajout d'une base de données secondaire</span><span class="sxs-lookup"><span data-stu-id="64831-109">Add a secondary database</span></span>
<span data-ttu-id="64831-110">Hello étapes suivantes créent une nouvelle base de données secondaire dans un partenariat de géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="64831-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="64831-111">tooadd une base de données secondaire, vous devez être propriétaire de l’abonnement hello ou copropriétaire.</span><span class="sxs-lookup"><span data-stu-id="64831-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="64831-112">base de données secondaire Hello a hello même nom qu’une base de données primaire hello et a, par défaut, hello même niveau de service.</span><span class="sxs-lookup"><span data-stu-id="64831-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="64831-113">base de données secondaire Hello peut être une base de données ou d’une base de données dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="64831-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="64831-114">Pour en savoir plus, consultez [Niveaux de service](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="64831-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="64831-115">Une fois hello secondaire est créée et amorcée, données commencent à se répliquer à partir de hello base de données primaire toohello nouvelle base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="64831-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="64831-116">Si la base de données partenaire hello existe déjà (par exemple, suite à l’arrêt d’une relation de géo-réplication précédente) commande hello échoue.</span><span class="sxs-lookup"><span data-stu-id="64831-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="64831-117">Bonjour [portail Azure](http://portal.azure.com), parcourir toohello de base de données que vous souhaitez tooset pour géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="64831-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="64831-118">Sur la page de base de données SQL hello, sélectionnez **géo-réplication**, puis sélectionnez hello région toocreate hello base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="64831-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="64831-119">Vous pouvez sélectionner n’importe quelle région autre que de la région de hello hébergeant la base de données primaire hello, mais nous vous recommandons de hello [région associée](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="64831-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configuration de la géo-réplication](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="64831-121">Sélectionnez ou configurer le serveur de hello et niveau de tarification pour la base de données secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="64831-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Configuration de la base de données secondaire](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="64831-123">Si vous le souhaitez, vous pouvez ajouter un pool élastique de base de données secondaire tooan.</span><span class="sxs-lookup"><span data-stu-id="64831-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="64831-124">base de données secondaire toocreate hello dans un pool, cliquez sur **pool élastique** et sélectionnez un pool sur le serveur cible de hello.</span><span class="sxs-lookup"><span data-stu-id="64831-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="64831-125">Un pool doit déjà exister sur le serveur cible de hello.</span><span class="sxs-lookup"><span data-stu-id="64831-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="64831-126">Ce workflow ne crée pas un pool.</span><span class="sxs-lookup"><span data-stu-id="64831-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="64831-127">Cliquez sur **créer** hello tooadd secondaire.</span><span class="sxs-lookup"><span data-stu-id="64831-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="64831-128">base de données secondaire Hello est créé et hello amorçage processus commence.</span><span class="sxs-lookup"><span data-stu-id="64831-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Configuration de la base de données secondaire](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="64831-130">Lorsque hello amorçage le processus est terminé, la base de données secondaire hello affiche son état.</span><span class="sxs-lookup"><span data-stu-id="64831-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Amorçage terminé](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="64831-132">Initialisation d’un basculement</span><span class="sxs-lookup"><span data-stu-id="64831-132">Initiate a failover</span></span>

<span data-ttu-id="64831-133">base de données secondaire Hello peut être hello toobecome commuté principal.</span><span class="sxs-lookup"><span data-stu-id="64831-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="64831-134">Bonjour [portail Azure](http://portal.azure.com), parcourir la base de données primaire toohello en partenariat de géo-réplication hello.</span><span class="sxs-lookup"><span data-stu-id="64831-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="64831-135">Dans le panneau de la base de données SQL hello, sélectionnez **tous les paramètres** > **géo-réplication**.</span><span class="sxs-lookup"><span data-stu-id="64831-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="64831-136">Bonjour **secondaires** liste, sélectionnez hello base de données toobecome hello nouveau réplica principal et cliquez sur **basculement**.</span><span class="sxs-lookup"><span data-stu-id="64831-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![Basculement](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="64831-138">Cliquez sur **Oui** toobegin hello basculement.</span><span class="sxs-lookup"><span data-stu-id="64831-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="64831-139">commande Hello bascule immédiatement la base de données secondaire hello dans le rôle principal de hello.</span><span class="sxs-lookup"><span data-stu-id="64831-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="64831-140">Il existe une courte période pendant laquelle les deux bases de données ne sont pas disponibles (dans l’ordre hello de 0 seconde too25) pendant le basculement des rôles de hello.</span><span class="sxs-lookup"><span data-stu-id="64831-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="64831-141">Si la base de données primaire hello a plusieurs bases de données secondaires, commande hello automatiquement reconfigure hello autres bases de données secondaires tooconnect toohello nouveau réplica principal.</span><span class="sxs-lookup"><span data-stu-id="64831-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="64831-142">toute l’opération Hello doit prendre moins d’une minute toocomplete dans des circonstances normales.</span><span class="sxs-lookup"><span data-stu-id="64831-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="64831-143">Cette commande est conçue pour une récupération rapide de base de données hello en cas de panne.</span><span class="sxs-lookup"><span data-stu-id="64831-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="64831-144">Elle déclenche un basculement sans synchronisation des données (basculement forcé).</span><span class="sxs-lookup"><span data-stu-id="64831-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="64831-145">Si hello principal est en ligne et la validation des transactions lors de la commande hello est émise une perte de données peut se produire.</span><span class="sxs-lookup"><span data-stu-id="64831-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="64831-146">Supprimer une base de données secondaire</span><span class="sxs-lookup"><span data-stu-id="64831-146">Remove secondary database</span></span>
<span data-ttu-id="64831-147">Cette opération arrête définitivement de la base de données secondaire de toohello réplication hello et modifications hello le rôle de base de données en lecture-écriture régulière hello tooa secondaire.</span><span class="sxs-lookup"><span data-stu-id="64831-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="64831-148">Si la base de données secondaire hello connectivité toohello est rompue, commande hello réussit mais hello est secondaire ne devient en lecture-écriture jusqu'à une fois que la connectivité est rétablie.</span><span class="sxs-lookup"><span data-stu-id="64831-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="64831-149">Bonjour [portail Azure](http://portal.azure.com), parcourir la base de données primaire toohello en partenariat de géo-réplication hello.</span><span class="sxs-lookup"><span data-stu-id="64831-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="64831-150">Sur la page de base de données SQL hello, sélectionnez **géo-réplication**.</span><span class="sxs-lookup"><span data-stu-id="64831-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="64831-151">Bonjour **secondaires** liste, sélectionnez hello base de données tooremove à partir du partenariat de géo-réplication hello.</span><span class="sxs-lookup"><span data-stu-id="64831-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="64831-152">Cliquez sur **Arrêter la réplication**.</span><span class="sxs-lookup"><span data-stu-id="64831-152">Click **Stop Replication**.</span></span>
   
    ![Suppression de la base de données secondaire](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="64831-154">Une fenêtre de confirmation s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="64831-154">A confirmation window opens.</span></span> <span data-ttu-id="64831-155">Cliquez sur **Oui** tooremove hello base de données partenariat de géo-réplication hello.</span><span class="sxs-lookup"><span data-stu-id="64831-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="64831-156">(Définissez la propriété en lecture-écriture de base de données ne fait pas partie de toute réplication tooa.)</span><span class="sxs-lookup"><span data-stu-id="64831-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="64831-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64831-157">Next steps</span></span>
* <span data-ttu-id="64831-158">toolearn en savoir plus sur la géo-réplication active, consultez [géo-réplication active](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64831-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="64831-159">Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="64831-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

