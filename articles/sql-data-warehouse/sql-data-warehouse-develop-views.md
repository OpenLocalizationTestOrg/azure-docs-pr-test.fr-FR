---
title: Utilisation des vues T-SQL dans Azure SQL Data Warehouse | Microsoft Docs
description: "Conseils relatifs à l’utilisation de vues Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="50fd4-103">Vues proposées par SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="50fd4-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="50fd4-104">Les vues sont particulièrement utiles dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="50fd4-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="50fd4-105">Vous pouvez les utiliser de différentes façons, afin d’améliorer la qualité de votre solution.</span><span class="sxs-lookup"><span data-stu-id="50fd4-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="50fd4-106">Cet article met en évidence quelques exemples montrant comment enrichir votre solution avec des vues, ainsi que les limites à prendre en considération.</span><span class="sxs-lookup"><span data-stu-id="50fd4-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="50fd4-107">La syntaxe de `CREATE VIEW` n’est pas abordée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="50fd4-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="50fd4-108">Consultez l’article [CREATE VIEW][CREATE VIEW] sur MSDN pour obtenir ces informations de référence.</span><span class="sxs-lookup"><span data-stu-id="50fd4-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="50fd4-109">Abstraction architecturale</span><span class="sxs-lookup"><span data-stu-id="50fd4-109">Architectural abstraction</span></span>
<span data-ttu-id="50fd4-110">Un des modèles d’application les plus courants consiste à recréer des tables au moyen de la commande CREATE TABLE AS SELECT (CTAS), suivie d’un modèle de changement de nom d’un objet, lors du chargement des données.</span><span class="sxs-lookup"><span data-stu-id="50fd4-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="50fd4-111">L’exemple ci-dessous permet d’ajouter de nouveaux enregistrements de date à une dimension de date.</span><span class="sxs-lookup"><span data-stu-id="50fd4-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="50fd4-112">Notez comment un nouvel objet, DimDate_New, est d’abord créé et ensuite renommé pour remplacer la version d’origine de la table.</span><span class="sxs-lookup"><span data-stu-id="50fd4-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="50fd4-113">Toutefois, cette approche peut provoquer l’apparition et la disparition de table d’une vue utilisateur, ainsi que l’affichage de messages d’erreur de type « la table n’existe pas ».</span><span class="sxs-lookup"><span data-stu-id="50fd4-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="50fd4-114">Vous pouvez utiliser des vues pour fournir aux utilisateurs une couche de présentation cohérente alors que les objets sous-jacents sont renommés.</span><span class="sxs-lookup"><span data-stu-id="50fd4-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="50fd4-115">Grâce à la mise à disposition d’un accès aux données via une vue, les utilisateurs n’ont pas besoin d’afficher les tables sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="50fd4-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="50fd4-116">Ainsi, l’expérience utilisateur est plus cohérente ; les concepteurs d’entrepôts de données peuvent faire évoluer le modèle de données tout en optimisant les performances, en exécutant la commande CTAS lors du processus de chargement des données.</span><span class="sxs-lookup"><span data-stu-id="50fd4-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="50fd4-117">Optimisation des performances</span><span class="sxs-lookup"><span data-stu-id="50fd4-117">Performance optimization</span></span>
<span data-ttu-id="50fd4-118">Une vue peut également être utilisée pour mettre en place des jointures plus performantes entre les tables.</span><span class="sxs-lookup"><span data-stu-id="50fd4-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="50fd4-119">Ainsi, une vue peut inclure une clé de distribution redondante parmi ses critères de jointure, afin de réduire le nombre de déplacements de données.</span><span class="sxs-lookup"><span data-stu-id="50fd4-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="50fd4-120">Elle peut également permettre de forcer une indication de jointure ou de requête spécifique.</span><span class="sxs-lookup"><span data-stu-id="50fd4-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="50fd4-121">Utiliser des vues de cette manière permet de garantir que les jointures sont toujours effectuées de façon optimale en évitant d’avoir à se souvenir de leur construction correcte.</span><span class="sxs-lookup"><span data-stu-id="50fd4-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="50fd4-122">Limitations</span><span class="sxs-lookup"><span data-stu-id="50fd4-122">Limitations</span></span>
<span data-ttu-id="50fd4-123">Dans SQL Data Warehouse, les vues concernent uniquement les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="50fd4-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="50fd4-124">De ce fait, les options suivantes ne sont pas disponibles :</span><span class="sxs-lookup"><span data-stu-id="50fd4-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="50fd4-125">Il n’existe aucune option de liaison de schéma.</span><span class="sxs-lookup"><span data-stu-id="50fd4-125">There is no schema binding option</span></span>
* <span data-ttu-id="50fd4-126">Les tables de base ne peuvent pas être mises à jour par le biais de la vue.</span><span class="sxs-lookup"><span data-stu-id="50fd4-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="50fd4-127">Vous ne pouvez pas créer des vues sur des tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="50fd4-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="50fd4-128">Les indications EXPAND/NOEXPAND ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="50fd4-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="50fd4-129">SQL Data Warehouse n’inclut aucune vue indexée.</span><span class="sxs-lookup"><span data-stu-id="50fd4-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="50fd4-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50fd4-130">Next steps</span></span>
<span data-ttu-id="50fd4-131">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="50fd4-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="50fd4-132">Pour la syntaxe de `CREATE VIEW`, consultez [CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="50fd4-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
