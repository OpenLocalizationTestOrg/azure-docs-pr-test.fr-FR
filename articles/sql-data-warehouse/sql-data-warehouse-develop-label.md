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
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>Utiliser les requêtes de tooinstrument d’étiquettes dans l’entrepôt de données SQL
SQL Data Warehouse prend en charge le concept de « libellé de requête ». Avant de l’étudier plus avant, voici un exemple parlant :

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

Cette dernière ligne des étiquettes requête toohello de hello chaîne « Mes requêtes étiquette ». Cela est particulièrement utile comme étiquette de hello est requête obtenue via hello DMV. Cela nous donne un tootrack mécanisme vers le bas de requêtes à problème et également toohelp identifier sa progression via une exécution du processus ETL.

À ce niveau, une convention d’affectation de noms efficace s’avère très utile. Par exemple, quelque chose comme « projet : procédure : instruction : commentaire ' serait identifier toouniquely requête hello dans la liste de tout code hello dans le contrôle de code source.

toosearch par l’étiquette que vous pouvez utiliser hello suivant la requête qui utilise hello des vues de gestion dynamique :

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> Il est essentiel d’encapsuler des crochets ou des guillemets doubles autour d’étiquette du mot hello lors de l’interrogation. En effet, le libellé est un mot réservé. Il entraîne une erreur s’il n’est pas délimité.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
