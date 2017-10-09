---
title: "Didacticiel : Créer une données toocopy du pipeline Azure Data Factory (portail Azure) | Documents Microsoft"
description: "Dans ce didacticiel, vous utilisez toocreate portail Azure un pipeline Azure Data Factory comportant des données toocopy d’activité de copie à partir d’une base de données SQL Azure de tooan stockage blob Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Didacticiel : Utiliser toocreate portail Azure données toocopy de pipeline de fabrique de données 
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistant de copie](data-factory-copy-data-wizard-tutorial.md)
> * [Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Dans cet article, vous apprendrez comment toouse [portail Azure](https://portal.azure.com) toocreate une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure. Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.   

Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie. activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge. Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats). activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).

Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Composants requis
Terminer la configuration requise indiquée dans hello [conditions préalables didacticiels](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article avant d’effectuer ce didacticiel.

## <a name="steps"></a>Étapes
Voici les étapes hello que vous effectuez dans le cadre de ce didacticiel :

1. Créez une **fabrique de données** Azure. Dans cette étape, vous créez une fabrique de données nommée ADFTutorialDataFactory. 
2. Créer **services liés** dans la fabrique de données hello. Au cours de cette étape, vous allez créer deux services liés de types : Stockage Azure et base de données SQL Azure. 
    
    Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Création d’un conteneur et de téléchargé de compte de stockage de données toothis dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé une table SQL dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   
3. Créer des entrées et sorties **jeux de données** dans la fabrique de données hello.  
    
    service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello Spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

    De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. De plus, hello sortie SQL table dataset spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copié.
4. Créer un **pipeline** dans la fabrique de données hello. Dans cette étape, vous allez créer un pipeline avec une activité de copie.   
    
    activité de copie Hello copie des données à partir d’un objet blob dans la table du tooa du stockage blob Azure hello dans la base de données SQL Azure hello. Vous pouvez utiliser une activité de copie dans un pipeline toocopy des données d’une destination de tooany pris en charge source prise en charge. Pour obtenir la liste des magasins de données pris en charge, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Pipeline de hello moniteur. Dans cette étape, vous **moniteur** hello tranches de jeux de données d’entrée et de sortie à l’aide du portail Azure. 

## <a name="create-data-factory"></a>Créer une fabrique de données
> [!IMPORTANT]
> Complète [conditions préalables requises pour le didacticiel de hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si vous n’avez pas déjà fait.   

Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive données tooproduct sortie les données d’entrée. Commençons par créer la fabrique de données hello dans cette étape.

1. Après la connexion toohello [portail Azure](https://portal.azure.com/), cliquez sur **nouveau** sur menu gauche hello **données + Analytique**, puis cliquez sur **Data Factory**. 
   
   ![Nouveau -> DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. Bonjour **nouvelle fabrique de données** panneau :
   
   1. Entrez **ADFTutorialDataFactory** pour hello **nom**. 
      
         ![Panneau Nouvelle fabrique de données](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       nom de Hello de fabrique de données Azure hello doit être **global unique**. Si vous recevez hello l’erreur suivante, renommez hello fabrique de données hello (par exemple, yournameADFTutorialDataFactory) et réessayez de créer à nouveau. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Nom de la fabrique de données indisponible](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Sélectionnez votre Azure **abonnement** dans lequel vous souhaitez la fabrique de données toocreate hello. 
   3. Pourquoi **groupe de ressources**, effectuez l’une des hello comme suit :
      
      - Sélectionnez **utiliser l’existante**, puis sélectionnez un groupe de ressources existant à partir de la liste déroulante de hello. 
      - Sélectionnez **nouvel**, puis entrez le nom hello d’un groupe de ressources.   
         
          Certaines des étapes hello dans ce didacticiel supposent que vous utilisez hello nom : **ADFTutorialResourceGroup** pour le groupe de ressources hello. toolearn sur les groupes de ressources, consultez [à l’aide de la ressource groupes toomanage vos ressources Azure](../azure-resource-manager/resource-group-overview.md).  
   4. Sélectionnez hello **emplacement** de fabrique de données hello. Seules les régions pris en charge par hello service Data Factory sont affichées dans la liste déroulante de hello.
   5. Sélectionnez **toodashboard du code confidentiel**.     
   6. Cliquez sur **Créer**.
      
      > [!IMPORTANT]
      > instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.
      > 
      > nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.                
      > 
      > 
3. Tableau de bord de hello, vous voyez hello suivant vignette avec l’état : **fabrique de données de déploiement**. 

    ![mosaïque déploiement de fabrique de données](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Après la création de hello est terminée, vous voyez hello **Data Factory** panneau comme indiqué dans l’image de hello.
   
   ![Page d'accueil Data Factory](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Créez des services liés
Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul. Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics. Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination). 

Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.  

Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
Dans cette étape, vous liez votre fabrique de données tooyour compte stockage Azure. Vous spécifiez le nom de hello et la clé de votre compte de stockage Azure dans cette section.  

1. Bonjour **Data Factory** panneau, cliquez sur **auteur et déployer** vignette.
   
   ![Vignette Créer et déployer](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Vous consultez hello **éditeur Data Factory** comme indiqué dans hello suivant image : 

    ![Data Factory Editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. Dans l’éditeur de hello, cliquez sur **nouveau magasin de données** bouton de barre d’outils hello et sélectionnez **le stockage Azure** à partir du menu déroulant de hello. Vous devez voir le modèle JSON hello pour la création d’un service lié Azure storage dans le volet de droite hello. 
   
    ![Éditeur - Bouton Nouveau magasin de données](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Remplacez `<accountname>` et `<accountkey>` avec hello compte nom et le compte de valeurs de clé pour votre compte de stockage Azure. 
   
    ![Éditeur - Stockage d’objets blob - JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Cliquez sur **déployer** sur la barre d’outils hello. Vous devez voir hello déployé **AzureStorageLinkedService** dans l’arborescence de hello afficher maintenant. 
   
    ![Éditeur - Stockage d'objets blob - Déploiement](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Pour plus d’informations sur les propriétés JSON dans la définition de service hello lié, consultez [connecteur de stockage d’objets Blob Azure](data-factory-azure-blob-connector.md#linked-service-properties) l’article.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Créer un service lié pour hello de base de données SQL Azure
Dans cette étape, vous liez votre fabrique de données de tooyour de base de données SQL Azure. Vous spécifiez le nom du serveur SQL Azure hello, nom de la base de données, nom d’utilisateur et mot de passe utilisateur dans cette section. 

1. Bonjour **éditeur Data Factory**, cliquez sur **nouveau magasin de données** bouton de barre d’outils hello et sélectionnez **base de données SQL Azure** à partir du menu déroulant de hello. Vous devez voir le modèle JSON hello pour la création du service lié SQL Azure de hello dans le volet de droite hello.
2. Remplacez les éléments `<servername>`, `<databasename>`, `<username>@<servername>` et `<password>` par le nom de votre serveur, de la base de données, du compte d’utilisateur SQL Azure et le mot de passe associé. 
3. Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **AzureSqlLinkedService**.
4. Vérifiez que vous voyez **AzureSqlLinkedService** dans l’arborescence hello sous **services liés**.  

    Pour plus d’informations sur ces propriétés JSON, consultez [Connecteur de base de données SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="create-datasets"></a>Créez les jeux de données
Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure. Dans cette étape, vous définissez deux jeux de données nommées InputDataset et OutputDataset qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.

service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello (InputDataset) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées. 

### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
Dans cette étape, vous créez un dataset nommé InputDataset qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService lié service. Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination. Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello. 

1. Bonjour **éditeur** pour hello fabrique de données, cliquez sur **... Plus**, cliquez sur **nouveau dataset**, puis cliquez sur **le stockage Blob Azure** à partir du menu déroulant de hello. 
   
    ![Menu Nouveau jeu de données](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Remplacez JSON dans le volet de droite hello hello suivant extrait de code JSON : 
   
    ```json
    {
      "name": "InputDataset",
      "properties": {
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
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```   

    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

    | Propriété | Description |
    |:--- |:--- |
    | type | propriété de type Hello est définie trop**AzureBlob** , car les données résident dans un stockage d’objets blob Azure. |
    | linkedServiceName | Fait référence toohello **AzureStorageLinkedService** que vous avez créé précédemment. |
    | folderPath | Spécifie l’objet blob de hello **conteneur** et hello **dossier** qui contient des objets BLOB d’entrée. Dans ce didacticiel, adftutorial est le conteneur d’objets blob hello et dossier est le dossier racine de hello. | 
    | fileName | Cette propriété est facultative. Si vous omettez cette propriété, tous les fichiers à partir de hello folderPath sont récupérées. Dans ce didacticiel, **emp.txt** n’est spécifié pour hello nom de fichier, ainsi que pour ce fichier est récupéré pour le traitement. |
    | format -> type |fichier d’entrée de Hello est au format de texte hello, nous utilisons **TextFormat**. |
    | columnDelimiter | colonnes Hello dans le fichier d’entrée de hello sont délimitées par **caractère virgule (`,`)**. |
    | frequency/interval | fréquence de Hello est défini trop**heure** et de l’intervalle est défini trop**1**, ce qui signifie que hello entrée tranches sont disponibles **toutes les heures**. En d’autres termes, hello service Data Factory recherche les données d’entrée toutes les heures dans le dossier racine de hello du conteneur d’objets blob (**adftutorial**) vous avez spécifié. Il recherche les données de salutation dans hello pipeline début et fin des heures, pas avant ou après ces moments précis.  |
    | external | Cette propriété a la valeur trop**true** si les données de salutation ne sont pas générées par ce pipeline. les données d’entrée de salutation dans ce didacticiel sont dans le fichier hello emp.txt, ce qui n’est pas généré par ce pipeline, et nous avons tootrue de cette propriété. |

    Pour plus d’informations sur ces propriétés JSON, voir [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).      
3. Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **InputDataset** jeu de données. Vérifiez que vous voyez hello **InputDataset** dans l’arborescence hello.

### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
Hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. Hello SQL table dataset de sortie (OututDataset) vous créez dans cette étape spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copiée.

1. Bonjour **éditeur** pour hello fabrique de données, cliquez sur **... Plus**, cliquez sur **nouveau dataset**, puis cliquez sur **SQL Azure** à partir du menu déroulant de hello. 
2. Remplacez JSON dans le volet de droite hello hello suivant extrait de code JSON :

    ```json   
    {
      "name": "OutputDataset",
      "properties": {
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
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
          "tableName": "emp"
        },
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```     

    Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

    | Propriété | Description |
    |:--- |:--- |
    | type | propriété de type Hello est définie trop**AzureSqlTable** , car les données sont table tooa copiées dans une base de données SQL Azure. |
    | linkedServiceName | Fait référence toohello **AzureSqlLinkedService** que vous avez créé précédemment. |
    | TableName | Hello spécifié **table** toowhich hello données sont copiées. | 
    | frequency/interval | Hello fréquence est définie trop**heure** et l’intervalle est **1**, ce qui signifie que les tranches de sortie hello sont produits **toutes les heures** entre le début du pipeline hello et les heures, pas avant de fin ou après ces moments précis.  |

    Il existe trois colonnes : **ID**, **FirstName**, et **LastName** : dans la table emp de hello dans la base de données hello. ID est une colonne d’identité, vous devez toospecify uniquement **FirstName** et **LastName** ici.

    Pour plus d’informations sur ces propriétés JSON, consultez l’article [Connecteur SQL Azure](data-factory-azure-sql-connector.md#dataset-properties).
3. Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **OutputDataset** jeu de données. Vérifiez que vous voyez hello **OutputDataset** dans l’arborescence hello sous **jeux de données**. 

## <a name="create-pipeline"></a>Création d’un pipeline
Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.

Actuellement, le dataset de sortie est les lecteurs hello planification. Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure. pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures. Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello. 

1. Bonjour **éditeur** pour hello fabrique de données, cliquez sur **... Plus**, puis sur **Nouveau pipeline**. Vous pouvez également cliquer sur **Pipelines** dans l’arborescence hello et cliquez sur **nouveau pipeline**.
2. Remplacez JSON dans le volet de droite hello hello suivant extrait de code JSON : 

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    Hello Notez les points suivants :
   
    - Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**. Pour plus d’informations sur l’activité de copie hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md). Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).
    - Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**. 
    - Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello. Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.
    - Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2016-10-14T16:32:41Z. Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel. Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**». pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.
     
    Hello précédent exemple, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.

    Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md). Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md). Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md). Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Connecteur de base de données SQL Azure](data-factory-azure-sql-connector.md).
3. Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **ADFTutorialPipeline**. Vérifiez que vous voyez pipeline hello dans arborescence hello. 
4. Maintenant, fermez hello **éditeur** panneau en cliquant sur **X**. Cliquez sur **X** nouveau toosee hello **Data Factory** page d’accueil de hello **ADFTutorialDataFactory**.

**Félicitations !** Vous venez de créer une fabrique de données Azure avec un pipeline toocopy des données d’une base de données SQL Azure de tooan stockage blob Azure. 


## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
Dans cette étape, vous utilisez hello Azure toomonitor portail, ce qui se passe dans une fabrique de données Azure.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Surveiller le pipeline à l’aide de l’application de surveillance et de gestion
Hello étapes suivantes vous montrent comment toomonitor pipelines dans votre fabrique de données à l’aide d’application d’analyse et de gestion hello : 

1. Cliquez sur **moniteur & gérer** vignette sur la page d’accueil hello pour votre fabrique de données.
   
    ![Vignette Surveiller et gérer](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. **L’application Surveiller et Gérer** doit apparaître dans un onglet distinct. 

    > [!NOTE]
    > Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », effectuez l’une des manières suivantes de hello : hello clair **bloquer les cookies tiers et les données de site** case à cocher (ou) créer une exception pour **login.microsoftonline.com**, puis essayez à nouveau tooopen hello application.

    ![Application de surveillance et gestion](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Hello de modification **l’heure de début** et **heure de fin** tooinclude (2017-05-11) de début et de fin (2017-05-12) de votre pipeline, puis cliquez sur **appliquer**.     
3. Vous consultez hello **windows de l’activité** associé à chaque heure entre le début du pipeline et de fin fois dans la liste hello dans le volet du milieu hello. 
4. toosee plus d’informations sur une fenêtre d’activité, sélectionnez hello fenêtre d’activité dans hello **Windows de l’activité** liste. 
    ![Détails de la fenêtre d’activité](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    Dans l’Explorateur de fenêtre d’activité sur hello droite, vous voyez que hello tranches de temps UTC en cours de toohello (8 12 h) sont traités (en vert). tranches de 8-9 PM, 9 et 10 PM, 10 et 11 PM, 23 h 00 - 12 h Hello ne sont pas encore traités.

    Hello **tentatives** section Bonjour droit volet fournit des informations sur l’activité hello exécutée pour la tranche de données hello. Si une erreur s’est produite, il fournit des détails sur l’erreur de hello. Par exemple, si hello d’entrée de dossier ou du conteneur ne pas existe et hello tranche le traitement échoue, vous voyez un message d’erreur indiquant que le conteneur de hello ou dossier n’existe pas.

    ![Tentatives d’exécution de l’activité](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Lancez **SQL Server Management Studio**connecter toohello base de données SQL Azure et vérifiez que les lignes de hello sont insérés dans toohello **emp** table hello de base de données.
    
    ![Résultats de la requête SQL](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Pour en savoir plus sur l’utilisation de cette application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).

### <a name="monitor-pipeline-using-diagram-view"></a>Surveillance d’un pipeline à l’aide de la Vue de diagramme
Vous pouvez également surveiller les pipelines de données à l’aide de vue de diagramme hello.  

1. Bonjour **Data Factory** panneau, cliquez sur **diagramme**.
   
    ![Panneau Fabrique de données - Vignette Diagramme](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. Vous devez voir toohello similaires du diagramme hello suivant image : 
   
    ![Vue schématique](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. Dans la vue de diagramme hello, double-cliquez sur **InputDataset** toosee des tranches pour hello le jeu de données.  
   
    ![Jeux de données avec InputDataset sélectionné](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Cliquez sur **plus** lien toosee toutes les tranches de données hello. Les 24 tranches horaires entre les heures de début et de fin du pipeline apparaissent. 
   
    ![Toutes les tranches de données d’entrée](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Notez que tous les hello tranches de données d’heure UTC actuelle de toohello sont **prêt** car hello **emp.txt** fichier existe tout temps hello dans le conteneur d’objets blob hello : **adftutorial\input**. tranches Hello de temps futures hello ne sont pas dans l’état ready encore. Vérifiez qu’aucune tranche n’apparaissent dans hello **récemment échec tranches** section bas hello.
6. Panneaux de fermer hello jusqu'à ce que vous consultez hello diagramme de vue (ou) défilement gauche toosee hello diagramme afficher. Ensuite, double-cliquez sur **OutputDataset**. 
8. Cliquez sur **plus** lien sur hello **Table** panneau pour **OutputDataset** toosee tous hello tranches.

    ![Panneau Tranches de données](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Notez que tous les hello tranches de temps UTC en cours de toohello déplacer à partir de **en attente d’exécution** état = > **en cours d’exécution** ==> **prêt** état. Hello hello dernières tranches (avant l’heure actuelle) sont traités à partir de la dernière toooldest par défaut. Par exemple, si hello heure actuelle est de 8 h 12 UTC, la tranche de hello pour 19 h 00 - 8 h est traitée avant la tranche de 6 h 00 - 19 h hello. tranche de 20 h 00 - 9 h Hello est traité à fin hello hello d’intervalle de temps par défaut, ce qui se trouve après 21 h 00.  
10. Cliquez sur n’importe quel tranche de données à partir de la liste de hello et vous devez voir hello **tranche de données** panneau. Une donnée associée à une fenêtre d’activité est appelée une tranche. Une tranche peut être constituée d’un ou de plusieurs fichiers.  
    
     ![Panneau Tranche de données](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Si la tranche de hello n’est pas hello **prêt** état, vous pouvez voir les tranches en amont hello qui ne sont pas prêtes et bloquent tranche à partir de l’exécution dans hello hello **tranches en amont qui ne sont pas prêtes** liste.
11. Bonjour **tranche de données** panneau, vous devez voir toutes les activités qui s’exécute dans la liste hello bas hello. Cliquez sur un **activité exécuter** toosee hello **détails de l’exécution activité** panneau. 
    
    ![Détails de l'exécution d'activité](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    Dans ce panneau, vous voyez comment l’opération de copie hello long est nécessaire, le débit, le nombre d’octets de données ont été en lecture et l’heure de début d’écriture, exécution, exécuter etc. l’heure de fin.  
12. Cliquez sur **X** tooclose tous les panneaux hello jusqu'à ce que vous récupérez panneau d’édition familiale toohello pour hello **ADFTutorialDataFactory**.
13. (facultatif) cliquez sur hello **Datasets** vignette ou **Pipelines** panneaux de hello tooget vignette que vous avez vu hello des étapes précédentes. 
14. Lancez **SQL Server Management Studio**connecter toohello base de données SQL Azure et vérifiez que les lignes de hello sont insérés dans toohello **emp** table hello de base de données.
    
    ![Résultats de la requête SQL](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez créé un Azure data factory toocopy de données à partir d’une base de données SQL Azure de tooan objets blob Azure. Vous avez utilisé la fabrique de données hello hello toocreate portail Azure, services liés, jeux de données et un pipeline. Voici les étapes principales hello que vous avez effectuées dans ce didacticiel :  

1. Création d’une **fabrique de données**Azure.
2. Création de **services liés**:
   1. Un **Azure Storage** lié service toolink votre compte de stockage Azure qui contient les données d’entrée.     
   2. Un **SQL Azure** lié service toolink votre base de données SQL Azure qui contient les données de sortie hello. 
3. Création de **jeux de données** qui décrivent les données d’entrée et de sortie des pipelines.
4. Création d’un **pipeline** avec une **activité de copie** avec **BlobSource** en tant que source et **SqlSink** en tant que récepteur.  

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie. Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello : 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.
