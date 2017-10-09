---
title: "les programmes à partir d’Azure Data Factory aaaInvoke Spark | Documents Microsoft"
description: "Découvrez comment les programmes de Spark tooinvoke à partir d’un à l’aide de la fabrique de données Azure hello activité MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Appeler des programmes Spark à partir des pipelines Azure Data Factory

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

## <a name="introduction"></a>Introduction
Activité de Spark est un des hello [activités de transformation des données](data-factory-data-transformation-activities.md) pris en charge par Azure Data Factory. Cette activité s’exécute hello spécifiée programme Spark sur votre cluster Apache Spark dans Azure HDInsight.    

> [!IMPORTANT]
> - L’activité Spark ne prend pas en charge les clusters Spark HDInsight qui utilisent Azure Data Lake Store en tant que stockage principal.
> - L’activité Spark prend en charge uniquement les clusters Spark HDInsight existants (c’est-à-dire vos propres clusters). Elle ne prend pas en charge les services liés HDInsight à la demande.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>Procédure pas à pas : création d’un pipeline avec l’activité Spark
Ici, les étapes classiques de hello toocreate un pipeline de fabrique de données avec une activité Spark.  

1. Créer une fabrique de données.
2. Créer un toolink de service lié Azure Storage de votre stockage Azure qui est associé à votre fabrique de données toohello cluster HDInsight Spark.     
2. Créer un toolink de service lié HDInsight Azure de votre cluster Apache Spark dans Azure HDInsight toohello data factory.
3. Créer un jeu de données qui fait référence toohello lié Azure Storage service. Actuellement, vous devez spécifier un jeu de données de sortie d’une activité même si aucune sortie n’est produite.  
4. Créer un pipeline avec activités Spark qui fait référence de service lié HDInsight de toohello créé dans #2. activité Hello est configurée avec hello le jeu de données créé à l’étape précédente de hello comme un jeu de données de sortie. jeu de données de sortie Hello est les lecteurs hello planification (horaire, quotidienne, etc.). Par conséquent, vous devez spécifier le jeu de données de sortie hello même si l’activité hello ne produit pas vraiment une sortie.

