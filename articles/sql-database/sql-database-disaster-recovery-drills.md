---
title: "Exercices de récupération d’urgence de SQL Database | Microsoft Docs"
description: "Découvrez des conseils et des meilleures pratiques en matière d’utilisation de la base de données Azure SQL pour effectuer des exercices de récupération d’urgence qui vous aideront à maintenir la résistance aux pannes de vos applications métier stratégiques en cas de défaillances."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="313a1-103">Exécution d'un exercice de récupération d'urgence</span><span class="sxs-lookup"><span data-stu-id="313a1-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="313a1-104">Nous recommandons de valider régulièrement la préparation des applications à la récupération.</span><span class="sxs-lookup"><span data-stu-id="313a1-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="313a1-105">La vérification du comportement de l'application et des implications en matière de pertes de données et/ou d'interruptions en cas basculement constitue une bonne pratique.</span><span class="sxs-lookup"><span data-stu-id="313a1-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="313a1-106">Il s'agit également d'une exigence figurant dans la plupart des normes industrielles dans le cadre d'une certification de la continuité des activités.</span><span class="sxs-lookup"><span data-stu-id="313a1-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="313a1-107">L'exécution d'un exercice de récupération d'urgence comprend :</span><span class="sxs-lookup"><span data-stu-id="313a1-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="313a1-108">la simulation d'une défaillance des couches de données</span><span class="sxs-lookup"><span data-stu-id="313a1-108">Simulating data tier outage</span></span>
* <span data-ttu-id="313a1-109">la récupération</span><span class="sxs-lookup"><span data-stu-id="313a1-109">Recovering</span></span>
* <span data-ttu-id="313a1-110">la validation de l'intégrité des applications après la récupération</span><span class="sxs-lookup"><span data-stu-id="313a1-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="313a1-111">Le flux de travail à exécuter peut varier en fonction de la [conception de votre application pour la continuité des activités](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="313a1-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="313a1-112">Ci-dessous, vous trouverez une description des meilleures pratiques en matière d'exécution d'un exercice de récupération d'urgence dans le contexte de bases de données Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="313a1-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="313a1-113">Géo-restauration</span><span class="sxs-lookup"><span data-stu-id="313a1-113">Geo-restore</span></span>
<span data-ttu-id="313a1-114">Pour éviter une perte de données potentielle lors d'un exercice de récupération d'urgence, nous vous recommandons d'effectuer l'exercice à dans un environnement de test en créant une copie de l'environnement de production et en l'utilisant pour vérifier le flux de travail de basculement de l'application.</span><span class="sxs-lookup"><span data-stu-id="313a1-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="313a1-115">Simulation d'une défaillance</span><span class="sxs-lookup"><span data-stu-id="313a1-115">Outage simulation</span></span>
<span data-ttu-id="313a1-116">Pour simuler la défaillance, vous pouvez supprimer ou renommer la base de données source.</span><span class="sxs-lookup"><span data-stu-id="313a1-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="313a1-117">Cela entraîne des échecs de connexion de l’application.</span><span class="sxs-lookup"><span data-stu-id="313a1-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="313a1-118">Récupérer</span><span class="sxs-lookup"><span data-stu-id="313a1-118">Recovery</span></span>
* <span data-ttu-id="313a1-119">Effectuez la géorestauration de la base de données sur un autre serveur, comme décrit [ici](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="313a1-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="313a1-120">Modifiez la configuration de l’application pour établir une connexion aux bases de données récupérées, puis suivez le guide [Configurer une base de données après récupération](sql-database-disaster-recovery.md) pour achever la récupération.</span><span class="sxs-lookup"><span data-stu-id="313a1-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="313a1-121">Validation</span><span class="sxs-lookup"><span data-stu-id="313a1-121">Validation</span></span>
* <span data-ttu-id="313a1-122">Achevez l’exercice de récupération en vérifiant l’intégrité des applications après la récupération (notamment, chaînes de connexion, connexions, test des fonctionnalités de base ou autres validations faisant partie de procédures d’approbations d’applications standard).</span><span class="sxs-lookup"><span data-stu-id="313a1-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="313a1-123">Géoréplication</span><span class="sxs-lookup"><span data-stu-id="313a1-123">Geo-replication</span></span>
<span data-ttu-id="313a1-124">Pour une base de données protégée à l’aide de la géoréplication, l’exercice implique un basculement planifié vers la base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="313a1-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="313a1-125">Le basculement planifié garantit que les bases de données principale et secondaire restent synchronisées lorsque les rôles sont permutés.</span><span class="sxs-lookup"><span data-stu-id="313a1-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="313a1-126">À la différence du basculement non planifié, cette opération n’entraîne pas de perte de données. L’exercice peut donc être exécuté dans l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="313a1-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="313a1-127">Simulation d'une défaillance</span><span class="sxs-lookup"><span data-stu-id="313a1-127">Outage simulation</span></span>
<span data-ttu-id="313a1-128">Pour simuler la défaillance, vous pouvez désactiver l’application web ou une machine virtuelle connectée à la base de données.</span><span class="sxs-lookup"><span data-stu-id="313a1-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="313a1-129">Cela entraîne des échecs de connectivité des clients web.</span><span class="sxs-lookup"><span data-stu-id="313a1-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="313a1-130">Récupérer</span><span class="sxs-lookup"><span data-stu-id="313a1-130">Recovery</span></span>
* <span data-ttu-id="313a1-131">Vérifiez que la configuration de l’application dans la région de récupération d’urgence pointe vers l’ancienne base de données secondaire qui devient la nouvelle base de données primaire entièrement accessible.</span><span class="sxs-lookup"><span data-stu-id="313a1-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="313a1-132">Exécutez un [basculement planifié](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) pour que la base de données secondaire devienne la nouvelle base de données primaire.</span><span class="sxs-lookup"><span data-stu-id="313a1-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="313a1-133">Suivez le guide [Configure a database after recovery](sql-database-disaster-recovery.md) pour effectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="313a1-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="313a1-134">Validation</span><span class="sxs-lookup"><span data-stu-id="313a1-134">Validation</span></span>
* <span data-ttu-id="313a1-135">Achevez l’exercice de récupération en vérifiant l’intégrité des applications après la récupération (notamment, chaînes de connexion, connexions, test des fonctionnalités de base ou autres validations faisant partie de procédures d’approbations d’applications standard).</span><span class="sxs-lookup"><span data-stu-id="313a1-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="313a1-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="313a1-136">Next steps</span></span>
* <span data-ttu-id="313a1-137">Pour en savoir plus sur les scénarios de continuité d’activités, consultez [Scénarios de continuité des activités](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="313a1-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="313a1-138">Pour en savoir plus sur les sauvegardes automatisées d’une base de données SQL Azure, consultez [Sauvegardes automatisées d’une base de données SQL](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="313a1-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="313a1-139">Pour en savoir plus sur l’utilisation des sauvegardes automatisées pour la récupération, consultez [Restaurer une base de données à partir des sauvegardes initiées par le service](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="313a1-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="313a1-140">Pour découvrir des options de récupération plus rapides, voir [Géoréplication active](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="313a1-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
