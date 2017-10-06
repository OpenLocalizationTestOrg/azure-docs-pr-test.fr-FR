---
title: "aaaBuild votre première fabrique de données (PowerShell) | Documents Microsoft"
description: "Dans ce didacticiel, vous allez créer un exemple de pipeline Azure Data Factory à l’aide d’Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Didacticiel : Créer votre première fabrique de données Azure à l’aide d’Azure PowerShell
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-build-your-first-pipeline.md)
> * [Portail Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modèle Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

Dans cet article, vous utilisez Azure PowerShell toocreate votre première Azure data factory. didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello.

pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**. Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce. pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin. 

> [!NOTE]
> le pipeline de données Hello dans ce didacticiel transforme les données de sortie de données d’entrée tooproduce. Elle ne copie pas les données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Composants requis
* Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.
* Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) article tooinstall version la plus récente d’Azure PowerShell sur votre ordinateur.
* (facultatif) Cet article ne couvre pas toutes les applets de commande hello Data Factory. Consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories) pour obtenir une documentation complète sur les applets de commande Data Factory.

## <a name="create-data-factory"></a>Créer une fabrique de données
Dans cette étape, vous utilisez Azure PowerShell toocreate une fabrique de données Azure nommé **FirstDataFactoryPSH**. Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive les données d’entrée. Commençons par créer la fabrique de données hello dans cette étape.

1. Démarrez Azure PowerShell et exécutez hello commande suivante. Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel. Si vous fermez et rouvrez, vous devez toorun ces commandes à nouveau.
   * Exécutez hello suivant de commande et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Tooselect hello abonnement toowork avec la commande suivante d’exécution hello. Cet abonnement doit être hello identique à celui Bonjour portail Azure hello.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello de commande suivante :
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Certaines des étapes hello dans ce didacticiel supposent que vous utilisez le groupe de ressources hello nommé ADFTutorialResourceGroup. Si vous utilisez un autre groupe de ressources, vous devez toouse il à la place de ADFTutorialResourceGroup dans ce didacticiel.
3. Exécutez hello **New-AzureRmDataFactory** applet de commande qui crée une fabrique de données nommée **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Hello Notez les points suivants :

* nom de Hello Hello Azure Data Factory doit être globalement unique. Si vous recevez une erreur de hello **nom de fabrique de données « FirstDataFactoryPSH » n’est pas disponible**, modifiez le nom hello (par exemple, yournameFirstDataFactoryPSH). Utilisez ce nom à la place d’ADFTutorialFactoryPSH quand vous effectuez les étapes de ce didacticiel. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.
* instances de fabrique de données toocreate, vous devez toobe un collaborateur/administrateur Hello abonnement Azure
* nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.
* Si vous recevez une erreur de hello : «**cet abonnement n’est pas un espace de noms inscrit toouse Microsoft.DataFactory**», effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :

  * Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello fabrique de données :

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello :

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Connexion à l’aide de hello abonnement Azure dans hello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure. Cette action enregistre automatiquement le fournisseur hello pour vous.

Avant de créer un pipeline, vous devez toocreate quelques entités de fabrique de données tout d’abord. Vous créez tout d’abord les services liés toolink données magasins/calcule tooyour données stockent, définissent l’entrée et sortie des données de d’entrée/sortie toorepresent de jeux de données dans des magasins de données liées et ensuite créer un pipeline de hello avec une activité qui utilise ces jeux de données.

## <a name="create-linked-services"></a>Créez des services liés
Dans cette étape, vous liez votre compte de stockage Azure et une fabrique de données à la demande Azure HDInsight cluster tooyour. blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple. Hello service lié HDInsight est toorun utilisé un script Hive spécifié dans l’activité hello du pipeline hello dans cet exemple. Identifier les données de magasin/calcul services sont utilisés dans votre scénario et lier ces fabrique de données de services toohello en créant des services liés.

### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage. Vous utilisez hello même compte de stockage Azure hello HQL et les données d’entrée/sortie toostore de fichier de script.

1. Créer un fichier JSON comportant StorageLinkedService.json dans le dossier de C:\ADFGetStarted hello hello suivant contenu. Créez le dossier hello ADFGetStarted si elle n’existe pas déjà.

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    Remplacez **nom de compte** avec le nom de hello de votre compte de stockage Azure et **clé de compte** avec la clé d’accès hello Hello compte de stockage Azure. toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. Dans Azure PowerShell, basculez toohello ADFGetStarted dossier.
3. Vous pouvez utiliser hello **New-AzureRmDataFactoryLinkedService** applet de commande qui crée un service lié. Cette applet de commande et d’autres applets de commande fabrique de données que vous utilisez dans ce didacticiel requiert vous toopass des valeurs pour hello *ResourceGroupName* et *DataFactoryName* paramètres. Vous pouvez également utiliser **Get-AzureRmDataFactory** tooget un **DataFactory** de l’objet et de passer un objet de hello sans avoir à taper *ResourceGroupName* et  *DataFactoryName* chaque fois que vous exécutez une applet de commande. Sortie de hello tooassign Hello de commandes suivante d’exécution hello **Get-AzureRmDataFactory** tooa de l’applet de commande **$df** variable.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. Exécutez maintenant hello **New-AzureRmDataFactoryLinkedService** liés de l’applet de commande qui crée hello **StorageLinkedService** service.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Si vous n’aviez pas exécuter hello **Get-AzureRmDataFactory** applet de commande et attribué hello sortie toohello **$df** variable, vous devez les valeurs toospecify pour hello *ResourceGroupName*et *DataFactoryName* paramètres comme suit.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Si vous fermez Azure PowerShell milieu hello du didacticiel de hello, vous avez toorun hello **Get-AzureRmDataFactory** prochain démarrage du didacticiel de hello toocomplete Azure PowerShell de l’applet de commande.

