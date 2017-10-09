---
title: "les schémas définis par l’aaaUser dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’utilisation de schémas Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="895da-103">Schémas définis par l’utilisateur dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="895da-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="895da-104">Entrepôts de données traditionnels souvent utiliser des bases de données toocreate des limites d’application en fonction de la charge de travail ou de domaine sécurité.</span><span class="sxs-lookup"><span data-stu-id="895da-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="895da-105">Par exemple, un entrepôt de données SQL Server classique peut inclure une base de données de la zone de transit, une base de données de l’entrepôt de données et quelques bases de données de mini-Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="895da-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="895da-106">Dans cette topologie, chaque base de données fonctionne comme une charge de travail et la limite de sécurité dans l’architecture de hello.</span><span class="sxs-lookup"><span data-stu-id="895da-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="895da-107">En revanche, SQL Data Warehouse exécute la charge de travail entrepôt de données entière hello au sein d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="895da-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="895da-108">Les jointures entre plusieurs bases de données ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="895da-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="895da-109">Par conséquent, SQL Data Warehouse attend que toutes les tables utilisées par toobe d’entrepôt hello stockée dans une base de données de hello.</span><span class="sxs-lookup"><span data-stu-id="895da-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="895da-110">SQL Data Warehouse ne prend pas en charge les requêtes de base de données croisées, de quelque nature que ce soit.</span><span class="sxs-lookup"><span data-stu-id="895da-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="895da-111">Par conséquent, les implémentations de l’entrepôt de données qui tirent parti de ce modèle devez toobe révisée.</span><span class="sxs-lookup"><span data-stu-id="895da-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="895da-112">Recommandations</span><span class="sxs-lookup"><span data-stu-id="895da-112">Recommendations</span></span>
<span data-ttu-id="895da-113">Tenez compte des recommandations lorsque vous consolidez des limites de charge de travail, fonctionnelles, de domaine et de sécurité :</span><span class="sxs-lookup"><span data-stu-id="895da-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="895da-114">Utilisez un toorun de base de données SQL Data Warehouse votre charge de travail de l’entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="895da-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="895da-115">Consolider vos données entrepôt environnement toouse un entrepôt de données SQL base de données existante</span><span class="sxs-lookup"><span data-stu-id="895da-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="895da-116">Tirer parti de la **schémas définis par l’utilisateur** tooprovide limite de hello précédemment implémentée à l’aide de bases de données.</span><span class="sxs-lookup"><span data-stu-id="895da-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="895da-117">Si aucun schéma défini par l’utilisateur n’a été utilisé précédemment, vous repartez de zéro.</span><span class="sxs-lookup"><span data-stu-id="895da-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="895da-118">Utiliser simplement vos schémas définis par l’utilisateur dans la base de données SQL Data Warehouse hello ancien nom de base de données hello comme base de hello.</span><span class="sxs-lookup"><span data-stu-id="895da-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="895da-119">Si les schémas ont été déjà utilisés, vous disposez de différentes options :</span><span class="sxs-lookup"><span data-stu-id="895da-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="895da-120">Supprimer des noms de schéma hérité hello et mettre à jour</span><span class="sxs-lookup"><span data-stu-id="895da-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="895da-121">Conserver les noms de schéma hérité hello par nom de table hello préalable en attente schéma hérité nom toohello</span><span class="sxs-lookup"><span data-stu-id="895da-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="895da-122">Conserver les noms de schéma hérité hello en implémentant des vues sur table hello dans un schéma supplémentaire de toore-créer une structure de schéma ancien hello.</span><span class="sxs-lookup"><span data-stu-id="895da-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="895da-123">Inspection première option 3 peut sembler comme option de hello plus attrayante.</span><span class="sxs-lookup"><span data-stu-id="895da-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="895da-124">Toutefois, les diable hello sont en détail hello.</span><span class="sxs-lookup"><span data-stu-id="895da-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="895da-125">Les vues sont en lecture seule dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="895da-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="895da-126">Toute modification de données ou de table doivent toobe effectuée sur la table de base hello.</span><span class="sxs-lookup"><span data-stu-id="895da-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="895da-127">Par ailleurs, cette troisième option présente une couche de vues au sein de votre système.</span><span class="sxs-lookup"><span data-stu-id="895da-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="895da-128">Vous pourriez toogive cette une réflexion supplémentaire si vous utilisez déjà des vues dans votre architecture.</span><span class="sxs-lookup"><span data-stu-id="895da-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="895da-129">Exemples :</span><span class="sxs-lookup"><span data-stu-id="895da-129">Examples:</span></span>
<span data-ttu-id="895da-130">Implémentation de schémas définis par l’utilisateur basés sur des noms de base de données</span><span class="sxs-lookup"><span data-stu-id="895da-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="895da-131">Conserver schéma hérité en attente avant les nomme toohello nom de la table.</span><span class="sxs-lookup"><span data-stu-id="895da-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="895da-132">Utilisez des schémas pour les limites de charge de travail hello.</span><span class="sxs-lookup"><span data-stu-id="895da-132">Use schemas for hello workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="895da-133">Conservation des noms de schémas hérités via des vues</span><span class="sxs-lookup"><span data-stu-id="895da-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="895da-134">Toute modification de la stratégie de schéma a besoin d’une revue hello du modèle de sécurité pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="895da-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="895da-135">Dans de nombreux cas, vous pouvez être toosimplify en mesure de modèle de sécurité de hello en assignant des autorisations au niveau du schéma hello.</span><span class="sxs-lookup"><span data-stu-id="895da-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="895da-136">S’il vous faut des autorisations plus granulaires, vous pouvez utiliser des rôles de base de données.</span><span class="sxs-lookup"><span data-stu-id="895da-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="895da-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="895da-137">Next steps</span></span>
<span data-ttu-id="895da-138">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="895da-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
