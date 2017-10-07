---
title: "Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de Visual Studio | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un pipeline Azure Data Factory avec une activité de copie à l’aide de Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Didacticiel : Créer un pipeline avec l'activité de copie à l'aide de Visual Studio
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

Dans cet article, vous découvrez comment toouse hello toocreate de Microsoft Visual Studio, une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure. Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.   

Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie. activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge. Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats). activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).

Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE] 
> le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Composants requis
1. Lisez [vue d’ensemble du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article et hello complète **condition préalable** étapes.       
2. instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.
3. Vous devez disposer de hello installé sur votre ordinateur : 
   * Visual Studio 2013 ou Visual Studio 2015
   * Téléchargez le Kit de développement logiciel (SDK) Azure pour Visual Studio 2013 ou Visual Studio 2015. Accédez trop[Page de téléchargement Azure](https://azure.microsoft.com/downloads/) et cliquez sur **VS 2013** ou **VS 2015** Bonjour **.NET** section.
   * Téléchargement du plug-in Azure Data Factory dernière hello pour Visual Studio : [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Vous pouvez également actualiser les plug-in hello en procédant comme hello comme suit : cliquez sur hello, **outils** -> **Extensions et mises à jour** -> **Online**  ->  **Galerie visual Studio** -> **Microsoft Azure Data Factory Tools pour Visual Studio** -> **mise à jour**.

## <a name="steps"></a>Étapes
Voici les étapes hello que vous effectuez dans le cadre de ce didacticiel :

1. Créer **services liés** dans la fabrique de données hello. Au cours de cette étape, vous allez créer deux services liés de types : Stockage Azure et base de données SQL Azure. 
    
    Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Création d’un conteneur et de téléchargé de compte de stockage de données toothis dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé une table SQL dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).     
2. Créer des entrées et sorties **jeux de données** dans la fabrique de données hello.  
    
    service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello Spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

    De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. De plus, hello sortie SQL table dataset spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copié.
3. Créer un **pipeline** dans la fabrique de données hello. Dans cette étape, vous allez créer un pipeline avec une activité de copie.   
    
    activité de copie Hello copie des données à partir d’un objet blob dans la table du tooa du stockage blob Azure hello dans la base de données SQL Azure hello. Vous pouvez utiliser une activité de copie dans un pipeline toocopy des données d’une destination de tooany pris en charge source prise en charge. Pour obtenir la liste des magasins de données pris en charge, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
4. Créez une **fabrique de données** Azure lors du déploiement des entités Data Factory (services liés, jeux de données/tables et pipelines). 

## <a name="create-visual-studio-project"></a>Création d’un projet Visual Studio
1. Lancez **Visual Studio 2015**. Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**. Vous devez voir hello **nouveau projet** boîte de dialogue.  
2. Bonjour **nouveau projet** boîte de dialogue, sélectionnez hello **DataFactory** modèle, puis cliquez sur **projet de la fabrique de données vide**.  
   
    ![Boîte de dialogue Nouveau projet](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Spécifiez le nom hello de projet de hello, l’emplacement de la solution de hello et le nom de la solution de hello, puis cliquez sur **OK**.
   
    ![Explorateur de solutions](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Créez des services liés
Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul. Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics. Vous allez utiliser deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination). 

Vous allez donc créer deux services liés de types : AzureStorage et AzureSqlDatabase.  

Hello le stockage Azure lié à des liens de service votre fabrique de données toohello compte stockage Azure. Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Liaisons de service de lié SQL Azure votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Services liés lier des magasins de données ou la fabrique de données Azure tooan de services de calcul. Consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour tous les hello sources et récepteurs pris en charge par l’activité de copie de hello. Consultez [services liés de calcul](data-factory-compute-linked-services.md) pour la liste des services de calcul pris en charge par la fabrique de données hello. Dans ce didacticiel, aucun service de calcul n’est utilisé. 

### <a name="create-hello-azure-storage-linked-service"></a>Créer le service lié Azure Storage de hello
1. Dans **l’Explorateur de solutions**, avec le bouton droit **Services liés**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.      
2. Bonjour **ajouter un nouvel élément** boîte de dialogue, sélectionnez **Service lié Azure Storage** à partir de la liste de hello, puis cliquez sur **ajouter**. 
   
    ![Nouveau service lié](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Remplacez `<accountname>` et `<accountkey>`* nom hello de votre compte de stockage Azure et sa clé. 
   
    ![Service lié Stockage Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Enregistrer hello **AzureStorageLinkedService1.json** fichier.

    Pour plus d’informations sur les propriétés JSON dans la définition de service hello lié, consultez [connecteur de stockage d’objets Blob Azure](data-factory-azure-blob-connector.md#linked-service-properties) l’article.

### <a name="create-hello-azure-sql-linked-service"></a>Créer le service lié SQL Azure de hello
1. Avec le bouton droit sur **Services liés** nœud Bonjour **l’Explorateur de solutions** à nouveau, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**. 
2. Cette fois, sélectionnez **Service lié SQL Azure**, puis cliquez sur **Ajouter**. 
3. Bonjour **AzureSqlLinkedService1.json fichier**, remplacez `<servername>`, `<databasename>`, `<username@servername>`, et `<password>` avec des noms de votre serveur SQL Azure, base de données, compte d’utilisateur et mot de passe.    
4. Enregistrer hello **AzureSqlLinkedService1.json** fichier. 
    
    Pour plus d’informations sur ces propriétés JSON, consultez [Connecteur de base de données SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).


## <a name="create-datasets"></a>Créez les jeux de données
Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure. Dans cette étape, vous définissez deux jeux de données nommées InputDataset et OutputDataset qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService1 et AzureSqlLinkedService1, respectivement.

service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello (InputDataset) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées. 

### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
Dans cette étape, vous créez un dataset nommé InputDataset qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService1 lié service. Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination. Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello. 

Ici, vous utilisez le terme hello « tables » plutôt que « jeux de données ». Une table est un jeu de données rectangulaire et hello seul type de jeu de données pris en charge actuellement. 

1. Avec le bouton droit **Tables** Bonjour **l’Explorateur de solutions**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.
2. Bonjour **ajouter un nouvel élément** boîte de dialogue, sélectionnez **objets Blob Azure**, puis cliquez sur **ajouter**.   
3. Remplacer un texte JSON hello hello suivant du texte et enregistrer hello **AzureBlobLocation1.json** fichier. 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
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

### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
Dans cette étape, vous créez un jeu de données de sortie nommé **OutputDataset**. Ce jeu de données pointe tooa SQL table dans la base de données SQL Azure hello représenté par **AzureSqlLinkedService1**. 

1. Avec le bouton droit **Tables** Bonjour **l’Explorateur de solutions** à nouveau, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.
2. Bonjour **ajouter un nouvel élément** boîte de dialogue, sélectionnez **SQL Azure**, puis cliquez sur **ajouter**. 
3. Remplacer un texte JSON hello hello suivant JSON et enregistrer hello **AzureSqlTableLocation1.json** fichier.

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
       "linkedServiceName": "AzureSqlLinkedService1",
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

## <a name="create-pipeline"></a>Création d’un pipeline
Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.

Actuellement, le dataset de sortie est les lecteurs hello planification. Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure. pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures. Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello. 

1. Avec le bouton droit **Pipelines** Bonjour **l’Explorateur de solutions**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.  
2. Sélectionnez **Pipeline de données de copie** Bonjour **ajouter un nouvel élément** boîte de dialogue et cliquez sur **ajouter**. 
3. Remplacez hello JSON hello suivant JSON et enregistrer hello **CopyActivity1.json** fichier.

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**. Pour plus d’informations sur l’activité de copie hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md). Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).
    - Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**. 
    - Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello. Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.  
     
    Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant. Vous pouvez spécifier qu’une partie date hello et ignorer la partie heure hello hello date heure. Par exemple, « 2016-02-03 », qui est l’équivalent trop « 2016-02-03T00:00:00Z »
     
    Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2016-10-14T16:32:41Z. Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel. 
     
    Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**». pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.
     
    Hello précédent exemple, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.

    Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md). Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md). Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md). Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Azure SQL Database connector](data-factory-azure-sql-connector.md) (Connecteur de base de données SQL Azure).

