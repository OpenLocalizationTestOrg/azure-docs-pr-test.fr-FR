---
title: "aaaBuild votre première fabrique de données (portail Azure) | Documents Microsoft"
description: "Dans ce didacticiel, vous créez un exemple de pipeline Azure Data Factory à l’aide d’éditeur Data Factory Bonjour portail Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Didacticiel : Créer votre première fabrique de données Azure à l’aide du portail Azure
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-build-your-first-pipeline.md)
> * [Portail Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modèle Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)


Dans cet article, vous apprendrez comment toouse [portail Azure](https://portal.azure.com/) toocreate votre première Azure data factory. didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello. 

pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**. Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce. pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin. 

> [!NOTE]
> le pipeline de données Hello dans ce didacticiel transforme les données de sortie de données d’entrée tooproduce. Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Composants requis
1. Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.
2. Cet article ne fournit pas une vue d’ensemble conceptuelle de hello service Azure Data Factory. Nous recommandons que vous parcourez [Introduction tooAzure Data Factory](data-factory-introduction.md) article pour obtenir une présentation détaillée du service de hello.  

## <a name="create-data-factory"></a>Créer une fabrique de données
Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive données tooproduct sortie les données d’entrée. Commençons par créer la fabrique de données hello dans cette étape.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **nouveau** sur menu gauche hello **données + Analytique**, puis cliquez sur **Data Factory**.

   ![Panneau Créer](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. Bonjour **nouvelle fabrique de données** panneau, entrez **GetStartedDF** pour hello nom.

   ![Panneau Nouvelle fabrique de données](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > nom de Hello de fabrique de données Azure hello doit être **global unique**. Si vous recevez une erreur de hello : **nom de fabrique de données « GetStartedDF » n’est pas disponible**. Modifier le nom hello hello fabrique de données (par exemple, yournameGetStartedDF) et essayez à nouveau de créer. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.
   >
   > nom Hello hello fabrique de données peut être enregistré comme un **DNS** nom dans les futures hello et donc devenir visible publiquement.
   >
   >
4. Sélectionnez hello **abonnement Azure** où vous souhaitez toobe de fabrique de données hello créé.
5. Sélectionnez un **groupe de ressources** existant ou créez-en un. Didacticiel de hello, créer un groupe de ressources nommé : **ADFGetStartedRG**.
6. Sélectionnez hello **emplacement** de fabrique de données hello. Seules les régions pris en charge par hello service Data Factory sont affichées dans la liste déroulante de hello.
7. Sélectionnez **toodashboard du code confidentiel**. 
8. Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.

   > [!IMPORTANT]
   > instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.
   >
   >
7. Tableau de bord de hello, vous voyez hello suivant vignette avec l’état : déploiement de fabrique de données.    

   ![État de la création de la fabrique de données](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Félicitations ! Vous avez créé votre première fabrique de données. Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données.     

    ![Panneau Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Avant de créer un pipeline dans la fabrique de données hello, vous devez toocreate quelques entités de fabrique de données tout d’abord. Vous créez tout d’abord les services liés toolink données magasins/calcule tooyour données stockent, définissent l’entrée et sortie des données de d’entrée/sortie toorepresent de jeux de données dans des magasins de données liées et ensuite créer un pipeline de hello avec une activité qui utilise ces jeux de données.

## <a name="create-linked-services"></a>Créez des services liés
Dans cette étape, vous liez votre compte de stockage Azure et une fabrique de données à la demande Azure HDInsight cluster tooyour. blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple. Hello service lié HDInsight est toorun utilisé un script Hive spécifié dans l’activité hello du pipeline hello dans cet exemple. Identifier les [magasin de données](data-factory-data-movement-activities.md)/[les services de calcul](data-factory-compute-linked-services.md) sont utilisés dans votre scénario et de lier ces fabrique de données de services toohello en créant des services liés.  

### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage. Dans ce didacticiel, vous utilisez hello même compte de stockage Azure hello HQL et les données d’entrée/sortie toostore de fichier de script.

1. Cliquez sur **auteur et déployer** sur hello **DATA FACTORY** panneau pour **GetStartedDF**. Vous devez voir hello éditeur Data Factory.

   ![Vignette Créer et déployer](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Cliquez sur **Nouveau magasin de données** et choisissez **Stockage Azure**.

   ![Nouveau magasin de données - Stockage Azure - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Vous devez voir hello script JSON pour la création d’un stockage Azure lié à service dans l’éditeur de hello.

   ![Service lié Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Remplacez **nom de compte** avec le nom de hello de votre compte de stockage Azure et **clé de compte** avec la clé d’accès hello Hello compte de stockage Azure. toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.

    ![Bouton déployer](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Une fois hello service lié est déployé avec succès, hello **Draft-1** fenêtre doit disparaître et vous voyez **AzureStorageLinkedService** dans l’arborescence hello sur hello gauche.

    ![Service lié au stockage dans le menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Créer le service lié Azure HDInsight
Dans cette étape, vous liez une fabrique de données à la demande HDInsight cluster tooyour. Hello cluster HDInsight est automatiquement créé lors de l’exécution et supprimée une fois ceci effectué inactifs et le traitement de la durée spécifiée hello.

1. Bonjour **éditeur Data Factory**, cliquez sur **... Plus**, puis sur **Nouveau calcul** et sélectionnez **Cluster à la demande HDInsight**.

    ![Nouveau calcul](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Copiez et collez hello suivant extrait toohello **Draft-1** fenêtre. extrait de code Hello JSON décrit les propriétés hello sont utilisées toocreate hello sur demande du cluster HDInsight.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

   | Propriété | Description |
   |:--- |:--- |
   | ClusterSize |Spécifie la taille de hello du cluster HDInsight de hello. |
   | TimeToLive | Spécifie la durée d’inactivité de ce hello pour le cluster HDInsight de hello, avant d’être supprimé. |
   | linkedServiceName | Spécifie le compte de stockage hello toostore utilisé hello journaux générés par HDInsight. |

    Hello Notez les points suivants :

   * Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello JSON. Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
   * Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
   * Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Avec le service lié HDInsight disponible à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (**timeToLive**). Hello cluster est automatiquement supprimé lorsque le traitement de hello est effectué.

       Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ». Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.

     Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
3. Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.

    ![Déployer un service lié HDInsight à la demande](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Vérifiez que vous voyez les deux **AzureStorageLinkedService** et **HDInsightOnDemandLinkedService** dans l’arborescence hello sur hello gauche.

    ![Arborescence avec les services liés](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Créez les jeux de données
Dans cette étape, vous créez des groupes de données toorepresent hello d’entrée et sortie des données pour le traitement de la ruche. Ces jeux de données font référence toohello **AzureStorageLinkedService** que vous avez créé précédemment dans ce didacticiel. Hello tooan de points de service lié compte de stockage Azure et de jeux de données spécifiez conteneur, dossier, le nom de fichier dans le stockage hello qui contient l’entrée et les données de sortie.   

### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
1. Bonjour **éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.

    ![Nouveau jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Copiez et collez hello suivant fenêtre toohello Draft-1. Dans l’extrait de code hello JSON, vous créez un dataset nommé **AzureBlobInput** qui représente les données d’entrée pour une activité dans le pipeline de hello. En outre, vous spécifiez que les données d’entrée hello se trouve dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

   | Propriété | Description |
   |:--- |:--- |
   | type |propriété de type Hello est définie trop**AzureBlob** , car les données résident dans un stockage d’objets blob Azure. |
   | linkedServiceName |Fait référence toohello **AzureStorageLinkedService** vous avez créé précédemment. |
   | folderPath | Spécifie l’objet blob de hello **conteneur** et hello **dossier** qui contient des objets BLOB d’entrée. | 
   | fileName |Cette propriété est facultative. Si vous omettez cette propriété, tous les fichiers hello hello folderPath sont récupérées. Dans ce didacticiel, uniquement hello **input.log** est traité. |
   | type |les fichiers journaux Hello étant au format texte, nous utilisons **TextFormat**. |
   | columnDelimiter |colonnes dans les fichiers journaux de hello sont délimitées par **caractère virgule (`,`)** |
   | frequency/interval |fréquence définie trop**mois** et l’intervalle est **1**, ce qui signifie que hello entrée tranches sont disponibles chaque mois. |
   | external | Cette propriété a la valeur trop**true** si les données d’entrée hello ne sont pas générées par ce pipeline. Dans ce didacticiel, le fichier de input.log de hello n’est pas généré par ce pipeline, et nous avons hello propriété tootrue. |

    Pour plus d’informations sur ces propriétés JSON, voir [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).
3. Cliquez sur **déployer** sur le jeu de données toodeploy hello nouvellement créée de la barre de commandes hello. Vous devez voir hello le jeu de données dans l’arborescence hello sur hello gauche.

### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
Maintenant, vous créez hello sortie dataset toorepresent hello sortie les données stockées dans hello le stockage Blob Azure.

1. Bonjour **éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.  
2. Copiez et collez hello suivant fenêtre toohello Draft-1. Dans l’extrait de code hello JSON, vous créez un dataset nommé **AzureBlobOutput**et préciser leur structure de données hello qui sont générées par le script Hive de hello hello. En outre, vous spécifiez que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **partitioneddata**. Hello **disponibilité** section spécifie ce jeu de données de sortie hello est généré sur une base mensuelle.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    Consultez **créer le jeu de données d’entrée hello** section pour obtenir une description de ces propriétés. Vous ne définissez pas la propriété d’externe de hello sur un jeu de données de sortie comme jeu de données hello est généré par le service de fabrique de données hello.
3. Cliquez sur **déployer** sur le jeu de données toodeploy hello nouvellement créée de la barre de commandes hello.
4. Vérifiez que ce jeu de données hello est créé avec succès.

    ![Arborescence avec les services liés](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Création d’un pipeline
Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** . Secteur d’entrée est disponible mensuellement (fréquence : mois, intervalle : 1), la tranche de sortie est générée chaque mois et hello du planificateur pour l’activité de hello est également définie toomonthly. paramètres Hello pour le jeu de données de sortie hello et planificateur d’activité hello doivent correspondre. Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie. Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello. propriétés qui Hello hello suivant JSON sont expliquées à fin hello de cette section.

1. Bonjour **éditeur Data Factory**, cliquez sur **points de suspension (...) Plusieurs commandes** puis cliquez sur **nouveau pipeline**.

    ![bouton Nouveau pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Copiez et collez hello suivant fenêtre toohello Draft-1.

   > [!IMPORTANT]
   > Remplacez **storageaccountname** avec nom hello de votre compte de stockage Bonjour JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **AzureStorageLinkedService**) et dans  **script** dossier dans le conteneur de hello **adfgetstarted**.

    Hello **définit** section est de paramètres d’exécution utilisés toospecify hello script hive de toohello passés en tant que valeurs de configuration Hive (exemple : ${hiveconf : inputtable}, ${hiveconf:partitionedtable}).

    Hello **Démarrer** et **fin** propriétés de pipeline de hello spécifie la période active de hello du pipeline de hello.

    Dans l’activité hello JSON, vous spécifiez ce script Hive hello s’exécute sur le calcul hello spécifié par hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Consultez la section « JSON de Pipeline » dans [Pipelines et les activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON utilisées dans l’exemple de hello.
   >
   >
3. Validez les éléments suivants de hello :

   1. **Input.log** fichier existe dans hello **inputdata** dossier Hello **adfgetstarted** conteneur Bonjour stockage d’objets blob Azure
   2. **partitionweblogs.hql** fichier existe dans hello **script** dossier Hello **adfgetstarted** conteneur Bonjour stockage d’objets blob Azure. Condition préalable de hello terminé les étapes Bonjour [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) si vous ne voyez pas ces fichiers.
   3. Vérifiez que vous avez remplacé **storageaccountname** avec nom hello de votre compte de stockage Bonjour JSON de pipeline.
4. Cliquez sur **déployer** sur le pipeline de hello toodeploy de barre de commandes hello. Depuis hello **Démarrer** et **fin** heures sont définies dans hello passée et **isPaused** est toofalse ensemble, pipeline de hello (activité dans le pipeline de hello) immédiatement après le déploiement.
5. Vérifiez que vous voyez pipeline hello dans arborescence hello.

    ![Arborescence avec pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. Félicitations ! Vous avez créé votre premier pipeline !

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
### <a name="monitor-pipeline-using-diagram-view"></a>Surveillance d’un pipeline à l’aide de la Vue de diagramme
1. Cliquez sur **X** tooclose éditeur Data Factory panneaux et toonavigate Panneau de fabrique de données toohello de sauvegarde, puis cliquez sur **diagramme**.

    ![Vignette schématique](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. Dans la vue de diagramme de hello, vous consultez une vue d’ensemble des pipelines de hello et jeux de données utilisés dans ce didacticiel.

    ![Vue du diagramme](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview diagramme de toutes les activités dans le pipeline de hello, pipeline avec le bouton droit dans hello et cliquez sur Ouvrir Pipeline.

    ![Menu Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Vérifiez que vous voyez hello HDInsightHive activité hello pipeline.

    ![Vue Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate sauvegarder toohello de vue précédente, cliquez sur **Data factory** dans le menu de navigation hello haut hello.
5. Bonjour **vue de diagramme**, double-cliquez sur le jeu de données hello **AzureBlobInput**. Confirmer que la tranche hello est **prêt** état. Il peut prendre quelques minutes pour hello tranche tooshow dans l’état Ready. Si elle ne se produit pas une fois que vous patientez un moment, consultez si vous avez des fichiers d’entrée hello (input.log) placé dans le conteneur de droite hello (adfgetstarted) et de dossier (inputdata).

   ![Segment d’entrée dans l’état Prêt](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Cliquez sur **X** tooclose **AzureBlobInput** panneau.
7. Bonjour **vue de diagramme**, double-cliquez sur le jeu de données hello **AzureBlobOutput**. Vous voyez ce secteur hello qui est en cours de traitement.

   ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Lorsque le traitement est terminé, vous consultez la section hello dans **prêt** état.

   ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes). Par conséquent, attendez que le pipeline de hello prennent trop **environ 30 minutes** tooprocess hello tranche.
   >
   >

9. Lorsque la tranche de hello est à **prêt** d’état, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.  

   ![données de sortie](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Cliquez sur Détails de toosee hello tranche sur celui-ci dans un **tranche de données** panneau.

   ![Détails de la tranche](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Cliquez sur une activité à exécuter dans hello **liste s’exécute l’activité** toosee des détails sur une activité exécuter (activité Hive dans notre scénario) dans un **détails de la série activité** fenêtre.   

   ![Détails de l'exécution d'activité](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   À partir de fichiers de journal hello, vous pouvez voir la requête Hive hello qui a été exécutée et les informations d’état. Ces journaux sont utiles pour résoudre les problèmes.
   Consultez l’article [Surveillance et gestion des pipelines d’Azure Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d’informations.

> [!IMPORTANT]
> fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès. Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Surveiller le pipeline à l’aide de l’application de surveillance et de gestion
Vous pouvez également utiliser le moniteur et gérer les applications toomonitor vos pipelines. Pour en savoir plus sur l’utilisation de cette application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).

1. Cliquez sur **moniteur & gérer** vignette sur la page d’accueil hello pour votre fabrique de données.

    ![Vignette Surveiller et gérer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. **L’application de surveillance et de gestion** devrait s’afficher. Hello de modification **l’heure de début** et **heure de fin** toomatch début et fin de votre pipeline, puis cliquez sur **appliquer**.

    ![Application de surveillance et gestion](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Sélectionnez une fenêtre d’activité Bonjour **Windows de l’activité** liste toosee des informations à son.

    ![Détails de la fenêtre d’activité](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez créé un Azure data factory tooprocess de données en exécutant le script Hive sur un cluster de hadoop HDInsight. Vous avez utilisé hello éditeur Data Factory dans Bonjour Azure toodo portail Bonjour comme suit :  

1. Création d’une **fabrique de données**Azure.
2. Création de deux **services liés**:
   1. **Le stockage Azure** lié service toolink votre stockage d’objets blob Azure qui contient la fabrique de données toohello les fichiers d’entrée/sortie.
   2. **Azure HDInsight** à la demande liée service toolink une fabrique de données à la demande HDInsight Hadoop cluster toohello. Azure Data Factory crée un HDInsight Hadoop données d’entrée de cluster juste-à-temps tooprocess et générer les données de sortie.
3. Créé deux **jeux de données**, qui décrivent les données d’entrée et de sortie pour l’activité HDInsight Hive dans le pipeline de hello.
4. Création d’un **pipeline** avec une activité **Hive HDInsight**.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez créé un pipeline avec une activité de transformation (Activité HDInsight) qui exécute un script Hive sur un cluster HDInsight à la demande. toosee toouse un activité de copie toocopy des données d’une tooAzure d’objets Blob Azure SQL, voir [didacticiel : copier des données à partir d’un tooAzure d’objets blob Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Voir aussi
| Rubrique | Description |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario. |
| [Groupes de données](data-factory-create-datasets.md) |Cet article vous aide à comprendre les jeux de données dans Azure Data Factory. |
| [Planification et exécution](data-factory-scheduling-and-execution.md) |Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory. |
| [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.](data-factory-monitor-manage-app.md) |Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion. |
