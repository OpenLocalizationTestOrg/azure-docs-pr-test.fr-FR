---
title: "aaaSQL serveur activité de procédure stockée"
description: "Découvrez comment vous pouvez utiliser l’activité de la procédure stockée SQL Server de hello tooinvoke une procédure stockée dans une base de données SQL Azure ou d’un entrepôt de données SQL Azure à partir d’un pipeline de fabrique de données."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>Activité de procédure stockée SQL Server
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Activité Hive](data-factory-hive-activity.md) 
> * [Activité pig](data-factory-pig-activity.md)
> * [Activité MapReduce](data-factory-map-reduce.md)
> * [Activité de diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Activité Spark](data-factory-spark.md)
> * [Activité d’exécution par lot Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Activité des ressources de mise à jour de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Activité de procédure stockée](data-factory-stored-proc-activity.md)
> * [Activité U-SQL Data Lake Analytics](data-factory-usql-activity.md)
> * [Activité personnalisée .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Vue d'ensemble
Vous utilisez des activités de transformation des données dans une fabrique de données [pipeline](data-factory-create-pipelines.md) tootransform et traitent les données brutes dans des prédictions et des analyses. Hello activité de procédure stockée est une des activités de transformation hello qui prend en charge de la fabrique de données. Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge dans la fabrique de données.

Vous pouvez utiliser tooinvoke d’activité de procédure stockée hello une procédure stockée dans un des données suivantes de hello stocke dans votre entreprise ou sur une machine virtuelle Azure (VM) : 

- Base de données SQL Azure
- Azure SQL Data Warehouse
- Base de données SQL Server  Si vous utilisez SQL Server, installez la passerelle de gestion des données sur le même ordinateur que les ordinateurs hôtes hello de base de données ou sur un ordinateur distinct qui possède la base de données access toohello de hello. La passerelle de gestion des données est un composant qui connecte des sources de données locales ou se trouvant sur une machine virtuelle Azure à des services cloud de manière gérée et sécurisée. Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour plus d’informations sur la passerelle.

> [!IMPORTANT]
> Lors de la copie des données dans la base de données SQL Azure ou SQL Server, vous pouvez configurer hello **SqlSink** dans l’activité de copie tooinvoke une procédure stockée à l’aide de hello **sqlWriterStoredProcedureName** propriété. Pour plus de détails, consultez l’article [Appeler une procédure stockée à partir d’une activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md). Pour plus d’informations sur la propriété de hello, consultez suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). L’appel d’une procédure stockée lors de la copie de données dans Azure SQL Data Warehouse avec une activité de copie n’est pas pris en charge. Toutefois, vous pouvez utiliser tooinvoke activité de procédure stockée hello une procédure stockée dans un entrepôt de données SQL. 
>  
> Lors de la copie des données à partir de la base de données SQL Azure ou SQL Server ou entrepôt de données SQL Azure, vous pouvez configurer **SqlSource** dans l’activité de copie tooinvoke un tooread de données de la procédure stockée à partir de la base de données source hello à l’aide de hello  **sqlReaderStoredProcedureName** propriété. Pour plus d’informations, consultez hello suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


Hello, suivant la procédure pas à pas utilise hello activité de procédure stockée dans un pipeline de tooinvoke une procédure stockée dans une base de données SQL Azure. 

## <a name="walkthrough"></a>Procédure pas à pas
### <a name="sample-table-and-stored-procedure"></a>Exemple de table et de procédure stockée
1. Créer hello **table** dans votre base de données SQL Azure à l’aide de SQL Server Management Studio ou tout autre outil que vous êtes familiarisé avec. colonne de datetimestamp Hello est la date de hello et l’heure à laquelle le code hello correspondante est généré.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    ID est hello unique identifié et hello datetimestamp est date de hello et l’heure à laquelle le code hello correspondante est généré.
    
    ![Exemples de données](./media/data-factory-stored-proc-activity/sample-data.png)

    Dans cet exemple, la procédure stockée hello est dans une base de données SQL Azure. Si hello procédure stockée est dans un entrepôt de données SQL Azure et de la base de données SQL Server, l’approche de hello est similaire. Pour une base de données SQL Server, vous devez installer une [passerelle de gestion des données](data-factory-data-management-gateway.md).
2. Créer hello **procédure stockée** qui insère des données dans toohello **sampletable**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Nom** et **casse** Hello paramètre (DateTime dans cet exemple) doit correspondre à celui du paramètre spécifié dans le pipeline/activité hello JSON. Dans hello la définition de procédure stockée, vérifiez que  **@**  est utilisé en tant que préfixe pour le paramètre hello.

