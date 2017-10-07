---
title: "Didacticiel : Créer un toomove de données de pipeline à l’aide d’Azure PowerShell | Documents Microsoft"
description: "Dans ce didacticiel, vous créez un pipeline Azure Data Factory avec une activité de copie à l’aide d’Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Didacticiel : Créer un pipeline Data Factory qui déplace les données à l’aide d’Azure PowerShell
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

Dans cet article, vous apprendrez comment toouse PowerShell toocreate une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure. Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.   

Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie. activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge. Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats). activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).

Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Cet article ne couvre pas toutes les applets de commande hello Data Factory. Consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories) pour obtenir une documentation complète sur ces applets de commande.
> 
> le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Composants requis
- Terminer la configuration requise indiquée dans hello [conditions préalables didacticiels](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) l’article.
- Installez **Azure PowerShell**. Suivez les instructions de hello dans [comment tooinstall et configurer Azure PowerShell](../powershell-install-configure.md).

## <a name="steps"></a>Étapes
Voici les étapes hello que vous effectuez dans le cadre de ce didacticiel :

1. Créez une **fabrique de données** Azure. Dans cette étape, vous créez une fabrique de données nommée ADFTutorialDataFactoryPSH. 
2. Créer **services liés** dans la fabrique de données hello. Au cours de cette étape, vous allez créer deux services liés de types : Stockage Azure et base de données SQL Azure. 
    
    Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Création d’un conteneur et de téléchargé de compte de stockage de données toothis dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé une table SQL dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   
3. Créer des entrées et sorties **jeux de données** dans la fabrique de données hello.  
    
    service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello Spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

    De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. De plus, hello sortie SQL table dataset spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copié.
4. Créer un **pipeline** dans la fabrique de données hello. Dans cette étape, vous allez créer un pipeline avec une activité de copie.   
    
    activité de copie Hello copie des données à partir d’un objet blob dans la table du tooa du stockage blob Azure hello dans la base de données SQL Azure hello. Vous pouvez utiliser une activité de copie dans un pipeline toocopy des données d’une destination de tooany pris en charge source prise en charge. Pour obtenir la liste des magasins de données pris en charge, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Pipeline de hello moniteur. Dans cette étape, vous **moniteur** hello tranches de jeux de données d’entrée et de sortie à l’aide de PowerShell.

