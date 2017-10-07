---
title: "données aaaTransform à l’aide du script U-SQL - Azure | Documents Microsoft"
description: "Découvrez comment tooprocess ou transformation des données en exécutant des scripts U-SQL sur Azure données Lake Analytique service de calcul."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Transformer des données en exécutant des scripts U-SQL sur Azure Data Lake Analytics 
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

Un pipeline dans une fabrique de données Azure traite les données dans les services de stockage liés à l'aide des services de calcul liés. Il contient une séquence d'activités dans laquelle chaque activité effectue une opération de traitement spécifique. Cet article décrit hello **données Lake Analytique U-SQL activité** qui exécute un **U-SQL** de script sur un **Analytique de LAC de données Azure** service lié de calcul. 

> [!NOTE]
> Créez un compte Azure Data Lake Analytics avant de créer un pipeline avec une activité U-SQL Data Lake Analytics. toolearn sur Analytique de LAC de données Azure, consultez [prise en main Azure données Lake Analytique](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Hello de révision [créer votre premier didacticiel de pipeline](data-factory-build-your-first-pipeline.md) pour obtenir des instructions détaillées toocreate une fabrique de données, lié à un pipeline, jeux de données et services. Utiliser des extraits de code JSON avec l’éditeur Data Factory ou entités de fabrique de données toocreate Visual Studio ou Azure PowerShell.

## <a name="supported-authentication-types"></a>Types d’authentification pris en charge
L’activité U-SQL prend en charge les types d’authentification ci-dessous pour Data Lake Analytics :
* Authentification d’un principal du service
* Utilisation de l’authentification des informations d’identification utilisateur (OAuth) 

Nous vous recommandons d’utiliser l’authentification de principal du service, en particulier pour une exécution de U-SQL planifiée. Un comportement d’expiration de jeton peut se produire avec l’authentification par informations d’identification utilisateur. Pour plus d’informations, consultez hello [lié des propriétés du service](#azure-data-lake-analytics-linked-service) section.

## <a name="azure-data-lake-analytics-linked-service"></a>Service lié Analytique Azure Data Lake
Vous créez un **Analytique de LAC de données Azure** lié service toolink une Analytique de LAC de données Azure compute service tooan Azure data factory. Hello activité Data Lake Analytique U-SQL dans le pipeline de hello fait référence toothis lié service. 

Hello tableau suivant fournit des descriptions pour hello propriétés génériques utilisées dans hello définition JSON. Vous pouvez ensuite choisir entre une authentification par principal de service et par informations d’identification utilisateur.

| Propriété | Description | Requis |
| --- | --- | --- |
| **type** |propriété de type Hello doit indiquer : **AzureDataLakeAnalytics**. |Oui |
| **accountName** |Nom du compte du service Analytique Azure Data Lake. |Oui |
| **dataLakeAnalyticsUri** |URI du service Analytique Azure Data Lake. |Non |
| **subscriptionId** |ID d’abonnement Azure |Non (si non spécifié, abonnement Hello fabrique de données est utilisée). |
| **resourceGroupName** |Nom du groupe de ressources Azure |Non (si non spécifié, groupe de ressources de hello fabrique de données est utilisée). |

### <a name="service-principal-authentication-recommended"></a>Authentification d’un principal du service (recommandée)
authentification principale du service toouse, inscrire une entité de l’application dans Azure Active Directory (Azure AD) et accordez à elle hello accéder à tooData Lake Store. Consultez la page [Authentification de service à service](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) pour des instructions détaillées. Prenez note de hello après les valeurs que vous pouvez utiliser toodefine hello de service lié :
* ID de l'application
* Clé de l'application 
* ID client

Utilisez l’authentification principale du service en spécifiant hello propriétés suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **servicePrincipalId** | Spécifiez l’ID client de. l’application hello | Oui |
| **servicePrincipalKey** | Spécifiez la clé de l’application hello. | Oui |
| **client** | Spécifiez les informations de locataire hello (ID client ou le nom de domaine) dans lequel réside votre application. Vous pouvez le récupérer par pointage de souris hello dans le coin supérieur droit de hello Hello portail Azure. | Oui |

**Exemple : authentification du principal de service**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Authentification des informations d’identification utilisateur
Vous pouvez également utiliser authentification des informations d’identification utilisateur pour l’Analytique lac de données en spécifiant les propriétés suivantes de hello :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **authorization** | Cliquez sur hello **Authorize** bouton Bonjour éditeur Data Factory et entrez vos informations d’identification qui affecte le propriété toothis URL hello générées automatiquement d’autorisation. | Oui |
| **sessionId** | ID de session OAuth à partir de la session de d’autorisation OAuth hello. Chaque ID de session est unique et ne peut être utilisé qu’une seule fois. Ce paramètre est automatiquement généré lorsque vous utilisez hello éditeur Data Factory. | Oui |

**Exemple : authentification des informations d’identification utilisateur**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiration du jeton
Hello code d’autorisation généré à l’aide de hello **Authorize** bouton expire après un certain temps. Consultez hello tableau suivant pour les délais d’expiration de hello pour différents types de comptes d’utilisateur. Hello message d’erreur suivant peut s’afficher lorsque hello authentification **expiration du jeton**: erreur de l’opération des informations d’identification : invalid_grant - AADSTS70002 : erreur de validation des informations d’identification. AADSTS70008 : hello fourni octroi d’accès est expiré ou révoqué. Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z ».

| Type d’utilisateur | Expire après |
|:--- |:--- |
| Comptes d’utilisateurs NON gérés par Azure Active Directory (@hotmail.com, @live.com, etc.) |12 heures |
| Comptes d’utilisateurs gérés par Azure Active Directory (AAD) |exécution de 14 jours après la dernière tranche de hello. <br/><br/>90 jours, si une tranche basée sur un service lié OAuth est exécutée au moins une fois tous les 14 jours. |

tooavoid/résoudre cette erreur, autorisez à nouveau à l’aide de hello **Authorize** bouton lorsque hello **expiration du jeton** et redéployez hello lié service. Vous pouvez également générer par programmation des valeurs pour les propriétés **sessionId** et **authorization** à l’aide du code suivant :

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Consultez [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), et [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) pour plus d’informations sur les classes de fabrique de données hello utilisées dans le code hello. Ajoutez une référence à : Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll pour hello WindowsFormsWebAuthenticationDialog classe. 

## <a name="data-lake-analytics-u-sql-activity"></a>Activité U-SQL Data Lake Analytics
Hello suivant extrait de code JSON définit un pipeline avec une activité de données Lake Analytique U-SQL. définition d’activité Hello possède une référence de toohello service Analytique de LAC de données Azure lié vous avez créé précédemment.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Hello tableau suivant décrit les noms et descriptions des propriétés qui sont spécifiques toothis activité. 

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type |propriété de type Hello doit être définie trop**DataLakeAnalyticsU-SQL**. |Oui |
| scriptPath |Toofolder de chemin d’accès qui contient le script de hello U-SQL. Nom du fichier de hello respecte la casse. |Non (si vous utilisez le script) |
| scriptLinkedService |Service lié qui établit un lien stockage hello qui contient la fabrique de données hello script toohello |Non (si vous utilisez le script) |
| script |Spécifiez un script en ligne au lieu de spécifier scriptPath et scriptLinkedService. Par exemple : `"script": "CREATE DATABASE test"`. |Non (si vous utilisez scriptPath et scriptLinkedService) |
| degreeOfParallelism |nombre maximal de Hello de nœuds utilisés simultanément tâche hello de toorun. |Non |
| priority |Détermine les tâches en dehors de tout ce qui sont en attente doivent être sélectionné toorun tout d’abord. Hello hello numéro inférieur, une priorité plus élevée hello hello. |Non |
| parameters |Paramètres de script de hello U-SQL |Non |
| runtimeVersion | Version du runtime de toouse de moteur hello U-SQL | Non | 
| compilationMode | <p>Mode de compilation d’U-SQL. Doit avoir l’une des valeurs suivantes :</p> <ul><li>**Semantic :** exécuter uniquement les vérifications sémantiques et les contrôles d’intégrité nécessaires.</li><li>**Complète :** effectuer une compilation complète hello, y compris la vérification de la syntaxe, l’optimisation, la génération de code, etc..</li><li>**SingleBox :** effectuer une compilation complète hello, avec tooSingleBox de paramètre TargetType.</li></ul><p>Si vous ne spécifiez pas une valeur pour cette propriété, serveur de hello détermine le mode de compilation optimal hello. </p>| Non | 

Consultez [SearchLogProcessing.txt Script définition](#sample-u-sql-script) pour la définition de script hello. 

## <a name="sample-input-and-output-datasets"></a>Exemples de jeux de données d'entrée et de sortie
### <a name="input-dataset"></a>Jeu de données d'entrée
Dans cet exemple, les données d’entrée hello résident dans un Azure Data Lake Store (fichier SearchLog.tsv dans le dossier de datalake/entrée hello). 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Jeu de données de sortie
Dans cet exemple, les données de sortie de hello produites par hello script U-SQL sont stockées dans un Azure Data Lake Store (dossier datalake/sortie). 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Exemple de service lié Data Lake Store
Voici la définition hello d’exemple hello Qu'azure Data Lake Store lié service utilisé par les jeux de données d’entrée/sortie de hello. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

Consultez [déplacer tooand de données à partir d’Azure Data Lake Store](data-factory-azure-datalake-connector.md) article pour une description des propriétés JSON. 

## <a name="sample-u-sql-script"></a>Exemple de script SQL-U

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

Hello pour les valeurs  **@in**  et  **@out**  paramètres dans le script de hello U-SQL sont passés dynamiquement par la définition d’application à l’aide de la section « Paramètres » de hello. Consultez la section de « paramètres » de hello dans la définition de pipeline hello.

Vous pouvez spécifier d’autres propriétés comme la priorité et degreeOfParallelism également dans votre définition de pipeline pour les travaux hello qui s’exécutent sur hello service d’Analytique de LAC de données Azure.

## <a name="dynamic-parameters"></a>Paramètres dynamiques
Dans la définition de pipeline exemple hello et l’extraction sont affectées aux paramètres avec des valeurs codées en dur. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

Il est possible toouse les paramètres dynamiques à la place. Par exemple : 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

Dans ce cas, les fichiers d’entrée sont toujours extraits à partir du dossier /datalake/input hello et les fichiers de sortie sont générés dans le dossier de /datalake/output hello. les noms de fichiers Hello sont dynamiques en fonction de l’heure de début de tranche hello.  

