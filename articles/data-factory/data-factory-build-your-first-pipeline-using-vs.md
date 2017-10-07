---
title: "aaaBuild votre première fabrique de données (Visual Studio) | Documents Microsoft"
description: "Dans ce didacticiel, vous allez créer un exemple de pipeline Azure Data Factory avec Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Didacticiel : Créer une fabrique de données à l’aide de Visual Studio
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-build-your-first-pipeline.md)
> * [Portail Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modèle Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Ce didacticiel vous montre comment toocreate une fabrique de données Azure à l’aide de Visual Studio. Vous créez un projet Visual Studio à l’aide du modèle de projet de Data Factory hello définissez des entités de fabrique de données (services liés, des datasets et pipeline) au format JSON et ensuite publierez/déployez ces cloud de toohello d’entités. 

pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**. Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce. pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin. 

> [!NOTE]
> Ce didacticiel n’explique pas comment copier des données à l’aide d’Azure Data Factory. Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>Procédure pas à pas : Création et publication d’entités Data Factory
Voici les étapes hello que vous effectuez dans le cadre de cette procédure pas à pas :

1. Créez deux services liés : **AzureStorageLinkedService1** et **HDInsightOnDemandLinkedService1**. 
   
    Dans ce didacticiel, les données d’entrée et de sortie pour l’activité de ruche hello sont dans hello même stockage d’objets Blob Azure. Vous utilisez une à la demande HDInsight cluster tooprocess des données d’entrée tooproduce sortie données existantes. cluster de HDInsight Hello à la demande est automatiquement créé pour vous par Azure Data Factory en cours d’exécution lorsque les données d’entrée hello sont prêt toobe traité. Vous devez toolink vos données stockent et calcule la fabrique de données tooyour afin que le service de fabrique de données hello peut se connecter à toothem lors de l’exécution. Par conséquent, vous liez votre fabrique de données toohello compte de stockage Azure à l’aide de hello AzureStorageLinkedService1 et liez un cluster de HDInsight à la demande à l’aide de hello HDInsightOnDemandLinkedService1. Lors de la publication, vous spécifiez le nom hello toobe de fabrique de données hello créé ou une fabrique de données.  
2. Créez deux jeux de données : **InputDataset** et **OutputDataset**, qui représentent les données d’entrée/sortie hello stockées Bonjour stockage d’objets blob Azure. 
   
    Ces définitions de jeu de données font référence toohello lié Azure Storage service est créé à l’étape précédente de hello. Pourquoi InputDataset, vous spécifiez le conteneur d’objets blob hello (adfgetstarted) et hello dossier (inptutdata) qui contient un objet blob avec les données d’entrée hello. Pourquoi OutputDataset, vous spécifiez le conteneur d’objets blob hello (adfgetstarted) et le dossier hello (partitioneddata) qui contient les données de sortie hello. Vous spécifiez également d’autres propriétés telles que la structure, la disponibilité et la stratégie.
3. Créez un pipeline nommé **MyFirstPipeline**. 
  
    Dans cette procédure pas à pas, le pipeline de hello n'a qu’une seule activité : **activité de la ruche HDInsight**. Cette transformation de l’activité d’entrée de données de sortie de données tooproduce en exécutant un script hive sur un cluster de HDInsight à la demande. toolearn en savoir plus sur l’activité hive, consultez [activité Hive](data-factory-hive-activity.md) 
4. Créez une fabrique de données nommée **DataFactoryUsingVS**. Déployer la fabrique de données hello et toutes les entités de fabrique de données (services liés, les tables et les pipeline hello).
5. Après la publication, vous utilisez panneaux portail Azure et pipeline de hello toomonitor analyse & application de gestion. 
  
### <a name="prerequisites"></a>Composants requis
1. Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes. Vous pouvez également sélectionner hello **vue d’ensemble et conditions préalables** option dans la liste déroulante de hello à l’article de toohello hello tooswitch supérieur. Après avoir terminé la configuration requise de hello, passer toothis précédent article en sélectionnant **Visual Studio** option dans la liste déroulante de hello.
2. instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.  
3. Vous devez disposer de hello installé sur votre ordinateur :
   * Visual Studio 2013 ou Visual Studio 2015
   * Téléchargez le Kit de développement logiciel (SDK) Azure pour Visual Studio 2013 ou Visual Studio 2015. Accédez trop[Page de téléchargement Azure](https://azure.microsoft.com/downloads/) et cliquez sur **VS 2013** ou **VS 2015** Bonjour **.NET** section.
   * Téléchargement du plug-in Azure Data Factory dernière hello pour Visual Studio : [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Vous pouvez également actualiser les plug-in hello en procédant comme hello comme suit : cliquez sur hello, **outils** -> **Extensions et mises à jour** -> **Online**  ->  **Galerie visual Studio** -> **Microsoft Azure Data Factory Tools pour Visual Studio** -> **mise à jour**.

Maintenant, nous allons utiliser Visual Studio toocreate une fabrique de données Azure.

### <a name="create-visual-studio-project"></a>Création d’un projet Visual Studio
1. Lancez **Visual Studio 2013** ou **Visual Studio 2015**. Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**. Vous devez voir hello **nouveau projet** boîte de dialogue.  
2. Bonjour **nouveau projet** boîte de dialogue, sélectionnez hello **DataFactory** modèle, puis cliquez sur **projet de la fabrique de données vide**.   

    ![Boîte de dialogue Nouveau projet](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Entrez un **nom** pour le projet de hello, **emplacement**et un nom pour hello **solution**, puis cliquez sur **OK**.

    ![Explorateur de solutions](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Créer des services liés
Au cours de cette étape, vous allez créer deux services liés : **Stockage Azure** et **HDInsight à la demande**. 

Hello Azure Storage liés aux liaisons de service votre fabrique de données de stockage Azure compte toohello en fournissant des informations de connexion hello. Service de fabrique de données utilise la chaîne de connexion de hello à partir du paramètre de service hello lié tooconnect toohello stockage Azure lors de l’exécution. Ce système de stockage conserve d’entrée et les données de sortie pour le pipeline de hello et hello hive le fichier de script utilisé par l’activité de ruche hello. 

Service lié HDInsight à la demande hello cluster HDInsight est créé automatiquement lors de l’exécution lorsque les données d’entrée hello tooprocessed prêt. cluster de Hello est supprimée une fois ceci effectué inactifs et le traitement de la durée spécifiée hello. 

> [!NOTE]
> Vous créez une fabrique de données en spécifiant son nom et les paramètres au moment de hello de votre solution de fabrique de données de publication.

#### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
1. Avec le bouton droit **Services liés** hello l’Explorateur de solutions, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.      
2. Bonjour **ajouter un nouvel élément** boîte de dialogue, sélectionnez **Service lié Azure Storage** à partir de la liste de hello, puis cliquez sur **ajouter**.
    ![Service lié Azure Storage](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Remplacez `<accountname>` et `<accountkey>` avec nom hello de votre compte de stockage Azure et sa clé. toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Service lié Azure Storage](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Enregistrer hello **AzureStorageLinkedService1.json** fichier.

#### <a name="create-azure-hdinsight-linked-service"></a>Créer le service lié Azure HDInsight
1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **Services liés**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.
2. Sélectionnez **Service lié à la demande HDInsight** puis cliquez sur **Ajouter**.
3. Remplacez hello **JSON** avec hello suivant JSON :

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

    Propriété | Description
    -------- | ----------- 
    ClusterSize | Spécifie la taille de hello Hello cluster HDInsight Hadoop.
    TimeToLive | Spécifie la durée d’inactivité de ce hello pour le cluster HDInsight de hello, avant d’être supprimé.
    linkedServiceName | Spécifie le compte de stockage hello toostore utilisé hello journaux générés par le cluster HDInsight Hadoop. 

    > [!IMPORTANT]
    > Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (linkedServiceName). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Avec le service lié HDInsight à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (timeToLive). Hello cluster est automatiquement supprimé lorsque le traitement de hello est effectué.
    > 
    > Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.

    Pour plus d’informations sur les propriétés JSON, consultez [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). 
4. Enregistrer hello **HDInsightOnDemandLinkedService1.json** fichier.

### <a name="create-datasets"></a>Créez les jeux de données
Dans cette étape, vous créez des groupes de données toorepresent hello d’entrée et sortie des données pour le traitement de la ruche. Ces jeux de données font référence toohello **AzureStorageLinkedService1** que vous avez créé précédemment dans ce didacticiel. Hello tooan de points de service lié compte de stockage Azure et de jeux de données spécifiez conteneur, dossier, le nom de fichier dans le stockage hello qui contient l’entrée et les données de sortie.   

#### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **Tables**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.
2. Sélectionnez **objets Blob Azure** à partir de la liste de hello, renommez hello du fichier de hello trop**InputDataSet.json**, puis cliquez sur **ajouter**.
3. Remplacez hello **JSON** dans l’éditeur de hello avec hello suivant extrait de code JSON :

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    Cet extrait de code JSON définit un jeu de données appelée **AzureBlobInput** qui représente les données d’entrée pour l’activité de ruche hello dans le pipeline de hello. Vous spécifiez que les données d’entrée hello se trouve dans le conteneur d’objets blob hello appelé `adfgetstarted` et dossier hello appelé `inputdata`.

    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

    Propriété | Description |
    -------- | ----------- |
    type |propriété de type Hello est définie trop**AzureBlob** , car les données résident dans le stockage d’objets Blob Azure.
    linkedServiceName | Fait référence toohello AzureStorageLinkedService1 que vous avez créé précédemment.
    fileName |Cette propriété est facultative. Si vous omettez cette propriété, tous les fichiers hello hello folderPath sont récupérées. Dans ce cas, uniquement les input.log hello est traitée.
    type | les fichiers journaux Hello étant au format texte, nous utilisons TextFormat. |
    columnDelimiter | colonnes dans les fichiers journaux de hello sont délimitées par virgule hello (`,`)
    frequency/interval | fréquence égale tooMonth et l’intervalle est 1, ce qui signifie que les tranches d’entrée hello sont disponibles chaque mois.
    external | Cette propriété a la valeur tootrue si les données d’entrée pour l’activité de hello de salutation ne sont pas générées par le pipeline de hello. Cette propriété est uniquement spécifiée sur les jeux de données d’entrée. Pour hello dataset d’entrée de la première activité hello, toujours définir tootrue.
4. Enregistrer hello **InputDataset.json** fichier.

#### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
Maintenant, vous créez hello sortie dataset toorepresent sortie les données stockées dans hello le stockage Blob Azure.

1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **tables**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.
2. Sélectionnez **objets Blob Azure** à partir de la liste de hello, renommez hello du fichier de hello trop**OutputDataset.json**, puis cliquez sur **ajouter**.
3. Remplacez hello **JSON** dans l’éditeur de hello avec hello suivant JSON :
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    extrait de code Hello JSON définit un jeu de données appelée **AzureBlobOutput** qui représente les données produites par hello ruche activité hello pipeline de sortie. Vous spécifiez que la sortie hello données sont générées par l’activité de ruche hello est placé dans le conteneur d’objets blob hello appelé `adfgetstarted` et dossier hello appelé `partitioneddata`. 
    
    Hello **disponibilité** section spécifie ce jeu de données de sortie hello est généré sur une base mensuelle. planification de hello lecteurs Hello sortie dataset du pipeline de hello. pipeline de Hello s’exécute chaque mois entre les heures de début et de fin. 

    Consultez **créer le jeu de données d’entrée hello** section pour obtenir une description de ces propriétés. Vous ne définissez pas la propriété d’externe de hello sur un jeu de données de sortie comme jeu de données hello est généré par le pipeline de hello.
4. Enregistrer hello **OutputDataset.json** fichier.

### <a name="create-pipeline"></a>Création d’un pipeline
Vous avez créé jusqu'à présent service lié Azure Storage de hello et jeux de données d’entrée et de sortie. Vous allez maintenant créer un pipeline avec une activité **HDInsightHive**. Hello **d’entrée** pour la ruche de hello activité est définie trop**AzureBlobInput** et **sortie** est défini trop**AzureBlobOutput**. Un secteur d’un jeu de données d’entrée est disponible mensuellement (fréquence : mois, intervalle : 1), hello sortie tranche est générée chaque mois trop. 

1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **Pipelines**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément.**
2. Sélectionnez **Pipeline de Transformation Hive** à partir de la liste de hello, puis cliquez sur **ajouter**.
3. Remplacez hello **JSON** avec hello suivant extrait de code :

    > [!IMPORTANT]
    > Remplacez `<storageaccountname>` par nom de hello de votre compte de stockage.

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
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > Remplacez `<storageaccountname>` par nom de hello de votre compte de stockage.

    extrait de code Hello JSON définit un pipeline qui se compose d’une seule activité (activité Hive). Cette activité exécute un ruche script tooprocess d’entrée de données sur un données de sortie à la demande HDInsight cluster tooproduce. Dans la section d’activités hello hello JSON du pipeline, vous ne voyez qu’une seule activité dans le tableau de hello avec le type de trop**HDInsightHive**. 

    Dans les propriétés de type hello qui sont des activités de ruche tooHDInsight spécifique, vous spécifiez le service lié Azure Storage a le fichier de script hive hello, fichier de script toohello hello chemin d’accès et fichier de script de toohello de paramètres. 

    fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans le compte de stockage Azure hello (spécifié par hello scriptLinkedService) et hello `script` dossier dans le conteneur de hello `adfgetstarted`.

    Hello `defines` section est de paramètres d’exécution utilisés toospecify hello script hive de toohello passés en tant que valeurs de configuration Hive (par exemple `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Hello **Démarrer** et **fin** propriétés de pipeline de hello spécifie la période active de hello du pipeline de hello. Vous avez configuré hello toobe de dataset généré tous les mois, par conséquent, une seule fois la tranche est produite par le pipeline de hello (étant donné que les mois hello sont identique sur les dates de début et de fin).

    Dans l’activité hello JSON, vous spécifiez ce script Hive hello s’exécute sur le calcul hello spécifié par hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.
4. Enregistrer hello **HiveActivity1.json** fichier.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>Ajouter partitionweblogs.hql et input.log comme dépendance
1. Avec le bouton droit **dépendances** Bonjour **l’Explorateur de solutions** fenêtre, pointez trop**ajouter**, puis cliquez sur **élément existant**.  
2. Accédez toohello **C:\ADFGettingStarted** et sélectionnez **partitionweblogs.hql**, **input.log** fichiers, puis cliquez sur **ajouter**. Vous avez créé ces deux fichiers dans le cadre de la configuration requise à partir de hello [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md).

Lorsque vous publiez la solution de hello dans l’étape suivante de hello, hello **partitionweblogs.hql** fichier est téléchargé toohello **script** dossier Bonjour `adfgetstarted` conteneur d’objets blob.   

### <a name="publishdeploy-data-factory-entities"></a>Publier/déployer des entités Data Factory
Dans cette étape, vous publiez des entités de fabrique de données hello (services liés, des datasets et pipeline) dans votre projet de toohello service Azure Data Factory. Dans le processus de hello de publication, vous spécifiez nom hello pour votre fabrique de données. 

1. Cliquez sur le projet dans l’Explorateur de solutions de hello, puis cliquez sur **publier**.
2. Si vous voyez **connecter tooyour compte Microsoft** boîte de dialogue, entrez vos informations d’identification de compte hello qui dispose d’abonnement Azure, puis cliquez sur **connectez-vous**.
3. Vous devez voir hello suivant la boîte de dialogue :

   ![Boîte de dialogue Publier](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. Bonjour **fabrique de données de configuration** page, procédez comme hello comme suit :

    ![Publier - Nouveau paramètres de fabrique de données](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. Sélectionnez l’option **Créer une fabrique de données** .
   2. Entrez une valeur unique **nom** de fabrique de données hello. Par exemple : **DataFactoryUsingVS09152016**. nom de Hello doit être globalement unique.
   3. Sélectionnez l’abonnement pour hello hello **abonnement** champ. 
        > [!IMPORTANT]
        > Si vous ne voyez pas d’un abonnement, assurez-vous que vous connecté en utilisant un compte qui est administrateur ou coadministrateur de l’abonnement de hello.
   4. Sélectionnez hello **groupe de ressources** pour toobe de fabrique de données hello créé.
   5. Sélectionnez hello **région** de fabrique de données hello.
   6. Cliquez sur **suivant** tooswitch toohello **publier des éléments** page. (Appuyez sur **onglet** toomove hors Bonjour nom champ tooif Bonjour **suivant** bouton est désactivé.)

    > [!IMPORTANT]
    > Si vous recevez une erreur de hello **nom de fabrique de données « DataFactoryUsingVS » n’est pas disponible** lors de la publication, modifiez le nom de hello (par exemple, yournameDataFactoryUsingVS). Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.   
1. Bonjour **publier des éléments** , vérifiez que tous les hello fabriques de données entités sont sélectionnées, puis cliquez sur **suivant** tooswitch toohello **Résumé** page.

    ![Page Publier des éléments](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Passez en revue la synthèse de hello et cliquez sur **suivant** toostart Bonjour déploiement processus et vue Bonjour **état du déploiement**.

    ![Page de résumé](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. Bonjour **état du déploiement** page, vous devez voir État hello hello du processus de déploiement. Après le déploiement de hello, cliquez sur Terminer.

Toonote des points importants suivants :

- Si vous recevez une erreur de hello : **cet abonnement n’est pas un espace de noms inscrit toouse Microsoft.DataFactory**, effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :
    - Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello Data Factory.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Connexion à l’aide de hello abonnement Azure dans toohello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure. Cette action enregistre automatiquement le fournisseur hello pour vous.
- nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.
- instances de fabrique de données toocreate, vous devez toobe un administrateur ou coadministrateur de hello abonnement Azure

### <a name="monitor-pipeline"></a>Surveillance d’un pipeline
Dans cette étape, vous surveillez pipeline hello à l’aide de la vue de diagramme de la fabrique de données hello. 

#### <a name="monitor-pipeline-using-diagram-view"></a>Surveillance d’un pipeline à l’aide de la Vue de diagramme
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/), hello comme suit :
   1. Cliquez sur **Plus de services**, puis sur **Fabriques de données**.
       
        ![Parcourir les fabriques de données](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Nom hello Sélectionnez votre fabrique de données (par exemple : **DataFactoryUsingVS09152016**) à partir de la liste de hello des fabriques de données.
   
       ![Sélectionner votre fabrique de données](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. Dans la page d’accueil hello pour votre fabrique de données, cliquez sur **diagramme**.

    ![Vignette schématique](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. Dans la vue de diagramme de hello, vous consultez une vue d’ensemble des pipelines de hello et jeux de données utilisés dans ce didacticiel.

    ![Vue du diagramme](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview diagramme de toutes les activités dans le pipeline de hello, pipeline avec le bouton droit dans hello et cliquez sur Ouvrir Pipeline.

    ![Menu Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Vérifiez que vous voyez hello HDInsightHive activité hello pipeline.

    ![Vue Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate sauvegarder toohello de vue précédente, cliquez sur **Data factory** dans le menu de navigation hello haut hello.
6. Bonjour **vue de diagramme**, double-cliquez sur le jeu de données hello **AzureBlobInput**. Confirmer que la tranche hello est **prêt** état. Il peut prendre quelques minutes pour hello tranche tooshow dans l’état Ready. Si elle ne se produit pas une fois que vous patientez un moment, consultez si vous avez des fichiers d’entrée hello (input.log) placé dans le conteneur de droite hello (`adfgetstarted`) et le dossier (`inputdata`). Et vous assurer que hello **externe** propriété hello de jeu de données d’entrée est définie trop**true**. 

   ![Segment d’entrée dans l’état Prêt](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Cliquez sur **X** tooclose **AzureBlobInput** panneau.
8. Bonjour **vue de diagramme**, double-cliquez sur le jeu de données hello **AzureBlobOutput**. Vous voyez ce secteur hello qui est en cours de traitement.

   ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. Lorsque le traitement est terminé, vous consultez la section hello dans **prêt** état.

   > [!IMPORTANT]
   > La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes). Par conséquent, s’attendent hello pipeline tootake **environ 30 minutes** tooprocess hello tranche.  
   
    ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Lorsque la tranche de hello est à **prêt** d’état, vérifiez hello `partitioneddata` dossier Bonjour `adfgetstarted` conteneur dans votre stockage d’objets blob pour hello les données de sortie.  

    ![données de sortie](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Cliquez sur Détails de toosee hello tranche sur celui-ci dans un **tranche de données** panneau.

    ![Détails de la tranche](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Cliquez sur une activité à exécuter dans hello **liste s’exécute l’activité** toosee des détails sur une activité exécuter (activité Hive dans notre scénario) dans un **détails de la série activité** fenêtre. 
  
    ![Détails de l'exécution d'activité](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    À partir de fichiers de journal hello, vous pouvez voir la requête Hive hello qui a été exécutée et les informations d’état. Ces journaux sont utiles pour résoudre les problèmes.  

Consultez [analyser des jeux de données et le pipeline](data-factory-monitor-manage-pipelines.md) pour obtenir des instructions sur la façon dont pipeline de hello toouse hello toomonitor portail Azure et les jeux de données vous avez créé dans ce didacticiel.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>Surveiller le pipeline à l’aide de l’application de surveillance et de gestion
Vous pouvez également utiliser le moniteur et gérer les applications toomonitor vos pipelines. Pour en savoir plus sur l’utilisation de cette application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).

1. Cliquez sur la vignette Surveiller et gérer.

    ![Vignette Surveiller et gérer](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. L’application de surveillance et de gestion devrait s’afficher. Hello de modification **l’heure de début** et **heure de fin** toomatch début (04-01-2016 12:00 AM) et l’heure de fin (04-02-2016 12:00 AM) de votre pipeline, puis cliquez sur **appliquer**.

    ![Application de surveillance et gestion](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. toosee plus d’informations sur une fenêtre d’activité, sélectionnez-la dans hello **liste activité Windows** toosee des informations à son.
    ![Détails de la fenêtre d’activité](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès. Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, télécharger hello fichier d’entrée (input.log) toohello `inputdata` dossier Hello `adfgetstarted` conteneur.

### <a name="additional-notes"></a>Remarques supplémentaires
- Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive les données d’entrée. Consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour tous les hello sources et récepteurs pris en charge par l’activité de copie de hello. Consultez [services liés de calcul](data-factory-compute-linked-services.md) pour la liste des services de calcul pris en charge par la fabrique de données hello.
- Services liés lier des magasins de données ou la fabrique de données Azure tooan de services de calcul. Consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour tous les hello sources et récepteurs pris en charge par l’activité de copie de hello. Consultez [services liés de calcul](data-factory-compute-linked-services.md) pour la liste des services de calcul pris en charge par la fabrique de données hello et [des activités de transformation](data-factory-data-transformation-activities.md) qui peut s’exécuter sur ces derniers.
- Consultez [déplacer des données à partir de / tooAzure d’objets Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur les propriétés JSON utilisées Bonjour Azure Storage lié définition de service.
- Vous pouvez utiliser votre propre cluster HDInsight au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .
-  Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello précédant JSON. Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
- Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (linkedServiceName). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Avec le service lié HDInsight à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (timeToLive). Hello cluster est automatiquement supprimé lorsque le traitement de hello est effectué.
    
    Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.
- Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie. Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello. 
- Ce didacticiel n’explique pas comment copier des données à l’aide d’Azure Data Factory. Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Utiliser des fabriques de données de l’Explorateur de serveurs tooview
1. Dans **Visual Studio**, cliquez sur **vue** hello menu et cliquez sur **l’Explorateur de serveurs**.
2. Dans la fenêtre de l’Explorateur de serveurs hello, développez **Azure** et développez **Data Factory**. Si vous voyez **connecter tooVisual Studio**, entrez hello **compte** associé à votre abonnement Azure et d’un clic **continuer**. Saisissez le **mot de passe**, puis cliquez sur **Se connecter**. Visual Studio essaie de tooget d’informations sur toutes les fabriques de données Azure dans votre abonnement. Vous voyez l’état hello de cette opération Bonjour **liste des tâches données fabrique** fenêtre.

    ![Explorateur de serveurs](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. Vous pouvez cliquez sur une fabrique de données, puis sélectionnez **tooNew d’exporter la fabrique de données projet** toocreate un projet Visual Studio basé sur une fabrique de données.

    ![Exporter la fabrique de données](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Mettre à jour des outils Data Factory pour Visual Studio
outils d’Azure Data Factory tooupdate pour Visual Studio, procédez comme hello comme suit :

1. Cliquez sur **outils** sur hello menu et sélectionnez **Extensions et mises à jour**.
2. Sélectionnez **mises à jour** dans hello du volet gauche, puis sélectionnez **galerie Visual Studio**.
3. Sélectionnez **Outils Azure Data Factory pour Visual Studio**, puis cliquez sur **Mettre à jour**. Si vous ne voyez pas cette entrée, vous avez déjà la version la plus récente des outils de hello hello.

## <a name="use-configuration-files"></a>Utiliser des fichiers de configuration
Vous pouvez utiliser des fichiers de configuration dans les propriétés de tooconfigure Visual Studio pour les services/tables/pipelines liés différemment pour chaque environnement.

Envisagez de hello définition JSON pour un service lié Azure Storage. toospecify **connectionString** avec des valeurs différentes pour accountname et accountkey selon hello environnement (développement/Test/Production) toowhich vous déployez des entités de fabrique de données. Vous pouvez parvenir à ce comportement en utilisant un fichier de configuration distinct pour chaque environnement.

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

### <a name="add-a-configuration-file"></a>Ajouter un fichier de configuration
Ajoutez un fichier de configuration pour chaque environnement en effectuant hello comme suit :   

1. Cliquez sur le projet de Data Factory hello dans votre solution Visual Studio, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.
2. Sélectionnez **Config** à partir de la liste hello de modèles installés sur hello gauche, sélectionnez **fichier de Configuration**, entrez un **nom** pour la configuration de hello fichier, puis cliquez sur **Ajouter**.

    ![Ajouter un fichier de configuration](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Ajouter des paramètres de configuration et leurs valeurs Bonjour suivant le format :

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    Cet exemple configure la propriété connectionString d’un service lié Azure Storage et d’un service lié SQL Azure. Notez que la syntaxe de hello pour spécifier un nom est [JsonPath](http://goessner.net/articles/JsonPath/).   

    Si JSON possède une propriété qui a un tableau de valeurs comme indiqué dans hello suivant de code :  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Configurez les propriétés comme indiqué dans hello suivant du fichier de configuration (Utilisez zéro) :

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Noms de propriétés avec des espaces
Si un nom de propriété comporte des espaces, utilisez des crochets comme indiqué dans hello (nom du serveur de base de données) de l’exemple suivant :

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Déployer une solution à l’aide d’une configuration
Lorsque vous publiez des entités d’Azure Data Factory dans Visual Studio, vous pouvez spécifier la configuration hello que vous souhaitez toouse pour cette opération de publication.

entités toopublish dans un projet Azure Data Factory à l’aide du fichier de configuration :   

1. Cliquez sur le projet de la fabrique de données, sur **publier** toosee hello **publier des éléments** boîte de dialogue.
2. Sélectionnez une fabrique de données existante ou de spécifier des valeurs pour la création d’une fabrique de données sur hello **fabrique de données de configuration** page, puis cliquez sur **suivant**.   
3. Sur hello **publier des éléments** page : une liste déroulante avec les configurations disponibles pour hello **sélectionner une configuration de déploiement** champ.

    ![Sélectionner un fichier de config](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Sélectionnez hello **fichier de configuration** que vous souhaitez toouse et cliquez sur **suivant**.
5. Vérifiez que vous voyez le nom hello du fichier JSON Bonjour **Résumé** page, puis cliquez sur **suivant**.
6. Cliquez sur **Terminer** une fois l’opération de déploiement hello est terminée.

Lorsque vous déployez, hello valeurs hello fichier de configuration sont tooset utilisé les valeurs des propriétés dans les fichiers au format JSON hello avant que les entités hello soient déployé tooAzure service Data Factory.   

## <a name="use-azure-key-vault"></a>Utiliser Azure Key Vault
Il n’est pas recommandé et souvent sur des données sensibles de sécurité stratégie toocommit comme référentiel de code de connexion chaînes toohello. Consultez [ADF Secure publier](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample sur toolearn GitHub sur le stockage des informations sensibles dans Azure Key Vault et son utilisation lors de la publication des entités de fabrique de données. Hello Secure publier l’extension pour Visual Studio permet hello toobe de clés secrètes stockée dans le coffre de clés et uniquement les références toothem sont spécifiés dans les services liés / configurations de déploiement. Ces références sont résolues lors de la publication tooAzure des entités de fabrique de données. Ces fichiers peuvent ensuite être référentiel toosource validée sans exposer les clés secrètes.

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

Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, voir [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md). 


## <a name="see-also"></a>Voir aussi
| Rubrique | Description |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct flux de travail pilotés par les données pour votre entreprise ou votre scénario. |
| [Groupes de données](data-factory-create-datasets.md) |Cet article vous aide à comprendre les jeux de données dans Azure Data Factory. |
| [Activités de transformation des données](data-factory-data-transformation-activities.md) |Cet article fournit une liste des activités de transformation de données (par exemple, la transformation Hive HDInsight que vous avez utilisée dans ce didacticiel) prises en charge par Azure Data Factory. |
| [Planification et exécution](data-factory-scheduling-and-execution.md) |Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory. |
| [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.](data-factory-monitor-manage-app.md) |Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion. |