### <a name="create-azure-hdinsight-linked-service"></a>Créer le service lié Azure HDInsight
Dans cette étape, vous liez une fabrique de données à la demande HDInsight cluster tooyour. Hello cluster HDInsight est automatiquement créé lors de l’exécution et supprimée une fois ceci effectué inactifs et le traitement de la durée spécifiée hello. Vous pouvez utiliser votre propre cluster HDInsight au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .

1. Créez un fichier JSON nommé **HDInsightOnDemandLinkedService**.json Bonjour **C:\ADFGetStarted** dossier avec hello suivant le contenu.

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

   | Propriété | Description |
   |:--- |:--- |
   | ClusterSize |Spécifie la taille de hello du cluster HDInsight de hello. |
   | TimeToLive |Spécifie la durée d’inactivité de ce hello pour le cluster HDInsight de hello, avant d’être supprimé. |
   | linkedServiceName |Spécifie le compte de stockage hello toostore utilisé hello journaux générés par HDInsight |

    Hello Notez les points suivants :

   * Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello JSON. Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
   * Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
   * Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Avec le service lié HDInsight disponible à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (**timeToLive**). Hello cluster est automatiquement supprimé lorsque le traitement de hello est effectué.

       Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ». Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.

     Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
2. Exécutez hello **New-AzureRmDataFactoryLinkedService** applet de commande qui crée hello lié service appelé HDInsightOnDemandLinkedService.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Créez les jeux de données
Dans cette étape, vous créez des groupes de données toorepresent hello d’entrée et sortie des données pour le traitement de la ruche. Ces jeux de données font référence toohello **StorageLinkedService** que vous avez créé précédemment dans ce didacticiel. Hello tooan de points de service lié compte de stockage Azure et de jeux de données spécifiez conteneur, dossier, le nom de fichier dans le stockage hello qui contient l’entrée et les données de sortie.

### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
1. Créez un fichier JSON nommé **InputTable.json** Bonjour **C:\ADFGetStarted** dossier avec hello suivant le contenu :

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Hello JSON définit un dataset nommé **AzureBlobInput**, qui représente les données d’entrée pour une activité dans le pipeline de hello. En outre, il spécifie que les données d’entrée hello se trouve dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **inputdata**.

    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

   | Propriété | Description |
   |:--- |:--- |
   | type |propriété de type Hello a la valeur tooAzureBlob, car les données résident dans le stockage blob Azure. |
   | linkedServiceName |fait référence toohello StorageLinkedService que vous avez créé précédemment. |
   | fileName |Cette propriété est facultative. Si vous omettez cette propriété, tous les fichiers hello hello folderPath sont récupérées. Dans ce cas, uniquement les input.log hello est traitée. |
   | type |les fichiers journaux Hello étant au format texte, nous utilisons TextFormat. |
   | columnDelimiter |colonnes dans les fichiers journaux de hello sont délimitées par un caractère de virgule hello (,). |
   | frequency/interval |fréquence égale tooMonth et l’intervalle est 1, ce qui signifie que les tranches d’entrée hello sont disponibles chaque mois. |
   | external |Cette propriété a la valeur tootrue si les données d’entrée hello ne sont pas générées par le service de fabrique de données hello. |
2. Exécutez hello commande Azure PowerShell toocreate hello Data Factory DataSet suivante :

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
Maintenant, vous créez hello sortie dataset toorepresent hello sortie les données stockées dans hello le stockage Blob Azure.

1. Créez un fichier JSON nommé **OutputTable.json** Bonjour **C:\ADFGetStarted** dossier avec hello suivant le contenu :

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    Hello JSON définit un dataset nommé **AzureBlobOutput**, qui représente les données de sortie d’une activité dans le pipeline de hello. En outre, il spécifie que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **partitioneddata**. Hello **disponibilité** section spécifie ce jeu de données de sortie hello est généré sur une base mensuelle.
2. Exécutez hello commande Azure PowerShell toocreate hello Data Factory DataSet suivante :

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>Création d’un pipeline
Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** . Secteur d’entrée est disponible mensuellement (fréquence : mois, intervalle : 1), la tranche de sortie est générée chaque mois et hello du planificateur pour l’activité de hello est également définie toomonthly. paramètres Hello pour le jeu de données de sortie hello et planificateur d’activité hello doivent correspondre. Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie. Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello. propriétés qui Hello hello suivant JSON sont expliquées à fin hello de cette section.

