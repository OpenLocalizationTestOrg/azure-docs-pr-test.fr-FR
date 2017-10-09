---
title: "Didacticiel : Utilisation REST API toocreate un pipeline Azure Data Factory | Documents Microsoft"
description: "Dans ce didacticiel, vous utilisez des API REST toocreate un pipeline Azure Data Factory comportant des données toocopy d’activité de copie à partir d’un stockage d’objets blob Azure une base de données SQL Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Didacticiel : Utilisation REST API toocreate un Azure Data Factory pipeline toocopy de données 
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

Dans cet article, vous découvrez comment toouse REST API toocreate une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure. Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.   

Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie. activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge. Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats). activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).

Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Cet article ne couvre pas hello toutes les API REST de fabrique de données. Consultez les [informations de référence sur l’API REST Data Factory](/rest/api/datafactory/) pour obtenir une documentation complète sur les applets de commande Data Factory.
>  
> le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Composants requis
* Passez en revue [vue d’ensemble du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) et hello complète **condition préalable** étapes.
* Installez [Curl](https://curl.haxx.se/dlwiz/) sur votre ordinateur. Vous utilisez l’outil de Curl de hello avec d’autres commandes toocreate une fabrique de données. 
* Suivez les instructions de [cet article](../azure-resource-manager/resource-group-create-service-principal-portal.md) pour effectuer les opérations suivantes : 
  1. Créez une application Web nommée **ADFCopyTutotiralApp** dans Azure Active Directory.
  2. Obtenez un **ID client** et une **clé secrète**. 
  3. Obtenez l’ **ID de locataire**. 
  4. Affecter hello **ADFCopyTutorialApp** application toohello **collaborateur de fabrique de données** rôle.  
* Installez [Azure PowerShell](/powershell/azure/overview).  
* Lancez **PowerShell** et hello comme suit. Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel. Si vous fermez et rouvrez, vous devez à nouveau les commandes de hello toorun.
  
  1. Exécutez hello commande suivante, puis entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure :
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte :

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Tooselect hello abonnement toowork avec la commande suivante d’exécution hello. Remplacez  **&lt;NameOfAzureSubscription** &gt; avec le nom de hello de votre abonnement Azure. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello commande Bonjour PowerShell suivante :  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Si groupe de ressources hello existe déjà, vous spécifiez si tooupdate il (Y) ou conserver en tant que (N). 
     
      Certaines des étapes hello dans ce didacticiel supposent que vous utilisez le groupe de ressources hello nommé ADFTutorialResourceGroup. Si vous utilisez un autre groupe de ressources, vous devez le nom de hello toouse de votre groupe de ressources à la place de ADFTutorialResourceGroup dans ce didacticiel.

## <a name="create-json-definitions"></a>Créer des définitions JSON
Créer des fichiers JSON dans le dossier hello où se trouve curl.exe suivants. 

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nom doit être globalement unique, vous pouvez donc tooprefix/suffixe ADFCopyTutorialDF toomake il un nom unique. 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Remplacez **accountname** et **accountkey** par le nom et la clé de votre compte de stockage Azure. toolearn comment tooget votre stockage accéder aux clés, voir [clés d’accès afficher, copier et régénérer stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

```JSON
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

Pour plus d’informations sur les propriétés JSON, consultez [Service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Remplacez **nom_serveur**, **databasename**, **nom d’utilisateur**, et **mot de passe** avec le nom de votre serveur SQL Azure, le nom de base de données SQL, utilisateur compte et mot de passe pour le compte de hello.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Pour plus d’informations sur les propriétés JSON, consultez [Service lié SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
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

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
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

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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
- Entrée d’activité hello est définie trop**AzureBlobInput** et de sortie d’activité hello est définie trop**AzureSqlOutput**. 
- Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello. Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.  
 
Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant. Vous pouvez spécifier qu’une partie date hello et ignorer la partie heure hello hello date heure. Par exemple, « 2017-02-03 », qui est l’équivalent trop « 2017-02-03T00:00:00Z »
 
Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2016-10-14T16:32:41Z. Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel. 
 
Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**». pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.
 
Hello précédent exemple, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.

Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md). Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md). Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md). Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Azure SQL Database connector](data-factory-azure-sql-connector.md) (Connecteur de base de données SQL Azure).

## <a name="set-global-variables"></a>Définir des variables globales
Dans Azure PowerShell, exécutez hello suivant les commandes après le remplacement des valeurs de hello par les vôtres :

> [!IMPORTANT]
> Consultez la section [Configuration requise](#prerequisites) pour savoir comment obtenir un ID client, une clé secrète client, un ID de locataire et un ID d’abonnement.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Exécutez hello commande suivante après la mise à jour nom hello hello fabrique de données que vous utilisez : 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Authentifier avec AAD
Exécutez hello suivant commande tooauthenticate avec Azure Active Directory (AAD) : 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Créer une fabrique de données
Dans cette étape, vous créez une fabrique de données Azure nommée **ADFCopyTutorialDF**. Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, magasin de données toocopy l’activité de copie à partir de la source de données de destination tooa. Un toorun d’activité HDInsight Hive un tootransform de script Hive les données de sortie de tooproduct de données d’entrée. Exécutez hello suivant la fabrique de données de commandes toocreate hello : 

1. Affecter hello toovariable de commande nommé **cmd**. 
   
    > [!IMPORTANT]
    > Confirmer ce nom hello hello fabrique de données vous spécifiez ici les correspondances (ADFCopyTutorialDF) hello nom spécifié dans hello **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si la fabrique de données hello a été créé avec succès, vous voyez hello JSON de fabrique de données hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.  
   
    ```
    Write-Host $results
    ```

Hello Notez les points suivants :

* nom de Hello Hello Azure Data Factory doit être globalement unique. Si vous voyez l’erreur hello dans les résultats : **nom de fabrique de données « ADFCopyTutorialDF » n’est pas disponible**, hello comme suit :  
  
  1. Modifier le nom hello (par exemple, yournameADFCopyTutorialDF) Bonjour **datafactory.json** fichier.
  2. Dans la première commande de hello où hello **$cmd** une valeur est assignée à la variable, remplacez ADFCopyTutorialDF avec le nouveau nom de hello et exécutez la commande hello. 
  3. Résultats de la série hello deux commandes tooinvoke hello API REST toocreate hello données fabrique et impression hello d’opération de hello. 
     
     Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.
* instances de fabrique de données toocreate, vous devez toobe un collaborateur/administrateur Hello abonnement Azure
* nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.
* Si vous recevez une erreur de hello : «**cet abonnement n’est pas un espace de noms inscrit toouse Microsoft.DataFactory**», effectuez l’une des manières suivantes les hello et essayez de publier à nouveau : 
  
  * Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello fabrique de données : 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Connexion à l’aide de hello abonnement Azure dans hello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure. Cette action enregistre automatiquement le fournisseur hello pour vous.

Avant de créer un pipeline, vous devez toocreate quelques entités de fabrique de données tout d’abord. Vous créez tout d’abord la source de toolink services liés et les données de destination stocke les données tooyour stocker. Ensuite, définissez les jeux de données d’entrée et de sortie toorepresent données de magasins de données lié. Enfin, créez le pipeline de hello avec une activité qui utilise ces jeux de données.

## <a name="create-linked-services"></a>Créez des services liés
Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul. Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics. Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination). Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.  

Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
Dans cette étape, vous liez votre fabrique de données tooyour compte stockage Azure. Vous spécifiez le nom de hello et la clé de votre compte de stockage Azure dans cette section. Consultez [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur JSON propriétés utilisées toodefine un stockage Azure le service lié.  

1. Affecter hello toovariable de commande nommé **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si hello lié service a été créé avec succès, vous voyez hello JSON pour le service lié de hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Créer un service lié Azure SQL
Dans cette étape, vous liez votre fabrique de données de tooyour de base de données SQL Azure. Vous spécifiez le nom du serveur SQL Azure hello, nom de la base de données, nom d’utilisateur et mot de passe utilisateur dans cette section. Consultez [service lié Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) pour plus d’informations sur JSON propriétés utilisées toodefine service lié de SQL Azure.

1. Affecter hello toovariable de commande nommé **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si hello lié service a été créé avec succès, vous voyez hello JSON pour le service lié de hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Créez les jeux de données
Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure. Dans cette étape, vous définissez deux jeux de données nommées AzureBlobInput et AzureSqlOutput qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.

service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello (AzureBlobInput) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées. 

### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
Dans cette étape, vous créez un dataset nommé AzureBlobInput qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService lié service. Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination. Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello. 

1. Affecter hello toovariable de commande nommé **cmd**. 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
Hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. Hello SQL table dataset de sortie (OututDataset) vous créez dans cette étape spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copiée.

1. Affecter hello toovariable de commande nommé **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a>Création d’un pipeline
Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **AzureBlobInput** en entrée et **AzureSqlOutput** en sortie.

Actuellement, le dataset de sortie est les lecteurs hello planification. Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure. pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures. Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello. 

1. Affecter hello toovariable de commande nommé **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.  

    ```PowerShell   
    Write-Host $results
    ```

**Félicitations !** Vous venez de créer une fabrique de données Azure, avec un pipeline qui copie les données à partir de la base de données SQL Azure Blob Storage tooAzure.

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
Dans cette étape, vous utilisez tranches de toomonitor API REST de fabrique données produits par le pipeline de hello.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Assurez-vous que Démarrer de hello et heures spécifiées dans hello suivant de fin commande correspondance hello début et fin du pipeline de hello. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Exécutez hello Invoke-Command et hello suivant jusqu'à ce que vous voyiez un secteur dans **prêt** état ou **n’a pas pu** état. Lors de la tranche de hello est prêt, vérifiez hello **emp** table dans votre base de données SQL Azure pour les données de sortie hello. 

Pour chaque secteur, deux lignes de données à partir du fichier de source de hello sont table emp de toohello copiés dans la base de données SQL Azure hello. Par conséquent, vous voyez 24 nouveaux enregistrements dans la table emp de hello lorsque toutes les tranches de hello sont traitées avec succès (dans l’état prêt). 

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez utilisé les API REST toocreate un Azure fabrique toocopy de données à partir d’une base de données SQL Azure de tooan objets blob Azure. Voici les étapes principales hello que vous avez effectuées dans ce didacticiel :  

1. Création d’une **fabrique de données**Azure.
2. Création de **services liés**:
   1. Un stockage Azure lié à service toolink votre compte de stockage Azure qui contient les données d’entrée.     
   2. SQL Azure lié à service toolink votre base de données SQL Azure qui contient les données de sortie hello. 
3. Création des **jeux de données**qui décrivent les données d’entrée et de sortie des pipelines.
4. Création d’un **pipeline** avec une activité de copie avec BlobSource en tant que source et SqlSink en tant que récepteur. 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie. Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello : 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.
