---
title: "Schémas définis par l’utilisateur dans SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="c6d43-103">Schémas définis par l’utilisateur dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c6d43-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="c6d43-104">Les entrepôts de données traditionnels utilisent souvent des bases de données distinctes pour créer des limites d’application basées sur la charge de travail, le domaine ou la sécurité.</span><span class="sxs-lookup"><span data-stu-id="c6d43-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="c6d43-105">Par exemple, un entrepôt de données SQL Server classique peut inclure une base de données de la zone de transit, une base de données de l’entrepôt de données et quelques bases de données de mini-Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6d43-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="c6d43-106">Dans cette topologie, chaque base de données joue le rôle d’étendue de sécurité et de charge de travail dans l’architecture.</span><span class="sxs-lookup"><span data-stu-id="c6d43-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="c6d43-107">À l’inverse, SQL Data Warehouse exécute l’intégralité de la charge de travail des entrepôts de données au sein d’une seule et même base de données.</span><span class="sxs-lookup"><span data-stu-id="c6d43-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="c6d43-108">Les jointures entre plusieurs bases de données ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="c6d43-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="c6d43-109">Par conséquent, SQL Data Warehouse s’attend que l’ensemble des tables utilisées par l’entrepôt soient stockées au sein d’une seule et même base de données.</span><span class="sxs-lookup"><span data-stu-id="c6d43-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="c6d43-110">SQL Data Warehouse ne prend pas en charge les requêtes de base de données croisées, de quelque nature que ce soit.</span><span class="sxs-lookup"><span data-stu-id="c6d43-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="c6d43-111">Par conséquent, les implémentations d’entrepôt de données tirant parti de ce modèle devront être modifiées.</span><span class="sxs-lookup"><span data-stu-id="c6d43-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="c6d43-112">Recommandations</span><span class="sxs-lookup"><span data-stu-id="c6d43-112">Recommendations</span></span>
<span data-ttu-id="c6d43-113">Tenez compte des recommandations lorsque vous consolidez des limites de charge de travail, fonctionnelles, de domaine et de sécurité :</span><span class="sxs-lookup"><span data-stu-id="c6d43-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="c6d43-114">Utilisez une base de données SQL Data Warehouse pour exécuter l’intégralité de la charge de travail des entrepôts de données.</span><span class="sxs-lookup"><span data-stu-id="c6d43-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="c6d43-115">Consolidez l’environnement d’entrepôt de données existant de manière à utiliser une seule base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6d43-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="c6d43-116">Tirez parti de **schémas définis par l’utilisateur** pour fournir la limite précédemment implémentée via des bases de données.</span><span class="sxs-lookup"><span data-stu-id="c6d43-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="c6d43-117">Si aucun schéma défini par l’utilisateur n’a été utilisé précédemment, vous repartez de zéro.</span><span class="sxs-lookup"><span data-stu-id="c6d43-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="c6d43-118">Il vous suffit d’utiliser l’ancien nom de base de données en tant que base pour vos schémas définis par l’utilisateur dans la base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6d43-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="c6d43-119">Si les schémas ont été déjà utilisés, vous disposez de différentes options :</span><span class="sxs-lookup"><span data-stu-id="c6d43-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="c6d43-120">Vous pouvez supprimer les noms de schéma hérités et recommencer de zéro.</span><span class="sxs-lookup"><span data-stu-id="c6d43-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="c6d43-121">Vous pouvez conserver le nom de schéma hérité, et ajouter ce dernier au nom de la table.</span><span class="sxs-lookup"><span data-stu-id="c6d43-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="c6d43-122">Vous pouvez conserver le nom de schéma hérité, en implémentant les vues sur la table au sein d’un schéma supplémentaire pour recréer l’ancienne structure du schéma.</span><span class="sxs-lookup"><span data-stu-id="c6d43-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="c6d43-123">À première vue, la troisième option semble la plus tentante.</span><span class="sxs-lookup"><span data-stu-id="c6d43-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="c6d43-124">Toutefois, si on l’étudie plus en détail, elle ne semble pas à la hauteur de ses promesses.</span><span class="sxs-lookup"><span data-stu-id="c6d43-124">However, the devil is in the detail.</span></span> <span data-ttu-id="c6d43-125">Les vues sont en lecture seule dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6d43-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="c6d43-126">Toute modification portant sur les données ou la table doit être effectuée sur la table de base.</span><span class="sxs-lookup"><span data-stu-id="c6d43-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="c6d43-127">Par ailleurs, cette troisième option présente une couche de vues au sein de votre système.</span><span class="sxs-lookup"><span data-stu-id="c6d43-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="c6d43-128">Peut-être devriez-vous étudier la question plus attentivement si vous utilisez déjà des vues dans votre architecture.</span><span class="sxs-lookup"><span data-stu-id="c6d43-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="c6d43-129">Exemples :</span><span class="sxs-lookup"><span data-stu-id="c6d43-129">Examples:</span></span>
<span data-ttu-id="c6d43-130">Implémentation de schémas définis par l’utilisateur basés sur des noms de base de données</span><span class="sxs-lookup"><span data-stu-id="c6d43-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="c6d43-131">Conservation du nom de schéma hérité et ajout au nom de la table ;</span><span class="sxs-lookup"><span data-stu-id="c6d43-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="c6d43-132">utilisation de schémas pour la limite de charge de travail</span><span class="sxs-lookup"><span data-stu-id="c6d43-132">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="c6d43-133">Conservation des noms de schémas hérités via des vues</span><span class="sxs-lookup"><span data-stu-id="c6d43-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="c6d43-134">Toute modification portant sur la stratégie de schéma nécessite une révision du modèle de sécurité de la base de données.</span><span class="sxs-lookup"><span data-stu-id="c6d43-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="c6d43-135">Dans de nombreux cas, il est possible de simplifier le modèle de sécurité en attribuant des autorisations au niveau du schéma.</span><span class="sxs-lookup"><span data-stu-id="c6d43-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="c6d43-136">S’il vous faut des autorisations plus granulaires, vous pouvez utiliser des rôles de base de données.</span><span class="sxs-lookup"><span data-stu-id="c6d43-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c6d43-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6d43-137">Next steps</span></span>
<span data-ttu-id="c6d43-138">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="c6d43-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
