---
title: "aaaUse étiquettes tooinstrument des requêtes dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils pour l’utilisation de requêtes de tooinstrument étiquettes dans l’entrepôt de données SQL Azure pour développer des solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="a61a0-103">Utiliser les requêtes de tooinstrument d’étiquettes dans l’entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="a61a0-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="a61a0-104">SQL Data Warehouse prend en charge le concept de « libellé de requête ».</span><span class="sxs-lookup"><span data-stu-id="a61a0-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="a61a0-105">Avant de l’étudier plus avant, voici un exemple parlant :</span><span class="sxs-lookup"><span data-stu-id="a61a0-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="a61a0-106">Cette dernière ligne des étiquettes requête toohello de hello chaîne « Mes requêtes étiquette ».</span><span class="sxs-lookup"><span data-stu-id="a61a0-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="a61a0-107">Cela est particulièrement utile comme étiquette de hello est requête obtenue via hello DMV.</span><span class="sxs-lookup"><span data-stu-id="a61a0-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="a61a0-108">Cela nous donne un tootrack mécanisme vers le bas de requêtes à problème et également toohelp identifier sa progression via une exécution du processus ETL.</span><span class="sxs-lookup"><span data-stu-id="a61a0-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="a61a0-109">À ce niveau, une convention d’affectation de noms efficace s’avère très utile.</span><span class="sxs-lookup"><span data-stu-id="a61a0-109">A good naming convention really helps here.</span></span> <span data-ttu-id="a61a0-110">Par exemple, quelque chose comme « projet : procédure : instruction : commentaire ' serait identifier toouniquely requête hello dans la liste de tout code hello dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="a61a0-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="a61a0-111">toosearch par l’étiquette que vous pouvez utiliser hello suivant la requête qui utilise hello des vues de gestion dynamique :</span><span class="sxs-lookup"><span data-stu-id="a61a0-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="a61a0-112">Il est essentiel d’encapsuler des crochets ou des guillemets doubles autour d’étiquette du mot hello lors de l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="a61a0-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="a61a0-113">En effet, le libellé est un mot réservé. Il entraîne une erreur s’il n’est pas délimité.</span><span class="sxs-lookup"><span data-stu-id="a61a0-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a61a0-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a61a0-114">Next steps</span></span>
<span data-ttu-id="a61a0-115">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="a61a0-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