1. Créer un fichier JSON comportant MyFirstPipelinePSH.json dans le dossier de C:\ADFGetStarted hello hello suivant contenu :

   > [!IMPORTANT]
   > Remplacez **storageaccountname** avec nom hello de votre compte de stockage Bonjour JSON.
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    Dans l’extrait de code hello JSON, vous créez un pipeline qui se compose d’une activité unique qui utilise la ruche tooprocess données sur un cluster HDInsight.

    fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **StorageLinkedService**) et dans **script**  dossier dans le conteneur de hello **adfgetstarted**.

    Hello **définit** section est de paramètres d’exécution utilisés toospecify hello être passé le script hive de toohello en tant que valeurs de configuration Hive (exemple : ${hiveconf : inputtable}, ${hiveconf:partitionedtable}).

    Hello **Démarrer** et **fin** propriétés de pipeline de hello spécifie la période active de hello du pipeline de hello.

    Dans l’activité hello JSON, vous spécifiez ce script Hive hello s’exécute sur le calcul hello spécifié par hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Consultez la section « JSON de Pipeline » dans [Pipelines et les activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON qui sont utilisées dans l’exemple de hello.

2. Vérifiez que vous voyez hello **input.log** fichier Bonjour **adfgetstarted/inputdata** dossier hello stockage d’objets blob Azure et exécution hello suivant de pipeline de commande toodeploy hello. Depuis hello **Démarrer** et **fin** heures sont définies dans hello passée et **isPaused** est toofalse ensemble, pipeline de hello (activité dans le pipeline de hello) immédiatement après le déploiement.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. Félicitations, vous avez réussi à créer votre premier pipeline avec Azure PowerShell.

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
Dans cette étape, vous utilisez Azure PowerShell toomonitor ce qui se passe dans une fabrique de données Azure.

1. Exécutez **Get-AzureRmDataFactory** et affecter hello sortie tooa **$df** variable.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Exécutez **Get-AzureRmDataFactorySlice** tooget plus d’informations sur toutes les tranches de hello **EmpSQLTable**, qui est la table de sortie hello du pipeline de hello.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    Notez que hello %StartDateTime;) que vous spécifiez ici est hello que même heure de début spécifiée dans le code JSON de pipeline hello. Voici le résultat de l’exemple hello :

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Exécutez **Get-AzureRmDataFactoryRun** tooget les détails de hello de l’activité s’exécute pour une tranche spécifique.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Voici le résultat de l’exemple hello : 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    Vous pouvez conserver en cours d’exécution cette applet de commande jusqu'à ce que vous voyiez secteur hello dans **prêt** état ou **n’a pas pu** état. Lors de la tranche de hello est prêt, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.  La création d’un cluster HDInsight à la demande prend généralement un certain temps.

    ![données de sortie](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes). Par conséquent, s’attendent hello pipeline tootake **environ 30 minutes** tooprocess hello tranche.
>
> fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès. Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.
>
>

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez créé un Azure data factory tooprocess de données en exécutant le script Hive sur un cluster de hadoop HDInsight. Vous avez utilisé hello éditeur Data Factory dans Bonjour Azure toodo portail Bonjour comme suit :

1. Création d’une **fabrique de données**Azure.
2. Création de deux **services liés**:
   1. **Le stockage Azure** lié service toolink votre stockage d’objets blob Azure qui contient la fabrique de données toohello les fichiers d’entrée/sortie.
   2. **Azure HDInsight** à la demande liée service toolink une fabrique de données à la demande HDInsight Hadoop cluster toohello. Azure Data Factory crée un HDInsight Hadoop données d’entrée de cluster juste-à-temps tooprocess et générer les données de sortie.
3. Créé deux **jeux de données**, qui décrivent les données d’entrée et de sortie pour l’activité HDInsight Hive dans le pipeline de hello.
4. Création d’un **pipeline** avec une activité **Hive HDInsight**.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez créé un pipeline avec une activité de transformation (Activité HDInsight) qui exécute un script Hive sur un cluster Azure HDInsight à la demande. toosee toouse un activité de copie toocopy des données d’une tooAzure d’objets Blob Azure SQL, voir [didacticiel : copier des données à partir d’un tooAzure d’objets Blob Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Voir aussi
| Rubrique | Description |
|:--- |:--- |
| [Informations de référence sur les applets de commande de Data Factory](/powershell/module/azurerm.datafactories) |Consultez la documentation complète sur les applets de commande de Data Factory |
| [Pipelines](data-factory-create-pipelines.md) |Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario. |
| [Groupes de données](data-factory-create-datasets.md) |Cet article vous aide à comprendre les jeux de données dans Azure Data Factory. |
| [Planification et exécution](data-factory-scheduling-and-execution.md) |Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory. |
| [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.](data-factory-monitor-manage-app.md) |Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion. |
