---
title: vues aaaUsing T-SQL dans Azure SQL Data Warehouse | Documents Microsoft
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
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="864e4-103">Vues proposées par SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="864e4-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="864e4-104">Les vues sont particulièrement utiles dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="864e4-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="864e4-105">Ils peuvent être utilisés dans un certain nombre de façons différentes tooimprove hello de qualité de votre solution.</span><span class="sxs-lookup"><span data-stu-id="864e4-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="864e4-106">Cet article présente quelques exemples de comment tooenrich votre solution avec les vues, ainsi que des limitations hello nécessitant toobe pris en compte.</span><span class="sxs-lookup"><span data-stu-id="864e4-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="864e4-107">La syntaxe de `CREATE VIEW` n’est pas abordée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="864e4-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="864e4-108">Reportez-vous toohello [CREATE VIEW] [ CREATE VIEW] l’article sur MSDN pour obtenir ces informations de référence.</span><span class="sxs-lookup"><span data-stu-id="864e4-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="864e4-109">Abstraction architecturale</span><span class="sxs-lookup"><span data-stu-id="864e4-109">Architectural abstraction</span></span>
<span data-ttu-id="864e4-110">Un modèle très courant de l’application est toore-créer des tables à l’aide de CREATE TABLE AS sélectionnez (SACT) suivi d’un objet renommer le modèle pendant le chargement de données.</span><span class="sxs-lookup"><span data-stu-id="864e4-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="864e4-111">exemple Hello ci-dessous ajoute la dimension de date tooa date nouveaux enregistrements.</span><span class="sxs-lookup"><span data-stu-id="864e4-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="864e4-112">Notez comment un nouveau tableau, DimDate_New, est créé et ensuite renommé la version d’origine de hello tooreplace de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="864e4-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="864e4-113">Toutefois, cette approche peut provoquer l’apparition et la disparition de table d’une vue utilisateur, ainsi que l’affichage de messages d’erreur de type « la table n’existe pas ».</span><span class="sxs-lookup"><span data-stu-id="864e4-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="864e4-114">Les vues peuvent être des utilisateurs de tooprovide utilisé avec une couche de présentation cohérent tandis que les objets sous-jacents hello sont renommés.</span><span class="sxs-lookup"><span data-stu-id="864e4-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="864e4-115">En fournissant aux utilisateurs un accès toohello des données via une vue, signifie que les utilisateurs n’ont besoin de visibilité toohave de tables sous-jacentes de hello.</span><span class="sxs-lookup"><span data-stu-id="864e4-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="864e4-116">Cela fournit une expérience utilisateur cohérente, tout en garantissant que les concepteurs d’entrepôts de données hello peuvent évolue au modèle de données hello et optimiser les performances à l’aide de SACT pendant le processus de chargement des données de salutation.</span><span class="sxs-lookup"><span data-stu-id="864e4-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="864e4-117">Optimisation des performances</span><span class="sxs-lookup"><span data-stu-id="864e4-117">Performance optimization</span></span>
<span data-ttu-id="864e4-118">Vues peuvent également être des jointures de performance optimisée tooenforce utilisé entre les tables.</span><span class="sxs-lookup"><span data-stu-id="864e4-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="864e4-119">Par exemple, une vue peut incorporer une clé de répartition redondant dans le cadre de hello toominimize déplacement des données dans les critères de jointure.</span><span class="sxs-lookup"><span data-stu-id="864e4-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="864e4-120">Un autre avantage d’une vue peut être tooforce une requête spécifique ou un indicateur de jointure.</span><span class="sxs-lookup"><span data-stu-id="864e4-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="864e4-121">À l’aide des vues de cette façon garantit que les jointures sont toujours effectuées en évitant recours hello pour la construction correcte de hello tooremember les utilisateurs pour les jointures de manière optimale.</span><span class="sxs-lookup"><span data-stu-id="864e4-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="864e4-122">Limites</span><span class="sxs-lookup"><span data-stu-id="864e4-122">Limitations</span></span>
<span data-ttu-id="864e4-123">Dans SQL Data Warehouse, les vues concernent uniquement les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="864e4-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="864e4-124">Par conséquent hello options suivantes n’est pas disponible :</span><span class="sxs-lookup"><span data-stu-id="864e4-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="864e4-125">Il n’existe aucune option de liaison de schéma.</span><span class="sxs-lookup"><span data-stu-id="864e4-125">There is no schema binding option</span></span>
* <span data-ttu-id="864e4-126">Tables de base ne peut pas être mis à jour via la vue de hello</span><span class="sxs-lookup"><span data-stu-id="864e4-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="864e4-127">Vous ne pouvez pas créer des vues sur des tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="864e4-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="864e4-128">Aucune prise en charge pour hello développer / indicateurs de NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="864e4-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="864e4-129">SQL Data Warehouse n’inclut aucune vue indexée.</span><span class="sxs-lookup"><span data-stu-id="864e4-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="864e4-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="864e4-130">Next steps</span></span>
<span data-ttu-id="864e4-131">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="864e4-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="864e4-132">Pour `CREATE VIEW` syntaxe, consultez trop[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="864e4-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
