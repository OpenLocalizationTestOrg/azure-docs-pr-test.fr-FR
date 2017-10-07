---
title: effectue une boucle aaaLeverage T-SQL dans Azure SQL Data Warehouse | Documents Microsoft
description: "Conseils relatifs à l’utilisation de boucles Transact-SQL et au remplacement de curseurs dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>Boucles dans SQL Data Warehouse
Entrepôt de données SQL prend en charge hello [pendant][tandis que] une boucle pour l’exécution répétée de blocs d’instructions. Il en sera de tant que hello spécifiée conditions sont remplies ou jusqu'à ce que les code hello termine spécifiquement boucle hello à l’aide de hello `BREAK` (mot clé). Les boucles sont particulièrement utiles pour remplacer des curseurs définis dans le code SQL. Heureusement, presque tous les curseurs qui sont écrits dans le code SQL sont Hello rapide, en lecture uniquement diverses. Par conséquent [tandis que] boucles sont une alternative intéressante si vous vous trouvez ayant tooreplace une.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Valorisation de boucles et remplacement de curseurs dans SQL Data Warehouse
Toutefois, avant d’examiner en tête tout d’abord vous devez vous poser hello suivant la question : « ce curseur peut être réécrit toouse des opérations basées sur ? ». Dans de nombreux cas, les réponses hello seront Oui et sont souvent hello meilleure approche. Une opération basée sur un jeu s’exécute généralement beaucoup plus rapidement qu’une méthode itérative de type ligne par ligne.

Les curseurs à avance rapide et en lecture seule peuvent facilement être remplacés par des constructions en boucle. Voici un exemple simple. Cet exemple de code met à jour les statistiques de hello pour chaque table dans la base de données hello. En effectuant une itération sur les tables de hello de boucle de hello nous est en mesure de tooexecute chaque commande dans la séquence.

Commencez par créer une table temporaire contenant une ligne unique numéro utilisé tooidentify hello des instructions individuelles :

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

En second lieu, initialiser boucle de hello hello variables tooperform requis :

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Ensuite, effectuez une boucle avec les instructions, en les exécutant l’une après l’autre :

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Enfin drop table temporaire de hello créée dans la première étape de hello

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble sur le développement][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[tandis que]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
