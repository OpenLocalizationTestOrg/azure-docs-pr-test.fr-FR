---
title: "aaaMigrate votre entrepôt de données de tooSQL solution | Documents Microsoft"
description: Conseils de migration pour mettre votre plateforme de SQL Data Warehouse tooAzure la solution.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="1ce46-103">Migrer votre tooAzure solution SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1ce46-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="1ce46-104">Consultez les conséquences de la migration d’un tooAzure de solution de base de données SQL Data Warehouse existant.</span><span class="sxs-lookup"><span data-stu-id="1ce46-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="1ce46-105">Profiler votre charge de travail</span><span class="sxs-lookup"><span data-stu-id="1ce46-105">Profile your workload</span></span>
<span data-ttu-id="1ce46-106">Avant de migrer, vous souhaitez toobe certaine que SQL Data Warehouse est hello bonne solution pour votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="1ce46-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="1ce46-107">Entrepôt de données SQL est un analytique de tooperform système distribué conçu sur des données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="1ce46-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="1ce46-108">Migration tooSQL de l’entrepôt de données nécessite des modifications de conception qui ne sont pas toounderstand trop difficile, mais peuvent prendre quelques tooimplement de temps.</span><span class="sxs-lookup"><span data-stu-id="1ce46-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="1ce46-109">Si votre entreprise requiert un entrepôt de données d’entreprise, les avantages de hello valent effort de hello.</span><span class="sxs-lookup"><span data-stu-id="1ce46-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="1ce46-110">Toutefois, si vous n’avez pas besoin power hello d’entrepôt de données SQL, il est plus économique toouse SQL Server ou une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1ce46-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="1ce46-111">Envisagez d’utiliser SQL Data Warehouse lorsque vous :</span><span class="sxs-lookup"><span data-stu-id="1ce46-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="1ce46-112">Possédez plusieurs To de données</span><span class="sxs-lookup"><span data-stu-id="1ce46-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="1ce46-113">Plan toorun analytique sur de grandes quantités de données</span><span class="sxs-lookup"><span data-stu-id="1ce46-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="1ce46-114">Besoin de stockage et calcul de hello capacité tooscale</span><span class="sxs-lookup"><span data-stu-id="1ce46-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="1ce46-115">Choix des coûts de toosave en plaçant les ressources de calcul lorsque vous n’en avez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="1ce46-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="1ce46-116">N’utilisez pas SQL Data Warehouse pour des charges de travail opérationnelles (OLTP) qui possèdent :</span><span class="sxs-lookup"><span data-stu-id="1ce46-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="1ce46-117">Des lectures et écritures haute fréquence</span><span class="sxs-lookup"><span data-stu-id="1ce46-117">High frequency reads and writes</span></span>
- <span data-ttu-id="1ce46-118">Un grand nombre de sélections singleton</span><span class="sxs-lookup"><span data-stu-id="1ce46-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="1ce46-119">Des volumes élevés d’insertions à une seule ligne</span><span class="sxs-lookup"><span data-stu-id="1ce46-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="1ce46-120">Des besoins de traitement ligne par ligne</span><span class="sxs-lookup"><span data-stu-id="1ce46-120">Row by row processing needs</span></span>
- <span data-ttu-id="1ce46-121">Des formats incompatibles (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="1ce46-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="1ce46-122">Migration du plan de hello</span><span class="sxs-lookup"><span data-stu-id="1ce46-122">Plan hello migration</span></span>

<span data-ttu-id="1ce46-123">Une fois que vous avez décidé de toomigrate un tooSQL existant de la solution l’entrepôt de données, il est important tooplan la migration hello avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="1ce46-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="1ce46-124">Un objectif de la planification est tooensure vos données, vos schémas de table, et votre code sont compatibles avec l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="1ce46-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="1ce46-125">Il existe certaines différences de compatibilité toowork autour entre votre système actuel et l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="1ce46-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="1ce46-126">De plus, migration de grandes quantités de données tooAzure prend du temps.</span><span class="sxs-lookup"><span data-stu-id="1ce46-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="1ce46-127">Une planification minutieuse accélère la mise en route de votre tooAzure de données.</span><span class="sxs-lookup"><span data-stu-id="1ce46-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="1ce46-128">Un autre objectif de la planification est conception toomake tooensure ajustements que votre solution tire parti des performances de requête hello Qu'entrepôt de données SQL est conçu tooprovide.</span><span class="sxs-lookup"><span data-stu-id="1ce46-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="1ce46-129">Conception d’entrepôts de données pour la montée en puissance présente des modèles de conception et les méthodes traditionnelles ainsi ne sont pas toujours hello mieux.</span><span class="sxs-lookup"><span data-stu-id="1ce46-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="1ce46-130">Bien que vous pouvez apporter certaines modifications de conception après la migration, apporter des modifications plus tôt dans le processus de hello enregistrera plus tard.</span><span class="sxs-lookup"><span data-stu-id="1ce46-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="1ce46-131">tooperform une migration réussie, vous devez toomigrate vos schémas de table, votre code et vos données.</span><span class="sxs-lookup"><span data-stu-id="1ce46-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="1ce46-132">Lisez ces articles pour en apprendre davantage sur la migration :</span><span class="sxs-lookup"><span data-stu-id="1ce46-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="1ce46-133">Migration de vos schémas</span><span class="sxs-lookup"><span data-stu-id="1ce46-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="1ce46-134">Migration de votre code</span><span class="sxs-lookup"><span data-stu-id="1ce46-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="1ce46-135">[Migration de vos données](sql-data-warehouse-migrate-data.md)</span><span class="sxs-lookup"><span data-stu-id="1ce46-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="1ce46-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ce46-136">Next steps</span></span>
<span data-ttu-id="1ce46-137">Hello CAT (équipe de consultants clients) a également certaines des instructions SQL Data Warehouse excellente, ils publient via les blogs.</span><span class="sxs-lookup"><span data-stu-id="1ce46-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="1ce46-138">Examinez leur article, [tooAzure de données de migration SQL Data Warehouse dans la pratique] [ Migrating data tooAzure SQL Data Warehouse in practice] pour obtenir des conseils supplémentaires sur la migration.</span><span class="sxs-lookup"><span data-stu-id="1ce46-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
