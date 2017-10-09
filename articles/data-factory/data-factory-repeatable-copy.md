---
title: copie aaaRepeatable dans Azure Data Factory | Documents Microsoft
description: "Découvrez comment tooavoid doublons même si un secteur qui copie des données est exécuté plusieurs fois."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Copie répétable dans Azure Data Factory

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.  
 
> [!NOTE]
> Hello exemples suivants sont pour SQL Azure, mais banque de données applicable tooany qui prend en charge les jeux de données rectangulaire. Vous avez peut-être tooadjust hello **type** de source et hello **requête** propriété (par exemple : requête au lieu de sqlReaderQuery) pour les données de salutation stocker.   

En règle générale, lors de la lecture à partir de magasins relationnelles, vous souhaitez tooread uniquement les données de hello correspondant toothat tranche. Un moyen toodo serait donc à l’aide de hello WindowStart et WindowEnd variables système disponibles dans Azure Data Factory. En savoir plus sur les variables de hello et les fonctions dans Azure Data Factory ici Bonjour [Azure Data Factory - fonctions et Variables système](data-factory-functions-variables.md) l’article. Exemple : 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Cette requête lit les données qui se situe à partir de la table de hello MyTable hello durée de la tranche (WindowStart -> WindowEnd). Réexécutez de cette tranche s’assurent également que ce hello mêmes données sont en lecture. 

Dans d’autres cas, vous souhaiterez peut-être tooread hello totalité de la table et pouvez définir hello sqlReaderQuery comme suit :

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>Écriture REPEATABLE tooSqlSink
Lors de la copie des données trop**Azure SQL/SQL Server** provenant d’autres banques de données, vous devez l’esprit tooavoid tookeep répétabilité des résultats inattendus. 

Lors de la copie des données tooAzure base de données SQL/SQL Server, l’activité de copie hello ajoute la table de données toohello récepteur par défaut. Par exemple, vous copiez des données à partir d’un format CSV (valeurs séparées par des virgules) fichier contenant deux enregistrements toohello suivant de table dans une base de données Azure SQL/SQL Server. Lorsqu’une tranche s’exécute, hello deux enregistrements sont copiés toohello SQL table. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Supposons que vous a détecté des erreurs dans le fichier source et quantité hello du Tube vers le bas à partir de 2 too4 mise à jour. Si vous réexécutez la tranche de données hello pour cette période manuellement, vous trouverez deux nouveaux enregistrements ajoutés tooAzure base de données SQL/SQL Server. Cet exemple suppose qu’aucune des colonnes hello dans la table de hello de contrainte de clé primaire hello.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid ce comportement, vous avez besoin d’une sémantique UPSERT toospecify en utilisant l’une des hello suivant deux mécanismes :

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Mécanisme 1 : utilisation de la propriété sqlWriterCleanupScript
Vous pouvez utiliser hello **sqlWriterCleanupScript** tooclean de propriété des données à partir de la table de récepteur de hello avant l’insertion de données de hello lors de l’exécution d’une tranche. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Lorsqu’une tranche s’exécute, le script de nettoyage hello est exécuté premières données toodelete correspondant tranche toohello à partir de la table SQL de hello. activité de copie Hello insère ensuite les données dans hello Table SQL. En cas de réexécution de la tranche de hello, la quantité de hello est mise à jour comme vous le souhaitez.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Supposons que hello enregistrement de laver plat est supprimé de volume partagé de cluster hello d’origine. Puis réexécuter la tranche de hello produirait hello suivant des résultats : 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

activité de copie Hello s’exécutaient hello nettoyage script toodelete hello données correspondantes pour ce secteur. Puis il lire l’entrée de hello de csv hello (qui puis ne contenus qu’un seul enregistrement) et inséré dans la Table de hello. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Mécanisme 2 : utilisation du paramètre sliceIdentifierColumnName
> [!IMPORTANT]
> Pour le moment, le paramètre sliceIdentifierColumnName n’est pas pris en charge par Azure SQL Data Warehouse. 

répétabilité de tooachieve Hello deuxième mécanisme est en ayant une colonne dédiée (sliceIdentifierColumnName) dans la cible de hello Table. Cette colonne peut être utilisée par Azure Data Factory tooensure hello source et destination reste synchronisé. Cette approche fonctionne quand il existe une grande souplesse dans la modification ou la définition de schéma de Table SQL de destination hello. 

Cette colonne est utilisée par la fabrique de données Azure à des fins de répétabilité et dans les processus hello Azure Data Factory ne fait pas de n’importe quel schéma change toohello Table. Méthode toouse cette approche :

1. Définir une colonne de type **binary (32)** dans Table SQL de destination hello. Aucune contrainte ne doit exister sur cette colonne. Pour les besoins de cet exemple, nommons cette colonne « AdfSliceIdentifier ».


    Table source :

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Table de destination : 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Utiliser dans l’activité de copie hello comme suit :
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Azure Data Factory remplit cette colonne en fonction de son besoin tooensure hello source et destination restent synchronisés. valeurs Hello cette colonne ne doivent pas être utilisées en dehors de ce contexte. 

Toomechanism similaires 1, l’activité de copie nettoie automatiquement les données hello pour hello donné tranche à partir de destination hello Table SQL. Il insère ensuite les données à partir de la source de table de destination toohello. 

## <a name="next-steps"></a>Étapes suivantes
Passez en revue hello suivant connecteur articles pour exécuter les exemples JSON : 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)