### <a name="create-a-data-factory"></a>Créer une fabrique de données
1. Connectez-vous trop[portail Azure](https://portal.azure.com/).
2. Cliquez sur **nouveau** sur menu gauche hello **Intelligence + Analytique**, puis cliquez sur **Data Factory**.

    ![Nouvelle fabrique de données](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. Bonjour **nouvelle fabrique de données** panneau, entrez **SProcDF** pour hello nom. Les noms Azure Data Factory sont **globalement uniques**. Vous avez besoin de nom de hello tooprefix hello fabrique de données avec votre nom, tooenable hello réussi la création de la fabrique de hello.

   ![Nouvelle fabrique de données](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Sélectionnez votre **abonnement Azure**.
5. Pour **groupe de ressources**, effectuez l’une des hello comme suit :
   1. Cliquez sur **nouvel** et entrez un nom pour le groupe de ressources hello.
   2. Cliquez sur **Utiliser l’existant** et sélectionnez un groupe de ressources existant.  
6. Sélectionnez hello **emplacement** de fabrique de données hello.
7. Sélectionnez **toodashboard du code confidentiel** afin que vous puissiez voir fabrique de données hello sur le tableau de bord hello prochaine ouverture de session dans.
8. Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.
9. Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure. Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données.

   ![Page d’accueil Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Créer un service lié Azure SQL
Après avoir créé la fabrique de données hello, vous créez un service lié SQL Azure qui lie votre base de données SQL Azure, qui contient la table de sampletable hello et sp_sample stockées procédure, fabrique de données tooyour.

1. Cliquez sur **auteur et déployer** sur hello **Data Factory** panneau pour **SProcDF** toolaunch hello éditeur Data Factory.
2. Cliquez sur **nouveau magasin de données** hello de barre de commandes et choisissez **base de données SQL Azure**. Vous devez voir le service dans l’éditeur de hello de lié hello script JSON pour la création d’une SQL Azure.

   ![Nouveau magasin de données](media/data-factory-stored-proc-activity/new-data-store.png)
3. Bonjour script JSON, apportez hello modifications suivantes :

   1. Remplacez `<servername>` par nom hello de votre serveur de base de données SQL Azure.
   2. Remplacez `<databasename>` avec la base de données hello dans lequel vous avez créé la table de hello et hello la procédure stockée.
   3. Remplacez `<username@servername>` avec un compte d’utilisateur hello qui possède la base de données access toohello.
   4. Remplacez `<password>` avec mot de passe hello hello compte d’utilisateur.

      ![Nouveau magasin de données](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy hello service lié, cliquez sur **déployer** sur la barre de commandes hello. Vérifiez que vous voyez hello AzureSqlLinkedService dans l’arborescence de hello afficher à gauche de hello.

    ![arborescence avec service lié](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Créer un jeu de données de sortie
Vous devez spécifier qu'un jeu de données de sortie pour une activité de procédure stockée même si la procédure stockée de hello ne produit pas de données. C'est-à-dire, car son hello la sortie de dataset qui gère la planification hello d’activité hello (la fréquence à laquelle hello exécution activité - toutes les heures, tous les jours, etc.). Hello dataset de sortie doit utiliser un **service lié** qui fait référence tooan de base de données SQL Azure ou d’un entrepôt de données SQL Azure ou d’une base de données SQL Server dans lequel vous souhaitez hello toorun de procédure stockée. Hello dataset de sortie puisse agir comme un moyen toopass hello de résultats de la procédure stockée hello pour un traitement ultérieur par une autre activité ([chaînage des propriétés des activités](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) dans le pipeline de hello. Toutefois, la fabrique de données n’écrit pas automatiquement sortie hello d’un dataset toothis de procédure stockée. Il est hello table SQL tooa écritures hello points de jeu de données de sortie à procédure stockée. Dans certains cas, le jeu de données de sortie hello peut être un **dataset factice** (un dataset qui pointe tooa table qui ne possède pas vraiment le résultat de hello ou procédure stockée). Ce jeu de données factice est utilisée uniquement de l’activité de procédure stockée de toospecify hello planification de l’exécution hello. 

1. Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** dans la barre d’outils de hello, cliquez sur **nouveau dataset**, puis cliquez sur **SQL Azure**. **Nouveau jeu de données** sur commande hello barre et sélectionnez **SQL Azure**.

    ![arborescence avec service lié](media/data-factory-stored-proc-activity/new-dataset.png)
2. Copiez-collez hello script JSON dans l’éditeur JSON toohello suivant.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello du jeu de données, cliquez sur **déployer** sur la barre de commandes hello. Vérifiez que vous voyez hello le jeu de données dans l’arborescence hello.

    ![arborescence avec services liés](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Créer un pipeline avec une activité SqlServerStoredProcedure
Nous allons maintenant créer un pipeline avec une activité de procédure stockée. 

Notez hello propriétés suivantes : 

- Hello **type** propriété a la valeur trop**SqlServerStoredProcedure**. 
- Hello **storedProcedureName** dans le type de propriétés est défini trop**sp_sample** (nom de hello ou procédure stockée).
- Hello **storedProcedureParameters** section contient un paramètre nommé **DataTime**. Nom et la casse du paramètre hello dans JSON doivent correspondre au nom de hello et de la casse du paramètre hello dans la définition de la procédure stockée hello. Si vous avez besoin de passer null pour un paramètre, utilisez la syntaxe de hello : `"param1": null` (tout en minuscules).
 
1. Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** hello de barre de commandes et cliquez sur **nouveau pipeline**.
2. Copier/coller hello suivant extrait de code JSON :   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. pipeline de hello toodeploy, cliquez sur **déployer** sur la barre d’outils hello.  

### <a name="monitor-hello-pipeline"></a>Pipeline d’analyse hello
1. Cliquez sur **X** tooclose éditeur Data Factory panneaux et toonavigate Panneau de fabrique de données toohello de sauvegarde, puis cliquez sur **diagramme**.

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. Bonjour **vue de diagramme**, vous voyez une vue d’ensemble des pipelines de hello et les datasets utilisés dans ce didacticiel.

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. Dans la vue de diagramme de hello, double-cliquez sur hello dataset `sprocsampleout`. Vous voyez les tranches hello dans l’état Ready. Il doit être cinq tranches, car une tranche est produite pour chaque heure entre l’heure de début hello et l’heure de fin de hello JSON.

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Lorsqu’une tranche est dans **prêt** état, exécutez un `select * from sampletable` requête sur tooverify de base de données SQL Azure hello qui hello de données a été inséré dans la table de toohello par la procédure stockée hello.

   ![Données de sortie](./media/data-factory-stored-proc-activity/output.png)

   Consultez [pipeline d’analyse hello](data-factory-monitor-manage-pipelines.md) pour plus d’informations sur la surveillance des pipelines d’Azure Data Factory.  


## <a name="specify-an-input-dataset"></a>Spécifier un jeu de données d’entrée
Procédure pas à pas de hello, activité de procédure stockée n’a pas les jeux de données d’entrée. Si vous spécifiez un jeu de données d’entrée, hello activité de procédure stockée ne s’exécute pas jusqu'à ce que la tranche hello du jeu de données d’entrée est disponible (prêt). Hello dataset peut être un jeu de données externe (qui n’est pas produit par une autre activité Bonjour même pipeline) ou un jeu de données interne qui est généré par une activité en amont (activité hello qui s’exécute avant cette activité). Vous pouvez spécifier plusieurs jeux de données d’entrée pour l’activité de procédure stockée hello. Si vous le faites, hello activité de procédure stockée s’exécute uniquement quand toutes les tranches de jeu de données d’entrée hello sont disponibles (dans l’état prêt). Hello de jeu de données d’entrée ne peut pas être utilisé dans la procédure stockée hello en tant que paramètre. Il est uniquement des dépendances hello toocheck utilisé avant l’activité de procédure stockée de départ hello.

## <a name="chaining-with-other-activities"></a>Chaînage avec d’autres activités
Si vous souhaitez toochain une activité en amont avec cette activité, spécifiez la sortie hello d’activité en amont hello en tant qu’entrée de cette activité. Lorsque vous procédez ainsi, hello activité de procédure stockée ne s’exécute pas avant l’achèvement d’activité en amont hello et hello dataset de sortie de l’activité en amont hello est disponible (en état « prêt »). Vous pouvez spécifier des jeux de données de sortie de plusieurs activités en amont en tant que jeux de données d’entrée de l’activité de procédure stockée hello. Lorsque vous procédez ainsi, à l’activité de procédure stockée de hello s’exécute uniquement quand toutes les tranches de jeu de données d’entrée hello sont disponibles.  

Dans l’exemple suivant de hello, sortie hello de l’activité de copie hello est : activité de procédure stockée de OutputDataset, qui est une entrée de hello. Par conséquent, hello activité de procédure stockée ne s’exécute pas avant l’achèvement de l’activité de copie hello et la tranche de OutputDataset hello est disponible (prêt). Si vous spécifiez plusieurs jeux de données d’entrée, hello activité de procédure stockée ne s’exécute pas jusqu'à ce que toutes les tranches de jeu de données d’entrée hello sont disponibles (dans l’état prêt). Hello de jeux de données d’entrée ne peut pas être utilisé directement en tant qu’activité de procédure stockée de toohello de paramètres. 

Pour plus d’informations sur le chaînage des activités, consultez [Plusieurs activités dans un pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

De même, toolink hello magasin activité de procédure avec **activités en aval** (activités hello exécutent une fois terminée hello activité de procédure stockée), spécifiez le dataset de sortie hello d’activité de procédure stockée hello comme un entrée de l’activité en aval hello dans le pipeline de hello.

> [!IMPORTANT]
> Lors de la copie des données dans la base de données SQL Azure ou SQL Server, vous pouvez configurer hello **SqlSink** dans l’activité de copie tooinvoke une procédure stockée à l’aide de hello **sqlWriterStoredProcedureName** propriété. Pour plus de détails, consultez l’article [Appeler une procédure stockée à partir d’une activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md). Pour plus d’informations sur la propriété de hello, consultez hello suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> Lors de la copie des données à partir de la base de données SQL Azure ou SQL Server ou entrepôt de données SQL Azure, vous pouvez configurer **SqlSource** dans l’activité de copie tooinvoke un tooread de données de la procédure stockée à partir de la base de données source hello à l’aide de hello  **sqlReaderStoredProcedureName** propriété. Pour plus d’informations, consultez hello suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>Format JSON
Voici le format JSON de hello pour définir une activité de procédure stockée :

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Hello tableau suivant décrit ces propriétés JSON :

| Propriété | Description | Requis |
| --- | --- | --- |
| name | Nom de l’activité hello |Oui |
| description |Texte qui décrit quelle activité hello est utilisé pour |Non |
| type | Doit être défini sur **SqlServerStoredProcedure** | Oui |
| inputs | facultatif. Si vous ne spécifiez pas un jeu de données d’entrée, il doit être disponible (en état « Prêt ») pour hello stockées toorun d’activité de procédure. Hello de jeu de données d’entrée ne peut pas être utilisé dans la procédure stockée hello en tant que paramètre. Il est uniquement des dépendances hello toocheck utilisé avant l’activité de procédure stockée de départ hello. |Non |
| outputs | Vous devez spécifier un jeu de données de sortie pour une activité de procédure stockée. Dataset de sortie spécifie hello **planification** pour hello stockées activité de procédure (horaire, hebdomadaire, mensuelle, etc.). <br/><br/>Hello dataset de sortie doit utiliser un **service lié** qui fait référence tooan de base de données SQL Azure ou d’un entrepôt de données SQL Azure ou d’une base de données SQL Server dans lequel vous souhaitez hello toorun de procédure stockée. <br/><br/>Hello dataset de sortie puisse agir comme un moyen toopass hello de résultats de la procédure stockée hello pour un traitement ultérieur par une autre activité ([chaînage des propriétés des activités](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) dans le pipeline de hello. Toutefois, la fabrique de données n’écrit pas automatiquement sortie hello d’un dataset toothis de procédure stockée. Il est hello table SQL tooa écritures hello points de jeu de données de sortie à procédure stockée. <br/><br/>Dans certains cas, le jeu de données de sortie hello peut être un **dataset factice**, qui est utilisé uniquement de l’activité de procédure stockée de toospecify hello planification de l’exécution hello. |Oui |
| storedProcedureName |Spécifiez le nom hello de procédure stockée hello dans la base de données SQL Azure hello ou base de données Azure SQL Data Warehouse ou SQL Server qui est représenté par le service hello lié hello utilisations de table de sortie. |Oui |
| storedProcedureParameters |Spécifiez les valeurs des paramètres de procédure stockée. Si vous avez besoin de toopass null pour un paramètre, utilisez la syntaxe de hello : « param1 » : null (toutes les minuscules). Consultez hello suivant toolearn exemple sur l’utilisation de cette propriété. |Non |

## <a name="passing-a-static-value"></a>Transmission d’une valeur statique
Maintenant, prenons l’exemple d’ajout d’une autre colonne nommée « Scénario » dans la table hello contenant une valeur statique est appelée « Exemple de Document ».

![Exemple de données 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Table :**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Procédure stockée**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

À présent, passez hello **scénario** activité de procédure stockée de valeur de paramètre et hello de hello. Hello **typeProperties** section Bonjour précédent exemple ressemble hello suivant extrait de code :

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Jeu de données Data Factory :**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline Data Factory**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```