### <a name="prerequisites"></a>Composants requis
1. Créer un **compte de stockage Azure à usage général** en suivant les instructions de procédure pas à pas hello : [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Créer un **cluster Apache Spark dans Azure HDInsight** en suivant les instructions dans le didacticiel de hello : [cluster créer Apache Spark dans Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Associer un compte de stockage Azure hello que vous avez créé à l’étape 1 de # avec ce cluster.  
3. Téléchargez et lisez le fichier de script python hello **test.py** situé à : [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Télécharger **test.py** toohello **pyFiles** dossier Bonjour **adfspark** conteneur dans votre stockage d’objets Blob Azure. Créer le conteneur de hello et le dossier de hello s’ils n’existent pas.

### <a name="create-data-factory"></a>Créer une fabrique de données
Commençons par créer la fabrique de données hello dans cette étape.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **nouveau** sur menu gauche hello **données + Analytique**, puis cliquez sur **Data Factory**.
3. Bonjour **nouvelle fabrique de données** panneau, entrez **SparkDF** pour hello nom.

   > [!IMPORTANT]
   > nom de Hello de fabrique de données Azure hello doit être **global unique**. Si vous voyez l’erreur de hello : **nom de fabrique de données « SparkDF » n’est pas disponible**. Modifier le nom hello hello fabrique de données (par exemple, yournameSparkDFdate et essayez à nouveau de créer. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.   
4. Sélectionnez hello **abonnement Azure** où vous souhaitez toobe de fabrique de données hello créé.
5. Sélectionnez un **groupe de ressources** Azure existant ou créez-en un.
6. Sélectionnez **toodashboard du code confidentiel** option.  
6. Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.

   > [!IMPORTANT]
   > instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.
7. Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure comme suit :   
8. Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données. Si vous ne voyez pas la page de fabrique de données hello, cliquez sur mosaïque hello pour votre fabrique de données sur le tableau de bord hello.

    ![Panneau Data Factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Créez des services liés
Dans cette étape, vous créez deux services liés, un toolink votre fabrique de données tooyour cluster Spark et hello autres toolink votre fabrique de données de stockage Azure tooyour.  

#### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage. Un jeu de données que vous créez dans une étape ultérieure de cette procédure fait référence toothis lié service. Hello service lié HDInsight que vous définissez dans l’étape suivante de hello fait référence toothis lié service.  

1. Cliquez sur **auteur et déployer** sur hello **Data Factory** Panneau de votre fabrique de données. Vous devez voir hello éditeur Data Factory.
2. Cliquez sur **Nouveau magasin de données** et choisissez **Stockage Azure**.

   ![Nouveau magasin de données - Stockage Azure - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Vous devez voir hello **script JSON** pour la création d’un stockage Azure des service dans l’éditeur de hello lié.

   ![Service lié Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Remplacez **nom de compte** et **clé de compte** avec la clé de hello accès et le nom de votre compte de stockage Azure. toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy hello service lié, cliquez sur **déployer** sur la barre de commandes hello. Une fois hello service lié est déployé avec succès, hello **Draft-1** fenêtre doit disparaître et vous voyez **AzureStorageLinkedService** dans l’arborescence hello sur hello gauche.

#### <a name="create-hdinsight-linked-service"></a>Créer un service lié Azure HDInsight
Dans cette étape, vous créez toolink du service lié HDInsight Azure votre fabrique de données toohello cluster HDInsight Spark. cluster HDInsight de Hello est programme de Spark hello utilisé toorun spécifié dans l’activité de Spark hello du pipeline hello dans cet exemple.  

1. Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** dans la barre d’outils de hello, cliquez sur **nouveau calcul**, puis cliquez sur **cluster HDInsight**.

    ![Créer un service lié Azure HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Copiez et collez hello suivant extrait toohello **Draft-1** fenêtre. Dans l’éditeur JSON hello, procédez comme hello comme suit :
    1. Spécifiez hello **URI** pour hello HDInsight Spark cluster. Par exemple : `https://<sparkclustername>.azurehdinsight.net/`.
    2. Spécifiez le nom hello Hello **utilisateur** qui a cluster Spark de toohello accès.
    3. Spécifiez hello **mot de passe** pour l’utilisateur.
    4. Spécifiez hello **service lié Azure Storage** associé hello cluster HDInsight Spark. Dans cet exemple, il s’agit de **AzureStorageLinkedService**.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - L’activité Spark ne prend pas en charge les clusters Spark HDInsight qui utilisent Azure Data Lake Store en tant que stockage principal.
    > - L’activité Spark prend en charge uniquement le cluster Spark HDInsight existant (c’est-à-dire votre propre cluster). Elle ne prend pas en charge les services liés HDInsight à la demande.

    Consultez [Service lié HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) pour plus d’informations sur hello HDInsight le service lié.
3.  toodeploy hello service lié, cliquez sur **déployer** sur la barre de commandes hello.  

### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
jeu de données de sortie Hello est les lecteurs hello planification (horaire, quotidienne, etc.). Par conséquent, vous devez spécifier un jeu de données de sortie pour l’activité de spark hello dans le pipeline de hello même si l’activité hello ne produit pas vraiment de sortie. Spécification d’un jeu de données d’entrée pour l’activité de hello est facultative.

1. Bonjour **éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.  
2. Copiez et collez hello suivant fenêtre toohello Draft-1. extrait de code Hello JSON définit un jeu de données appelée **OutputDataset**. En outre, vous spécifiez que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfspark** et dossier hello appelé **pyFiles/sortie**. Comme mentionné précédemment, ce jeu de données est un jeu de données factice. programme de Spark Hello dans cet exemple ne produit pas de sortie. Hello **disponibilité** section spécifie ce jeu de données de sortie hello est produite quotidiennement.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
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
3. toodeploy hello du jeu de données, cliquez sur **déployer** sur la barre de commandes hello.


### <a name="create-pipeline"></a>Création d’un pipeline
Dans cette étape, vous allez créer un pipeline avec une activité **HDInsightSpark**. Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie. Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello. Par conséquent, aucun jeu de données d’entrée n’est spécifié dans cet exemple.

1. Bonjour **éditeur Data Factory**, cliquez sur **... Plus** sur hello de barre de commandes, puis cliquez sur **nouveau pipeline**.
2. Remplacez le script hello dans la fenêtre hello Draft-1 avec hello script suivant :

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Hello Notez les points suivants :
    - Hello **type** propriété a la valeur trop**HDInsightSpark**.
    - Hello **rootPath** est défini trop**adfspark\\pyFiles** où adfspark est le conteneur d’objets Blob Azure hello et pyFiles est un dossier précis dans le conteneur. Dans cet exemple, hello stockage d’objets Blob Azure est hello qui est associé au cluster de Spark hello. Vous pouvez télécharger hello fichier tooa stockage Azure différent. Si vous procédez ainsi, vous pouvez créer un toolink de service lié Azure Storage cette fabrique de données de stockage compte toohello. Ensuite, spécifiez le nom hello du service de hello lié en tant que valeur pour hello **sparkJobLinkedService** propriété. Consultez [propriétés de l’activité de Spark](#spark-activity-properties) pour plus d’informations sur cette propriété et d’autres propriétés prises en charge par hello Spark activité.  
    - Hello **entryFilePath** a la valeur toohello **test.py**, qui est le fichier de python hello.
    - Hello **getDebugInfo** propriété a la valeur trop**toujours**, ce qui signifie que les fichiers journaux de hello est toujours généré (succès ou échec).

        > [!IMPORTANT]
        > Nous recommandons que vous ne définissez pas cette propriété trop`Always` dans un environnement de production, sauf si vous dépannez un problème.
    - Hello **génère** section a un jeu de données de sortie. Vous devez spécifier un jeu de données de sortie même si le programme de spark hello ne produit pas de sortie. planification de hello lecteurs Hello sortie dataset pour le pipeline de hello (horaire, quotidienne, etc.).  

        Pour plus d’informations sur les propriétés hello pris en charge par l’activité de Spark, consultez [nouvelles propriétés de l’activité](#spark-activity-properties) section.
3. pipeline de hello toodeploy, cliquez sur **déployer** sur la barre de commandes hello.

### <a name="monitor-pipeline"></a>Surveillance d’un pipeline
1. Cliquez sur **X** tooclose éditeur Data Factory panneaux et toonavigate sauvegarder toohello page d’accueil de Data Factory. Cliquez sur **analyse et gestion** hello toolaunch analyse de l’application dans un autre onglet.

    ![Mosaïque Surveiller et gérer](media/data-factory-spark/monitor-and-manage-tile.png)
2. Hello de modification **l’heure de début** trop de filtre en haut de hello**2/1/2017**, puis cliquez sur **appliquer**.
3. Vous devez voir qu’une seule fenêtre d’activité qu’il existe un seul jour entre hello début (2017-02-01) et de fin des heures (2017-02-02) du pipeline de hello. Confirmer cette tranche de données hello est **prêt** état.

    ![Pipeline d’analyse hello](media/data-factory-spark/monitor-and-manage-app.png)    
4. Sélectionnez hello **fenêtre d’activité** toosee plus d’informations sur l’exécution de l’activité hello. S’il existe une erreur, vous consultez les détails à ce sujet dans le volet de droite hello.

### <a name="verify-hello-results"></a>Vérifier les résultats de hello

1. Lancez le **bloc-notes Jupyter** pour votre cluster Spark HDInsight via l’URL suivante : https://NOMDUCLUSTER.azurehdinsight.net/jupyter. Vous pouvez également lancer le tableau de bord de votre cluster Spark HDInsight, puis ouvrir le **bloc-notes Jupyter**.
2. Cliquez sur **nouveau** -> **PySpark** toostart un nouvel ordinateur portable.

    ![Nouveau bloc-notes Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. Exécution hello commande suivante copie/collage de texte hello et appuyez sur **MAJ + ENTRÉE** à fin hello d’instruction de deuxième hello.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Vérifiez que les données de salutation à partir de la table de hvac hello :  

    ![Résultats de la requête Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

Consultez la section relative à [l’exécution d’une requête SQL Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) pour obtenir des instructions détaillées. 

### <a name="troubleshooting"></a>Résolution des problèmes
Étant donné que vous définissez **getDebugInfo** trop**toujours**, vous voyez un **journal** sous-dossier Bonjour **pyFiles** dossier dans votre conteneur d’objets Blob Azure. fichier de journal Hello dans le dossier du journal hello fournit des détails supplémentaires. Ce fichier journal est particulièrement utile en cas d’erreur. Dans un environnement de production, vous souhaiterez peut-être tooset il trop**échec**.

Pour résoudre le problème, procédez comme hello comme suit :


1. Accédez trop`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![Application d’interface utilisateur YARN](media/data-factory-spark/yarnui-application.png)  
2. Cliquez sur **journaux** pour l’une des hello exécuter tentatives.

    ![Page d’application](media/data-factory-spark/yarn-applications.png)
3. Vous devez voir les informations d’erreur supplémentaires dans la page du journal hello.

    ![Erreur du journal](media/data-factory-spark/yarnui-application-error.png)

Hello les sections suivantes fournit des informations sur le cluster d’Apache Spark Data Factory entités toouse et l’activité de Spark dans votre fabrique de données.

## <a name="spark-activity-properties"></a>Propriétés de l'activité Spark
Voici hello exemple JSON de définition d’un pipeline avec Spark activité :    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Hello tableau suivant décrit les propriétés JSON hello utilisées Bonjour définition JSON :

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| name | Nom de l’activité hello dans le pipeline de hello. | Oui |
| description | Texte décrivant de quelle activité hello effectue. | Non |
| type | Cette propriété doit être définie tooHDInsightSpark. | Oui |
| linkedServiceName | Nom de hello HDInsight lié service sur le hello Spark programme s’exécute. | Oui |
| rootPath | conteneur d’objets Blob Azure Hello et le dossier qui contient le fichier de Spark hello. nom de fichier Hello respecte la casse. | Oui |
| entryFilePath | Dossier racine du toohello chemin d’accès relatif de hello Spark/package de code. | Oui |
| className | Classe principale Java/Spark de l’application. | Non |
| arguments | Une liste de programme de Spark toohello des arguments de ligne de commande. | Non |
| proxyUser | programme Spark de Hello utilisateur compte tooimpersonate tooexecute hello | Non |
| sparkConfig | Spécifier les valeurs des propriétés de configuration Spark répertoriées dans la rubrique de hello : [Configuration Spark - propriétés de l’Application](https://spark.apache.org/docs/latest/configuration.html#available-properties). | Non |
| getDebugInfo | Spécifie les fichiers journaux hello Spark toohello copié le stockage Azure utilisé par le cluster HDInsight (ou) spécifié par sparkJobLinkedService. Valeurs autorisées : Aucun, Toujours ou Échec. Valeur par défaut : Aucun. | Non |
| sparkJobLinkedService | Hello service lié Azure Storage qui contient les journaux, les dépendances et les fichiers de travail hello Spark.  Si vous ne spécifiez pas une valeur pour cette propriété, le stockage de hello associé au cluster HDInsight est utilisé. | Non |

## <a name="folder-structure"></a>Structure de dossiers
Hello activité de Spark ne prend pas en charge un script en ligne en tant que Pig et effectuer des activités de la ruche. Les travaux Spark sont également plus extensibles que les travaux Pig/Hive. Pour les travaux de Spark, vous pouvez fournir plusieurs dépendances, telles que les packages (placés dans java de hello CLASSPATH), python fichiers jar (placés sur hello PYTHONPATH) et tous les autres fichiers.

Créer hello suivant la structure de dossiers Bonjour référencé par hello service lié HDInsight le stockage Blob Azure. Ensuite, téléchargez les fichiers dépendants toohello approprié sous-dossiers dans le dossier racine de hello représenté par **entryFilePath**. Par exemple, téléchargez le sous-dossier de python fichiers toohello pyFiles et jar fichiers toohello fichiers JAR sous-dossier du dossier racine de hello. Lors de l’exécution, service Data Factory attend hello suivant la structure de dossiers Bonjour le stockage Blob Azure :     

| Chemin | Description | Requis | Type |
| ---- | ----------- | -------- | ---- |
| . | chemin d’accès racine de Hello du travail de Spark hello dans le service de stockage lié hello    | Oui | Dossier |
| &lt;défini par l’utilisateur &gt; | chemin d’accès Hello pointant vers le fichier d’entrée toohello du travail de Spark hello | Oui | Fichier |
| ./jars | Tous les fichiers sous ce dossier sont téléchargés et placés sur le chemin de classe java hello du cluster de hello | Non | Dossier |
| ./pyFiles | Tous les fichiers sous ce dossier sont téléchargés et placés sur hello PYTHONPATH du cluster de hello | Non | Dossier |
| ./files | Tous les fichiers dans ce dossier sont téléchargés et placés dans le répertoire de travail de l’exécuteur | Non | Dossier |
| ./archives | Tous les fichiers dans ce dossier ne sont pas compressés | Non | Dossier |
| ./logs | dossier Hello sur lequel sont enregistrés les journaux de cluster de Spark hello.| Non | Dossier |

Voici un exemple pour un stockage qui contient deux fichiers de travail Spark Bonjour Azure Blob Storage référencé par hello service lié HDInsight.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