## <a name="create-a-data-factory"></a>Créer une fabrique de données
> [!IMPORTANT]
> Complète [conditions préalables requises pour le didacticiel de hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si vous n’avez pas déjà fait.   

Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive données tooproduct sortie les données d’entrée. Commençons par créer la fabrique de données hello dans cette étape.

1. Lancez **PowerShell**. Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel. Si vous fermez et rouvrez, vous devez à nouveau les commandes de hello toorun.

    Exécutez hello commande suivante, puis entrez les nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure :

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte :

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Tooselect hello abonnement toowork avec la commande suivante d’exécution hello. Remplacez  **&lt;NameOfAzureSubscription** &gt; avec le nom de hello de votre abonnement Azure :

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello de commande suivante :

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Certaines des étapes hello dans ce didacticiel supposent que vous utilisez le groupe de ressources hello nommé **ADFTutorialResourceGroup**. Si vous utilisez un autre groupe de ressources, vous devez toouse il à la place de ADFTutorialResourceGroup dans ce didacticiel.
3. Exécutez hello **New-AzureRmDataFactory** toocreate de l’applet de commande une fabrique de données nommée **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Ce nom peut avoir déjà été utilisé. Par conséquent, vous nom hello hello fabrique de données unique en ajoutant un préfixe ou un suffixe (par exemple : ADFTutorialDataFactoryPSH05152017) et réexécutez la commande hello.  

Hello Notez les points suivants :

* nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez hello l’erreur suivante, renommez hello (par exemple, yournameADFTutorialDataFactoryPSH). Utilisez ce nom à la place d’ADFTutorialFactoryPSH quand vous effectuez les étapes de ce didacticiel. Consultez la rubrique [Data Factory – Règles d’affectation des noms](data-factory-naming-rules.md) pour les artefacts Data Factory.

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* instances de fabrique de données toocreate, vous devez être un administrateur de hello abonnement Azure ou un collaborateur.
* nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.
* Hello, l’erreur suivante peut s’afficher : «**cet abonnement n’est pas un espace de noms toouse inscrits Microsoft.DataFactory.**» Effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :

  * Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello fabrique de données :

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Ce fournisseur est inscrit de fabrique de données hello, exécutez hello suivant tooconfirm de commande :

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Connectez-vous à l’aide de hello abonnement Azure toohello [portail Azure](https://portal.azure.com). Atteindre le panneau de fabrique de données tooa ou créez une fabrique de données Bonjour portail Azure. Cette action enregistre automatiquement le fournisseur hello pour vous.

## <a name="create-linked-services"></a>Créez des services liés
Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul. Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics. Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination). 

Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.  

Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Créer un service lié pour un compte de stockage Azure
Dans cette étape, vous liez votre fabrique de données tooyour compte stockage Azure.

1. Créez un fichier JSON nommé **AzureStorageLinkedService.json** dans **C:\ADFGetStartedPSH** dossier avec hello suivant contenu : (dossier hello créer ADFGetStartedPSH si elle n’existe pas déjà).

    > [!IMPORTANT]
    > Remplacez &lt;accountname&gt; et &lt;accountkey&gt; avec le nom et la clé de votre compte de stockage Azure avant d’enregistrer le fichier de hello. 

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
2. Dans **Azure PowerShell**, commutateur toohello **ADFGetStartedPSH** dossier.
4. Exécutez hello **New-AzureRmDataFactoryLinkedService** hello de toocreate d’applet de commande de service lié : **AzureStorageLinkedService**. Cette applet de commande et d’autres applets de commande fabrique de données que vous utilisez dans ce didacticiel requiert vous toopass des valeurs pour hello **ResourceGroupName** et **DataFactoryName** paramètres. Vous pouvez également, vous pouvez passer l’objet DataFactory hello retourné par l’applet de commande New-AzureRmDataFactory hello sans avoir à taper ResourceGroupName et DataFactoryName chaque fois que vous exécutez une applet de commande. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Voici le résultat de l’exemple hello :

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Autre méthode de création de ce service lié est toospecify nom de groupe de ressources et le nom de fabrique de données au lieu de spécifier l’objet DataFactory hello.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Créer un service lié pour une base de données Azure SQL
Dans cette étape, vous liez votre fabrique de données de tooyour de base de données SQL Azure.

1. Créer un fichier JSON comportant AzureSqlLinkedService.json dans le dossier de C:\ADFGetStartedPSH hello suivant contenu :

    > [!IMPORTANT]
    > Remplacez &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, et &lt;password&gt; par les noms de votre serveur SQL Azure, de la base de données, du compte d’utilisateur et par le mot de passe.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Exécutez hello suivant commande toocreate un service lié :

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Voici le résultat de l’exemple hello :

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Vérifiez que **autoriser l’accès des services de tooAzure** paramètre est activé pour votre serveur de base de données SQL. tooverify et mettez-le sous tension, hello comme suit :

    1. Connectez-vous à toohello [portail Azure](https://portal.azure.com)
    2. Cliquez sur **davantage de services >** sur hello gauche, puis cliquez sur **serveurs SQL** Bonjour **bases de données** catégorie.
    3. Sélectionnez votre serveur dans la liste hello de serveurs SQL Server.
    4. Dans le panneau hello SQL server, cliquez sur **afficher les paramètres de pare-feu** lien.
    5. Bonjour **des paramètres de pare-feu** panneau, cliquez sur **ON** pour **autoriser l’accès des services de tooAzure**.
    6. Cliquez sur **enregistrer** sur la barre d’outils hello. 

## <a name="create-datasets"></a>Créez les jeux de données
Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure. Dans cette étape, vous définissez deux jeux de données nommées InputDataset et OutputDataset qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.

service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello (InputDataset) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées. 

### <a name="create-an-input-dataset"></a>Créer un jeu de données d’entrée
Dans cette étape, vous créez un dataset nommé InputDataset qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService lié service. Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination. Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello.  

1. Créez un fichier JSON nommé **InputDataset.json** Bonjour **C:\ADFGetStartedPSH** dossier, avec hello suivant le contenu :

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
                "fileName": "emp.txt",
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
2. Exécutez hello suivant commande toocreate hello Data Factory dataset.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Voici le résultat de l’exemple hello :

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Créer un jeu de données de sortie
Dans cette partie de l’étape de hello, vous créez un dataset de sortie nommé **OutputDataset**. Ce jeu de données pointe tooa SQL table dans la base de données SQL Azure hello représenté par **AzureSqlLinkedService**. 

1. Créez un fichier JSON nommé **OutputDataset.json** Bonjour **C:\ADFGetStartedPSH** dossier avec hello suivant le contenu :

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
2. Exécutez hello suivant le jeu de données de la fabrique de données de commande toocreate hello.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Voici le résultat de l’exemple hello :

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>Créer un pipeline
Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.

Actuellement, le dataset de sortie est les lecteurs hello planification. Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure. pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures. Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello. 


1. Créez un fichier JSON nommé **ADFTutorialPipeline.json** Bonjour **C:\ADFGetStartedPSH** dossier, avec hello suivant le contenu :

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
     
    Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant. Vous pouvez spécifier qu’une partie date hello et ignorer la partie heure hello hello date heure. Par exemple, « 2016-02-03 », qui est l’équivalent trop « 2016-02-03T00:00:00Z »
     
    Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2016-10-14T16:32:41Z. Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel. 
     
    Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**». pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.
     
    Hello précédent exemple, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.

    Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md). Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md). Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md). Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Connecteur de base de données SQL Azure](data-factory-azure-sql-connector.md).
