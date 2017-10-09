---
title: "stockage en mémoire XTP aaaMonitor | Documents Microsoft"
description: "Estimer et surveiller la capacité et l’utilisation du stockage en mémoire XTP ; résoudre l’erreur de capacité 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="12f71-103">Surveiller le stockage OLTP In-Memory</span><span class="sxs-lookup"><span data-stu-id="12f71-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="12f71-104">Lorsque vous utilisez [OLTP en mémoire](sql-database-in-memory.md), les données des tables à mémoire optimisée et les variables de table résident dans un stockage OLTP en mémoire.</span><span class="sxs-lookup"><span data-stu-id="12f71-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="12f71-105">Chaque niveau de service Premium a une taille de stockage maximale OLTP en mémoire, qui est décrit dans hello [article des niveaux de Service de base de données SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="12f71-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="12f71-106">Une fois que cette limite est dépassée, des opérations d’insertion et de mise à jour peuvent commencer à échouer (en générant l’erreur 41823).</span><span class="sxs-lookup"><span data-stu-id="12f71-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="12f71-107">À ce stade serez tooeither delete tooreclaim mémoire, ou que vous mettez à niveau le niveau de performances hello de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="12f71-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="12f71-108">Déterminer si les données correspondront au sein de l’extrémité de stockage en mémoire hello</span><span class="sxs-lookup"><span data-stu-id="12f71-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="12f71-109">Déterminer l’extrémité de stockage hello : consultez hello [article des niveaux de Service de base de données SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) pour les majuscules du stockage hello des différents niveaux de service Premium hello.</span><span class="sxs-lookup"><span data-stu-id="12f71-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="12f71-110">Estimation de la configuration requise pour une table optimisée en mémoire fonctionne même hello de mémoire moyen pour SQL Server en tant qu’il effectue dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="12f71-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="12f71-111">Prenez quelques minutes tooreview cette rubrique sur [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="12f71-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="12f71-112">Notez que la table de hello et les lignes de la variable table, ainsi que les index, sont pris en compte taille des données utilisateur max hello.</span><span class="sxs-lookup"><span data-stu-id="12f71-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="12f71-113">En outre, ALTER TABLE doit suffisamment toocreate place une nouvelle version de la totalité de la table hello et ses index.</span><span class="sxs-lookup"><span data-stu-id="12f71-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="12f71-114">Surveillance et alerte</span><span class="sxs-lookup"><span data-stu-id="12f71-114">Monitoring and alerting</span></span>
<span data-ttu-id="12f71-115">Vous pouvez surveiller l’utilisation de stockage en mémoire sous forme de pourcentage de hello [cap de stockage pour votre niveau de performances](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) Bonjour Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="12f71-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="12f71-116">Dans Panneau de base de données hello, boîte de l’utilisation de ressources hello rechercher, puis cliquez sur Modifier.</span><span class="sxs-lookup"><span data-stu-id="12f71-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="12f71-117">Puis sélectionnez la métrique de hello `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="12f71-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="12f71-118">tooadd une alerte, cliquez sur Panneau métrique hello du tooopen zone hello l’utilisation des ressources, puis cliquez sur Ajouter une alerte.</span><span class="sxs-lookup"><span data-stu-id="12f71-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="12f71-119">Ou utilisez hello suivant l’utilisation du stockage en mémoire de requête tooshow hello :</span><span class="sxs-lookup"><span data-stu-id="12f71-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="12f71-120">Résoudre les situations de mémoire insuffisante - erreur 41823</span><span class="sxs-lookup"><span data-stu-id="12f71-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="12f71-121">Quand la mémoire devient insuffisante, les opérations INSERT, UPDATE et CREATE échouent en générant le message d’erreur 41823.</span><span class="sxs-lookup"><span data-stu-id="12f71-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="12f71-122">Message d’erreur 41823 indique que les tables optimisées en mémoire hello et variables de table ont dépassé la taille maximale de hello.</span><span class="sxs-lookup"><span data-stu-id="12f71-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="12f71-123">tooresolve cette erreur, soit :</span><span class="sxs-lookup"><span data-stu-id="12f71-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="12f71-124">Supprimer les données de tables mémoire optimisées de hello, tootraditional de données potentiellement déchargement hello, les tables sur disque ; ou,</span><span class="sxs-lookup"><span data-stu-id="12f71-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="12f71-125">Mise à niveau tooone de niveau de service hello stockage suffisant en mémoire pour les données de salutation, vous devez tookeep dans des tables optimisées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="12f71-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12f71-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12f71-126">Next steps</span></span>
<span data-ttu-id="12f71-127">Pour plus d’instructions sur la surveillance, consultez [Analyse de base de données SQL Azure à l’aide de vues de gestion dynamique](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