## <a name="publishdeploy-data-factory-entities"></a>Publier/déployer des entités Data Factory
Dans cette étape, vous publiez les entités Data Factory (services liés, jeux de données et pipeline) que vous avez créées précédemment. Vous spécifiez également le nom hello de hello nouvelles données fabrique toobe créé toohold ces entités.  

1. Cliquez sur le projet dans l’Explorateur de solutions de hello, puis cliquez sur **publier**. 
2. Si vous voyez **connecter tooyour compte Microsoft** boîte de dialogue, entrez vos informations d’identification de compte hello qui dispose d’abonnement Azure, puis cliquez sur **connectez-vous**.
3. Vous devez voir hello suivant la boîte de dialogue :
   
   ![Boîte de dialogue Publier](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. Dans la page de fabrique configurer données hello, procédez comme hello comme suit : 
   
   1. Sélectionnez l’option **Créer une fabrique de données** .
   2. Saisissez **VSTutorialFactory** dans le champ **Nom**.  
      
      > [!IMPORTANT]
      > nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez une erreur sur le nom hello de fabrique de données lors de la publication, modifiez le nom hello de fabrique de données hello (par exemple, yournameVSTutorialFactory) et essayez de publier à nouveau. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.        
      > 
      > 
   3. Sélectionnez votre abonnement Azure pour hello **abonnement** champ.
      
      > [!IMPORTANT]
      > Si vous ne voyez pas d’un abonnement, assurez-vous que vous connecté en utilisant un compte qui est administrateur ou coadministrateur de l’abonnement de hello.  
      > 
      > 
   4. Sélectionnez hello **groupe de ressources** pour toobe de fabrique de données hello créé. 
   5. Sélectionnez hello **région** de fabrique de données hello. Seules les régions pris en charge par hello service Data Factory sont affichées dans la liste déroulante de hello.
   6. Cliquez sur **suivant** tooswitch toohello **publier des éléments** page.
      
       ![Page Configurer une fabrique de données](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. Bonjour **publier des éléments** , vérifiez que tous les hello fabriques de données entités sont sélectionnées, puis cliquez sur **suivant** tooswitch toohello **Résumé** page.
   
   ![Page Publier des éléments](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Passez en revue la synthèse de hello et cliquez sur **suivant** toostart Bonjour déploiement processus et vue Bonjour **état du déploiement**.
   
   ![Page Résumé de la publication](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. Bonjour **état du déploiement** page, vous devez voir État hello hello du processus de déploiement. Après le déploiement de hello, cliquez sur Terminer.
 
   ![Page État du déploiement](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Hello Notez les points suivants : 

* Si vous recevez une erreur de hello : « cet abonnement n’est pas inscrit toouse, espace de noms Microsoft.DataFactory », effectuez l’une des manières suivantes les hello et essayez de publier à nouveau : 
  
  * Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello Data Factory. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Connexion à l’aide de hello abonnement Azure dans hello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure. Cette action enregistre automatiquement le fournisseur hello pour vous.
* nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.

> [!IMPORTANT]
> instances de fabrique de données toocreate, vous devez toobe une administration/co-admin Hello abonnement Azure

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
Accédez toohello page d’accueil de votre fabrique de données :

1. Connectez-vous trop[portail Azure](https://portal.azure.com).
2. Cliquez sur **davantage de services** sur hello du menu de gauche, puis cliquez sur **fabriques de données**.

    ![Parcourir les fabriques de données](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Commencez à taper le nom hello votre fabrique de données.

    ![Nom de la fabrique de données](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Cliquez sur votre data factory dans hello résultats liste toosee hello page d’accueil de votre fabrique de données.

    ![Page d'accueil Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Suivez les instructions à partir de [analyser des jeux de données et le pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline de hello toomonitor et jeux de données que vous avez créé dans ce didacticiel. Pour le moment, Visual Studio ne prend pas en charge la surveillance des pipelines Data Factory. 

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez créé un Azure data factory toocopy de données à partir d’une base de données SQL Azure de tooan objets blob Azure. Vous avez utilisé Visual Studio toocreate hello fabrique de données, les services liés, des groupes de données et un pipeline. Voici les étapes principales hello que vous avez effectuées dans ce didacticiel :  

1. Création d’une **fabrique de données**Azure.
2. Création de **services liés**:
   1. Un **Azure Storage** lié service toolink votre compte de stockage Azure qui contient les données d’entrée.     
   2. Un **SQL Azure** lié service toolink votre base de données SQL Azure qui contient les données de sortie hello. 
3. Création des **jeux de données**qui décrivent les données d’entrée et de sortie des pipelines.
4. Création d’un **pipeline** avec une **activité de copie** avec **BlobSource** en tant que source et **SqlSink** en tant que récepteur. 

toosee toouse une activité de la ruche HDInsight tootransform des données avec cluster Azure HDInsight, voir [ didacticiel : créer vos premières données tootransform de pipeline à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).

Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, voir [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md). 

## <a name="view-all-data-factories-in-server-explorer"></a>Afficher toutes les fabriques de données dans l’Explorateur de serveurs
Cette section décrit comment toouse hello de l’Explorateur de serveurs dans Visual Studio tooview toutes les fabriques de données hello dans votre abonnement Azure et comment créer un projet Visual Studio basé sur une fabrique de données. 

1. Dans **Visual Studio**, cliquez sur **vue** hello menu et cliquez sur **l’Explorateur de serveurs**.
2. Dans la fenêtre de l’Explorateur de serveurs hello, développez **Azure** et développez **Data Factory**. Si vous voyez **connecter tooVisual Studio**, entrez hello **compte** associé à votre abonnement Azure et d’un clic **continuer**. Saisissez le **mot de passe**, puis cliquez sur **Se connecter**. Visual Studio essaie de tooget d’informations sur toutes les fabriques de données Azure dans votre abonnement. Vous voyez l’état hello de cette opération Bonjour **liste des tâches données fabrique** fenêtre.

    ![Explorateur de serveurs](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Créer un projet Visual Studio pour une fabrique de données existante

- Avec le bouton droit une fabrique de données dans l’Explorateur de serveurs, puis sélectionnez **tooNew d’exporter la fabrique de données projet** toocreate un projet Visual Studio basé sur une fabrique de données.

    ![Projet VS tooa exportation data factory](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

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


## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie. Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello : 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.