2. Exécutez hello commande toocreate hello données fabrique tableau suivant.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Voici le résultat de l’exemple hello : 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Félicitations !** Vous venez de créer une fabrique de données Azure avec un pipeline toocopy des données d’une base de données SQL Azure de tooan stockage blob Azure. 

## <a name="monitor-hello-pipeline"></a>Pipeline d’analyse hello
Dans cette étape, vous utilisez Azure PowerShell toomonitor ce qui se passe dans une fabrique de données Azure.

1. Remplacez &lt;DataFactoryName&gt; avec nom hello de la fabrique de données et votre **Get-AzureRmDataFactory**et assigner hello sortie tooa $df variable.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Par exemple :
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Ensuite, exécutez le contenu d’impression hello Hello de toosee $df après la sortie : 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Exécutez **Get-AzureRmDataFactorySlice** tooget plus d’informations sur toutes les tranches de hello **OutputDataset**, qui est le jeu de données hello sortie du pipeline de hello.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   Ce paramètre doit correspondre à hello **Démarrer** valeur dans le code JSON de pipeline hello. Vous devez voir 24 secteurs, un pour chaque heure de 12 : 00 de hello jour too12 suis Hello jour suivant.

   Voici trois tranches d’exemple à partir de la sortie de hello : 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Exécutez **Get-AzureRmDataFactoryRun** tooget les détails de hello de l’activité s’exécute pour un **spécifique** tranche. Copier la valeur de date-heure hello à partir de la sortie hello de hello commande toospecify hello valeur précédente pour le paramètre de %StartDateTime;) hello. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Voici le résultat de l’exemple hello : 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Pour obtenir une documentation complète sur les applets de commande Data Factory, consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories).

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez créé un Azure data factory toocopy de données à partir d’une base de données SQL Azure de tooan objets blob Azure. Vous avez utilisé la fabrique de données PowerShell toocreate hello, services liés, jeux de données et un pipeline. Voici les étapes principales hello que vous avez effectuées dans ce didacticiel :  

1. Création d’une **fabrique de données**Azure.
2. Création de **services liés**:

   a. Un **Azure Storage** lié service toolink votre compte de stockage Azure qui contient les données d’entrée.     
   b. Un **SQL Azure** lié service toolink votre base de données SQL qui contient les données de sortie hello.
3. Création de **jeux de données** qui décrivent les données d’entrée et de sortie des pipelines.
4. Créé un **pipeline** avec **l’activité de copie**, avec **BlobSource** en tant que source de hello et **SqlSink** comme récepteur de hello.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie. Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello : 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello. 

