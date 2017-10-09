---
title: "aaaMove des données à partir de la Table Web à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment toomove les données d’une table dans un site Web page à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Déplacer des données depuis une source de table web à l’aide d’Azure Data Factory
Cet article décrit comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une table dans une page Web de tooa prises en charge le magasin de données récepteur. Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article qui présente une vue d’ensemble du déplacement des données avec la liste des activités et hello copie de banques de données pris en charge en tant que sources/récepteurs.

Fabrique de données prend en charge uniquement déplacer les données à partir de données Web table tooother stocke, mais ne pas déplacer les données à partir d’autres données stocke à destination de table tooa Web.

> [!IMPORTANT]
> Pour l’instant, ce connecteur web prend uniquement en charge l’extraction du contenu d’une table à partir d’une page HTML. tooretrieve des données à partir d’un point de terminaison HTTP/s, utilisez [connecteur HTTP](data-factory-http-connector.md) à la place.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API. 

- toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello. 
- Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions pour les entités de fabrique de données qui sont utilisés toocopy des données à partir d’une table de web JSON, [exemple de JSON : copier des données à partir de la table de Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON de table de Web utilisés toodefine Data Factory entités tooa spécifique :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description du service de tooWeb spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **Web** |Oui |
| Url |Source de l’URL toohello Web |Oui |
| authenticationType |Anonyme |Oui |

### <a name="using-anonymous-authentication"></a>Utilisation de l’authentification anonyme

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **WebTable** a les propriétés suivantes de hello

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type |Type de jeu de données hello. doit être défini trop**WebTable** |Oui |
| path |Une ressource URL toohello relative qui contient la table de hello. |Non. Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé. |
| index |index de Hello de table hello dans la ressource de hello. Consultez [Get index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) section pour l’index de toogetting étapes d’une table dans une page HTML. |Oui |

**Exemple :**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Actuellement, lorsque source hello dans l’activité de copie est de type **WebSource**, aucune des propriétés supplémentaires ne sont pris en charge.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>Exemple de JSON : copier des données à partir de la table de Web tooAzure Blob
Hello ci-dessous illustre d’exemple :

1. Un service lié de type [Web](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [WebTable](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [WebSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données à partir d’un tooan de table Azure blob Web toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

Hello suivant l’exemple montre comment toocopy des données à partir d’un tooan de table Web Azure blob. Toutefois, les données peuvent être copiées directement tooany Hello récepteurs hello est indiqué dans [les activités de déplacement des données](data-factory-data-movement-activities.md) article à l’aide de l’activité de copie de hello dans Azure Data Factory.

**Service lié de Web** cet exemple utilise hello Web lié à service avec l’authentification anonyme. Consultez la section [Service lié Web](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

**Service lié Azure Storage**

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Jeu de données d’entrée WebTable** paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité Bonjour fabrique de données.

> [!NOTE]
> Consultez [Get index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) section pour l’index de toogetting étapes d’une table dans une page HTML.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Jeu de données de sortie d’objet Blob Azure**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



**Pipeline avec activité de copie**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**WebSource** et **récepteur** type est défini trop**BlobSink**.

Consultez [WebSource les propriétés de type](#copy-activity-type-properties) pour la liste des propriétés prises en charge par hello WebSource hello.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="get-index-of-a-table-in-an-html-page"></a>Obtenir l’index d’une table dans une page HTML
1. Lancez **Excel 2016** et basculez toohello **données** onglet.  
2. Cliquez sur **nouvelle requête** dans la barre d’outils de hello, pointez trop**à partir d’autres Sources** et cliquez sur **à partir du Web**.

    ![Menu Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. Bonjour **à partir du Web** boîte de dialogue, entrez **URL** où vous souhaitez utiliser dans des service JSON lié (par exemple : https://en.wikipedia.org/wiki/), ainsi que le chemin d’accès que vous spécifiez pour le jeu de données hello (par exemple : AFI % 27s_100_Years... 100_Movies), puis cliquez sur **OK**.

    ![Boîte de dialogue À partir du web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    URL utilisée dans cet exemple : https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Si vous voyez **contenu Access Web** boîte de dialogue, à droite de hello sélectionnez **URL**, **authentification**, puis cliquez sur **Connect**.

   ![Boîte de dialogue Accéder au contenu web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Cliquez sur un **table** hello arborescence afficher toosee le contenu à partir de la table de hello d’élément, puis cliquez sur **modifier** bouton bas hello.  

   ![Boîte de dialogue Navigateur](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. Bonjour **l’éditeur de requête** fenêtre, cliquez sur **éditeur avancé** bouton de barre d’outils hello.

    ![Bouton Éditeur avancé](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Dans la boîte de dialogue Éditeur avancé hello, hello nombre suivant trop « Source » est index de hello.

    ![Éditeur avancé - Index](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Si vous utilisez Excel 2013, utilisez [Microsoft Power Query pour Excel](https://www.microsoft.com/download/details.aspx?id=39379) index de hello tooget. Consultez [page de connexion tooa web](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article pour plus d’informations. étapes de Hello sont identiques si vous utilisez [Microsoft Power BI pour Desktop](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
