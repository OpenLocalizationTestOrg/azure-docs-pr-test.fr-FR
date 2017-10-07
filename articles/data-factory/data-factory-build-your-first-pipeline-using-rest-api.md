---
title: "aaaBuild votre première data factory (REST) | Documents Microsoft"
description: "Dans ce didacticiel, vous allez créer un exemple de pipeline Azure Data Factory à l’aide de l’API REST Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Didacticiel : Créer votre première fabrique de données Azure en utilisant l’API REST Data Factory
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-build-your-first-pipeline.md)
> * [Portail Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modèle Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


Dans cet article, vous utilisez API REST de fabrique données toocreate votre première Azure data factory. didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello.

pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**. Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce. pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin.

> [!NOTE]
> Cet article ne couvre pas hello toutes les API REST. pour obtenir une documentation complète sur les API REST, consultez [Informations de référence sur l’API REST Data Factory](/rest/api/datafactory/).
> 
> Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a>Composants requis
* Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.
* Installez [Curl](https://curl.haxx.se/dlwiz/) sur votre ordinateur. Vous utilisez l’outil CURL de hello avec d’autres commandes toocreate une fabrique de données.
* Suivez les instructions de [cet article](../azure-resource-manager/resource-group-create-service-principal-portal.md) pour effectuer les opérations suivantes :
  1. Créez une application Web nommée **ADFGetStartedApp** dans Azure Active Directory.
  2. Obtenez un **ID client** et une **clé secrète**.
  3. Obtenez l’ **ID de locataire**.
  4. Affecter hello **ADFGetStartedApp** application toohello **collaborateur de fabrique de données** rôle.
* Installez [Azure PowerShell](/powershell/azure/overview).
* Lancez **PowerShell** et hello exécution de commande suivante. Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel. Si vous fermez et rouvrez, vous devez à nouveau les commandes de hello toorun.
  1. Exécutez **AzureRmAccount de connexion** et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.
  2. Exécutez **Get-AzureRmSubscription** tooview tous hello abonnements pour ce compte.
  3. Exécutez **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello abonnement toowork avec. Remplacez **NameOfAzureSubscription** avec le nom de hello de votre abonnement Azure.
* Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello commande Bonjour PowerShell suivante :

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

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
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Remplacez **accountname** et **accountkey** par le nom et la clé de votre compte de stockage Azure. toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

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

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

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
| ClusterSize |Taille du cluster HDInsight de hello. |
| TimeToLive |Spécifie la durée d’inactivité de ce hello pour le cluster HDInsight de hello, avant d’être supprimé. |
| linkedServiceName |Spécifie le compte de stockage hello toostore utilisé hello journaux générés par HDInsight |

Hello Notez les points suivants :

* Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello au-dessus de JSON. Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
* Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois une tranche est traitée, sauf s’il existe un cluster dynamique existant (**timeToLive**) et est supprimé quand le traitement de hello est effectué.

    Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ». Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.

Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

### <a name="inputdatasetjson"></a>inputdataset.json

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

Hello JSON définit un dataset nommé **AzureBlobInput**, qui représente les données d’entrée pour une activité dans le pipeline de hello. En outre, il spécifie que les données d’entrée hello se trouve dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **inputdata**.

Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :

| Propriété | Description |
|:--- |:--- |
| type |propriété de type Hello a la valeur tooAzureBlob, car les données résident dans le stockage blob Azure. |
| linkedServiceName |fait référence toohello StorageLinkedService que vous avez créé précédemment. |
| fileName |Cette propriété est facultative. Si vous omettez cette propriété, tous les fichiers hello hello folderPath sont récupérées. Dans ce cas, uniquement les input.log hello est traitée. |
| type |les fichiers journaux Hello étant au format texte, nous utilisons TextFormat. |
| columnDelimiter |colonnes dans les fichiers journaux de hello sont délimitées par une virgule () |
| frequency/interval |fréquence égale tooMonth et l’intervalle est 1, ce qui signifie que les tranches d’entrée hello sont disponibles chaque mois. |
| external |Cette propriété a la valeur tootrue si les données d’entrée hello ne sont pas générées par le service de fabrique de données hello. |

### <a name="outputdatasetjson"></a>outputdataset.json

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

Hello JSON définit un dataset nommé **AzureBlobOutput**, qui représente les données de sortie d’une activité dans le pipeline de hello. En outre, il spécifie que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **partitioneddata**. Hello **disponibilité** section spécifie ce jeu de données de sortie hello est généré sur une base mensuelle.

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Remplacez **storageaccountname** par le nom de votre compte Stockage Azure.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

Dans l’extrait de code hello JSON, vous créez un pipeline qui se compose d’une activité unique qui utilise des données de tooprocess Hive sur un cluster HDInsight.

fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **StorageLinkedService**) et dans **script**  dossier dans le conteneur de hello **adfgetstarted**.

Hello **définit** section spécifie les paramètres d’exécution qui sont passés de script hive de toohello en tant que valeurs de configuration Hive (exemple : ${hiveconf : inputtable}, ${hiveconf:partitionedtable}).

Hello **Démarrer** et **fin** propriétés de pipeline de hello spécifie la période active de hello du pipeline de hello.

Dans l’activité hello JSON, vous spécifiez ce script Hive hello s’exécute sur le calcul hello spécifié par hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.

> [!NOTE]
> Consultez la section « JSON de Pipeline » dans [Pipelines et les activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON utilisées Bonjour précédent exemple.
>
>

## <a name="set-global-variables"></a>Définir des variables globales
Dans Azure PowerShell, exécutez hello suivant les commandes après le remplacement des valeurs de hello par les vôtres :

> [!IMPORTANT]
> Consultez la section [Configuration requise](#prerequisites) pour savoir comment obtenir un ID client, une clé secrète client, un ID de locataire et un ID d’abonnement.
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Authentifier avec AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Créer une fabrique de données
Dans cette étape, vous créez une fabrique de données Azure Data Factory nommée **FirstDataFactoryREST**. Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, une activité de copie toocopy données à partir d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive une données tootransform du script Hive. Exécutez hello suivant la fabrique de données de commandes toocreate hello :

1. Affecter hello toovariable de commande nommé **cmd**.

    Confirmer ce nom hello hello fabrique de données vous spécifiez ici les correspondances (ADFCopyTutorialDF) hello nom spécifié dans hello **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si la fabrique de données hello a été créé avec succès, vous voyez hello JSON de fabrique de données hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.

    ```PowerShell
    Write-Host $results
    ```

Hello Notez les points suivants :

* nom de Hello Hello Azure Data Factory doit être globalement unique. Si vous voyez l’erreur hello dans les résultats : **nom de fabrique de données « FirstDataFactoryREST » n’est pas disponible**, hello comme suit :
  1. Modifier le nom hello (par exemple, yournameFirstDataFactoryREST) Bonjour **datafactory.json** fichier. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.
  2. Dans la première commande de hello où hello **$cmd** une valeur est assignée à la variable, remplacez FirstDataFactoryREST avec le nouveau nom de hello et exécutez la commande hello.
  3. Résultats de la série hello deux commandes tooinvoke hello API REST toocreate hello données fabrique et impression hello d’opération de hello.
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

Avant de créer un pipeline, vous devez toocreate quelques entités de fabrique de données tout d’abord. Vous créez tout d’abord les données de toolink services liés magasins/calcule tooyour données stocker, définissent l’entrée et sortie des données toorepresent de jeux de données dans des magasins de données liée.

## <a name="create-linked-services"></a>Créez des services liés
Dans cette étape, vous liez votre compte de stockage Azure et une fabrique de données à la demande Azure HDInsight cluster tooyour. blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple. Hello service lié HDInsight est toorun utilisé un script Hive spécifié dans l’activité hello du pipeline hello dans cet exemple.

### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage. Ce didacticiel, vous utilisez hello même compte de stockage Azure hello HQL et les données d’entrée/sortie toostore de fichier de script.

1. Affecter hello toovariable de commande nommé **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Exécutez la commande hello à l’aide de **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Afficher les résultats hello. Si hello lié service a été créé avec succès, vous voyez hello JSON pour le service lié de hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Créer le service lié Azure HDInsight
Dans cette étape, vous liez une fabrique de données à la demande HDInsight cluster tooyour. Hello cluster HDInsight est automatiquement créé lors de l’exécution et supprimée une fois ceci effectué inactifs et le traitement de la durée spécifiée hello. Vous pouvez utiliser votre propre cluster HDInsight au lieu d’utiliser un cluster HDInsight à la demande. Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .

1. Affecter hello toovariable de commande nommé **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
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
Dans cette étape, vous créez des groupes de données toorepresent hello d’entrée et sortie des données pour le traitement de la ruche. Ces jeux de données font référence toohello **StorageLinkedService** que vous avez créé précédemment dans ce didacticiel. Hello tooan de points de service lié compte de stockage Azure et de jeux de données spécifiez conteneur, dossier, le nom de fichier dans le stockage hello qui contient l’entrée et les données de sortie.

### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
Dans cette étape, vous créez hello dataset d’entrée toorepresent d’entrée les données stockées dans le stockage Blob Azure hello.

1. Affecter hello toovariable de commande nommé **cmd**.

    ```PowerShell
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
Dans cette étape, vous créez hello sortie dataset toorepresent sortie les données stockées dans hello le stockage Blob Azure.

1. Affecter hello toovariable de commande nommé **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
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
Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** . Secteur d’entrée est disponible mensuellement (fréquence : mois, intervalle : 1), la tranche de sortie est générée chaque mois et hello du planificateur pour l’activité de hello est également définie toomonthly. paramètres Hello pour le jeu de données de sortie hello et planificateur d’activité hello doivent correspondre. Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie. Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello.

Vérifiez que vous voyez hello **input.log** fichier Bonjour **adfgetstarted/inputdata** dossier hello stockage d’objets blob Azure et exécution hello suivant de pipeline de commande toodeploy hello. Depuis hello **Démarrer** et **fin** heures sont définies dans hello passée et **isPaused** est toofalse ensemble, pipeline de hello (activité dans le pipeline de hello) immédiatement après le déploiement.

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
4. Félicitations, vous avez réussi à créer votre premier pipeline avec Azure PowerShell.

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
Dans cette étape, vous utilisez tranches de toomonitor API REST de fabrique données produits par le pipeline de hello.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes). Par conséquent, s’attendent hello pipeline tootake **environ 30 minutes** tooprocess hello tranche.
>
>

Exécutez hello Invoke-Command et hello suivant jusqu'à ce que vous voyiez secteur hello dans **prêt** état ou **n’a pas pu** état. Lors de la tranche de hello est prêt, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.  la création d’un cluster de HDInsight à la demande Hello prend généralement un certain temps.

![données de sortie](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès. Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.
>
>

Vous pouvez également utiliser des sections de toomonitor portail Azure et résoudre les problèmes. Consultez la page [Surveillance et gestion des pipelines d’Azure Data Factory](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) pour plus d’informations.

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
| [Informations de référence sur l’API REST Data Factory](/rest/api/datafactory/) |Consultez la documentation complète sur les applets de commande de Data Factory |
| [Pipelines](data-factory-create-pipelines.md) |Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario. |
| [Groupes de données](data-factory-create-datasets.md) |Cet article vous aide à comprendre les jeux de données dans Azure Data Factory. |
| [Planification et exécution](data-factory-scheduling-and-execution.md) |Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory. |
| [Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.](data-factory-monitor-manage-app.md) |Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion. |
