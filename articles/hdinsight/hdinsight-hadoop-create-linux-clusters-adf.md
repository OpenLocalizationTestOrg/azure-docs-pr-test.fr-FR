---
title: "aaaCreate des clusters Hadoop de la demande à l’aide de Data Factory - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate à la demande Hadoop clusters dans HDInsight à l’aide d’Azure Data Factory."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Créer des clusters Hadoop à la demande dans HDInsight avec Azure Data Factor
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Azure Data Factory](../data-factory/data-factory-introduction.md) est un service d’intégration de données basées sur le cloud qui orchestre et automatise le déplacement de hello et la transformation de données. Il permet de créer un tooprocess juste-à-temps du cluster HDInsight Hadoop une tranche de données d’entrée et de supprimer le cluster de hello au terme du traitement de hello. Hello les avantages de l’utilisation d’un cluster de HDInsight Hadoop à la demande sont :

- Un paiement uniquement pour la tâche de temps hello s’exécute sur hello du cluster HDInsight Hadoop (plus un bref temps d’inactivité configurable). facturation Hello pour les clusters HDInsight est proportionnel par minute, que vous les utilisiez ou non. Lorsque vous utilisez un service lié HDInsight de la demande dans la fabrique de données, les clusters hello sont créés à la demande. Et les clusters hello sont supprimées automatiquement lorsque les tâches de hello sont terminées. Par conséquent, vous ne payez que pour la tâche hello heure et la durée d’inactivité brève hello (paramètre de durée de vie) en cours d’exécution.
- Vous pouvez créer un workflow à l’aide d’un pipeline Data Factory. Par exemple, vous pouvez avoir des données de toocopy hello pipeline à partir d’un tooan de SQL Server locale stockage d’objets blob Azure, traiter les données hello en exécutant un script Hive et un script Pig sur un cluster HDInsight Hadoop de la demande. Ensuite, copiez hello résultat données tooan Azure SQL Data Warehouse pour tooconsume d’applications BI.
- Vous pouvez planifier hello workflow toorun régulièrement (horaire, quotidienne, hebdomadaire, mensuelle, etc.).

Dans Azure Data Factory, une fabrique de données peut comporter un ou plusieurs pipelines de données. Un pipeline de données comprend une ou plusieurs activités. Il existe deux types d’activités : les [activités de déplacement des données](../data-factory/data-factory-data-movement-activities.md) et les [activités de transformation des données](../data-factory/data-factory-data-transformation-activities.md). Vous utilisez le déplacement des activités (actuellement, seule l’activité copie) toomove de données à partir d’un magasin de données de destination source données magasin tooa. Vous utilisez la transformation activités tootransform/processus de données. Activité de la ruche de HDInsight est une des activités de transformation hello pris en charge par la fabrique de données. Vous utilisez l’activité de transformation Hive hello dans ce didacticiel.

Vous pouvez configurer un toouse d’activité hive votre propre cluster HDInsight Hadoop ou un cluster de HDInsight Hadoop à la demande. Dans ce didacticiel, hello activité Hive dans le pipeline de fabrique de données hello est toouse configuré un cluster de HDInsight à la demande. Par conséquent, lorsque l’activité hello exécute tooprocess une tranche de données, voici ce qui se passe :

1. Un cluster HDInsight Hadoop est automatiquement créé pour la tranche hello juste-à-temps tooprocess.  
2. les données d’entrée Hello sont traitées en exécutant un script HiveQL sur le cluster de hello.
3. Hello cluster HDInsight Hadoop est supprimé après le traitement de hello est terminé et cluster de hello est inactive pour durée hello configuré (paramètre de la propriété timeToLive). Si la tranche de données suivante hello est disponible pour le traitement avec dans ce délai d’inactivité de la propriété timeToLive, hello même cluster est utilisé tooprocess hello tranche.  

Dans ce didacticiel, hello script HiveQL associé hello ruche activité exécute hello suivant des actions :

1. Crée une table externe références hello des données de journal web brut stockées dans un stockage d’objets Blob Azure.
2. Données brutes du hello partitions par année et mois.
3. Magasins hello les données partitionnées dans hello stockage d’objets blob Azure.

Dans ce didacticiel, hello script HiveQL associé hello ruche activité crée une table externe références hello les données de journal web brutes stockées Bonjour stockage d’objets Blob Azure. Voici les lignes d’exemple hello pour chaque mois dans le fichier d’entrée de hello.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

partitions de script HiveQL Hello hello données brutes par année et mois. Il crée trois dossiers de sortie en fonction de la saisie de hello. Chaque dossier contient un fichier avec les entrées correspondant à chaque mois.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Pour obtenir la liste des activités de transformation de données de fabrique de données dans l’activité de tooHive addition, consultez [transformer et analyser à l’aide d’Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Actuellement, vous ne pouvez créer qu’un cluster HDInsight version 3.2 à partir d’Azure Data Factory.

## <a name="prerequisites"></a>Composants requis
Avant de suivre les instructions hello dans cet article, vous devez disposer de hello éléments suivants :

* [Abonnement Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Préparer le compte de stockage
Vous pouvez utiliser des comptes de stockage toothree dans ce scénario :

- compte de stockage par défaut pour le cluster HDInsight de hello
- compte de stockage pour les données d’entrée hello
- compte de stockage pour les données de sortie hello

didacticiel de hello toosimplify, vous utilisez un compte tooserve hello trois des fins de stockage. Bonjour Azure PowerShell exemple de script dans cette section effectue hello tâches suivantes :

1. Ouvrez une session dans tooAzure.
2. Création d’un groupe de ressources Azure.
3. Création d’un compte Azure Storage.
4. Créer un conteneur d’objets Blob dans le compte de stockage hello
5. Copiez hello suivant le conteneur d’objets Blob toohello deux fichiers :

   * Fichier d’entrée : [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * Script HiveQL : [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Les deux fichiers sont stockés dans un conteneur d’objets blob public.


**tooprepare hello stockage et copier hello des fichiers à l’aide d’Azure PowerShell :**
> [!IMPORTANT]
> Spécifiez les noms de groupe de ressources Azure hello et de compte de stockage Azure hello qui sera créé par le script de hello.
> Notez **nom de groupe de ressources**, **nom de compte de stockage**, et **clé de compte de stockage** générées par le script de hello. Vous avez besoin dans la section suivante de hello.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Si vous avez besoin d’aide avec le script PowerShell de hello, consultez [Using hello Azure PowerShell avec le stockage Azure](../storage/common/storage-powershell-guide-full.md). Si vous le souhaitez toouse CLI d’Azure, consultez hello [annexe](#appendix) section pourquoi les script CLI d’Azure.

**tooexamine hello stockage compte et hello le contenu**

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **groupes de ressources** sur le volet gauche de hello.
3. Double-cliquez sur le nom de groupe de ressources hello que vous avez créé dans votre script PowerShell. Utilisez le filtre de hello si vous avez trop de groupes de ressources répertoriées.
4. Sur hello **ressources** vignette, doit avoir une seule ressource répertoriée, sauf si vous partagez un groupe de ressources hello avec d’autres projets. Cette ressource est un compte de stockage hello portant hello, que vous avez spécifié précédemment. Cliquez sur le nom de compte de stockage hello.
5. Cliquez sur hello **BLOB** vignettes.
6. Cliquez sur hello **adfgetstarted** conteneur. Vous voyez deux dossiers : **inputdata** et **script**.
7. Ouvrez le dossier de hello et vérifiez si hello dans les dossiers hello. Hello inputdata contient le fichier input.log de hello avec les données d’entrée et le dossier de scripts hello contient le fichier de script HiveQL hello.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Créer une fabrique de données à l’aide du modèle Resource Manager
Compte de stockage hello, les données d’entrée hello et hello script HiveQL préparé, vous êtes prêt toocreate une fabrique de données Azure. Il existe plusieurs méthodes pour créer la fabrique de données. Dans ce didacticiel, vous créez une fabrique de données en déployant un modèle Azure Resource Manager à l’aide de hello portail Azure. Vous pouvez également déployer un modèle Resource Manager en utilisant [l’interface de ligne de commande Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) et [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Pour les autres méthodes de création de fabriques de données, consultez la page [Didacticiel : créer votre première fabrique de données](../data-factory/data-factory-build-your-first-pipeline.md).

1. Cliquez sur hello suivant toosign image dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure. modèle de Hello se trouve dans https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json. Consultez hello [des entités de fabrique de données dans le modèle de hello](#data-factory-entities-in-the-template) section pour plus d’informations sur les entités définies dans le modèle de hello. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Sélectionnez **utiliser l’existant** option hello **groupe de ressources** paramètre et le nom hello sélectionnez hello du groupe de ressources créé à l’étape précédente de hello (à l’aide du script PowerShell).
3. Entrez un nom pour la fabrique de données hello (**nom de la fabrique de données**). Ce nom doit être globalement unique.
4. Entrez hello **nom de compte de stockage** et **clé de compte de stockage** notés à l’étape précédente de hello.
5. Sélectionnez **J’accepte les conditions générales toohello** mentionnées ci-dessus après avoir parcouru **termes et conditions**.
6. Sélectionnez **toodashboard du code confidentiel** option.
6. Cliquez sur **Acheter/Créer**. Vous voyez une vignette sur hello tableau de bord appelé **déploiement d’un modèle de déploiement**. Attendez que hello **groupe de ressources** panneau pour votre groupe de ressources s’ouvre. Vous pouvez également cliquer sur la vignette hello intitulée comme panneau de votre groupe de ressources groupe nom tooopen hello ressource.
6. Si le panneau des ressources de groupe hello n’est pas déjà ouvert, cliquez sur groupe de ressources hello vignette tooopen hello. Maintenant que vous allez voir une ressource de fabrique de données plus répertoriés en outre toohello des ressources de compte de stockage.
7. Cliquez sur nom hello votre fabrique de données (valeur que vous avez spécifié pour hello **nom de la fabrique de données** paramètre).
8. Dans le panneau de la fabrique de données hello, cliquez sur hello **diagramme** vignette. diagramme de Hello montre une activité avec un jeu de données d’entrée et un jeu de données de sortie :

    ![Diagramme du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    les noms de Hello sont définis dans le modèle de gestionnaire de ressources hello.
9. Double-cliquez sur **AzureBlobOutput**.
10. Sur hello **récents mis à jour les tranches**, vous devez voir un secteur. Si l’état de hello est **en cours d’exécution**, patientez jusqu'à ce qu’il a été modifié trop**prêt**. Cela prend généralement environ **20 minutes** toocreate un cluster HDInsight.

### <a name="check-hello-data-factory-output"></a>Vérifier la sortie de fabrique de données hello

1. Utilisez hello même procédure dans hello dernière session toocheck hello conteneurs du conteneur d’adfgetstarted hello. Il existe deux nouveaux conteneurs en outre trop**adfgetsarted**:

   * Un conteneur portant le nom qui suit le modèle de hello : `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Ce conteneur est un conteneur par défaut de hello pour le cluster HDInsight de hello.
   * adfjobs : ce conteneur est le conteneur hello pour les journaux de travaux hello ADF.

     sortie de fabrique de données Hello est stockée dans **afgetstarted** que vous avez configurés dans le modèle de gestionnaire de ressources hello.
2. Cliquez sur **adfgetstarted**.
3. Double-cliquez sur **partitioneddata**. Vous voyez un **année = 2014** dossier, car tous les journaux de web hello date année 2014.

    ![Sortie du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Si vous affichez la liste de hello, vous devez voir trois dossiers pour janvier, février et mars. Il y a un journal pour chaque mois.

    ![Sortie du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Entités de fabrique de données dans le modèle de hello
Voici comment le modèle de gestionnaire de ressources du niveau supérieur hello pour une fabrique de données ressemble à :

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Définir une fabrique de données
Vous définissez une fabrique de données dans le modèle de gestionnaire de ressources hello comme indiqué dans hello suivant l’exemple :  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
Hello dataFactoryName est le nom hello hello fabrique de données que vous spécifiez lorsque vous déployez le modèle de hello. Fabrique de données est uniquement pris en charge dans les régions est des États-Unis, ouest des États-Unis et Europe du Nord hello.

### <a name="defining-entities-within-hello-data-factory"></a>Définition des entités au sein de la fabrique de données hello
Hello des entités de fabrique de données suivantes sont définies dans le modèle JSON hello :

* [Service lié Azure Storage](#azure-storage-linked-service)
* [Service lié à la demande HDInsight](#hdinsight-on-demand-linked-service)
* [Jeu de données d'entrée d'objet Blob Azure](#azure-blob-input-dataset)
* [Jeu de données de sortie d’objet Blob Azure](#azure-blob-output-dataset)
* [Pipeline de données avec une activité de copie](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Service lié Azure Storage
Hello le stockage Azure lié à des liens de service votre fabrique de données toohello compte stockage Azure. Dans ce didacticiel, hello même compte de stockage est utilisé en tant que compte de stockage HDInsight hello par défaut, le stockage de données d’entrée et stockage des données de sortie. Par conséquent, vous ne définissez qu’un seul service lié Stockage Azure. Dans la définition de service lié de hello, vous spécifiez le nom de hello et la clé de votre compte de stockage Azure. Consultez [service lié Azure Storage](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur JSON propriétés utilisées toodefine un stockage Azure le service lié.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Hello **connectionString** utilise hello paramètres storageAccountName et storageAccountKey. Vous spécifiez des valeurs pour ces paramètres lors du déploiement de modèle de hello.  

#### <a name="hdinsight-on-demand-linked-service"></a>Service lié à la demande HDInsight
Bonjour à la demande HDInsight lié définition de service, vous spécifiez les valeurs des paramètres de configuration qui sont utilisés par hello Data Factory service toocreate un HDInsight Hadoop de cluster lors de l’exécution. Consultez [services liés de calcul](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article pour plus d’informations sur JSON propriétés utilisées toodefine un service lié à la demande de HDInsight.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Hello Notez les points suivants :

* Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous.
* Hello cluster HDInsight Hadoop est créé dans hello même région que le compte de stockage hello.
* Hello d’avis *timeToLive* paramètre. fabrique de données Hello supprime le cluster de hello automatiquement une fois le cluster de hello est inactif pendant 30 minutes.
* Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois qu’une tranche doit toobe traité sauf s’il existe un cluster dynamique existant (**timeToLive**) et est supprimé quand le traitement de hello est effectué.

Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

> [!IMPORTANT]
> Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ». Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.

#### <a name="azure-blob-input-dataset"></a>Jeu de données d'entrée d'objet Blob Azure
Dans la définition du jeu de données d’entrée hello, vous spécifiez les noms de conteneur d’objets blob, de dossier et de fichier qui contient les données d’entrée hello hello. Consultez [propriétés de jeu de données d’objets Blob Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

Notez hello suivant des paramètres spécifiques dans la définition de JSON hello :

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Jeu de données de sortie d’objet Blob Azure
Dans la définition de dataset de sortie hello, vous spécifiez les noms de conteneur d’objets blob et le dossier qui contient les données de sortie hello hello. Consultez [propriétés de jeu de données d’objets Blob Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

Hello folderPath spécifie hello chemin d’accès toohello dossier qui contient les données de sortie hello :

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Hello [dataset disponibilité](../data-factory/data-factory-create-datasets.md#dataset-availability) paramètre est le suivant :

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

Dans Azure Data Factory, pipeline de sortie dataset disponibilité lecteurs hello. Dans cet exemple, hello tranche est produite mensuelle hello dernier jour du mois (EndOfInterval). Pour plus d’informations, consultez [Planification et exécution avec Data Factory](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Pipeline de données
Vous définissez un pipeline qui transforme les données en exécutant le script Hive sur un cluster Azure HDInsight à la demande. Consultez [JSON de Pipeline](../data-factory/data-factory-create-pipelines.md#pipeline-json) pour les descriptions des éléments utilisés de JSON toodefine un pipeline dans cet exemple.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
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
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

pipeline de Hello contient une activité, HDInsightHive activité. Étant donné que les dates de début et de fin appartiennent toutes deux au mois de janvier 2016, le traitement ne porte que sur les données d’un seul mois (une tranche). Les deux *Démarrer* et *fin* d’activité hello ont une date passée, donc hello fabrique de données traite les données pour le mois de hello immédiatement. Si la fin de hello est une date ultérieure, fabrique de données hello crée une autre tranche hello moment venu. Pour plus d’informations, consultez [Planification et exécution avec Data Factory](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Nettoyer le didacticiel de hello

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>Supprimer des conteneurs d’objets blob hello créés par cluster de HDInsight à la demande
Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois qu’une tranche doit toobe traité sauf s’il existe un cluster dynamique existant (timeToLive) ; et cluster de hello est supprimé lorsque le traitement de hello est effectué. Pour chaque cluster, Azure Data Factory crée un conteneur d’objets blob dans hello stockage d’objets blob Azure utilisé comme compte de stockage par défaut hello pour le cluster de hello. Bien que le cluster HDInsight est supprimé, conteneur de stockage d’objets blob hello par défaut et le compte de stockage hello associée ne sont pas supprimés. Ce comportement est normal. Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Supprimer hello **adfjobs** et **adfyourdatafactoryname-linkedservicename-datetimestamp** dossiers. conteneur d’adfjobs Hello contient des journaux de travail à partir d’Azure Data Factory.

### <a name="delete-hello-resource-group"></a>Supprimer le groupe de ressources hello
[Le Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) est toodeploy utilisé, gérer et surveiller votre solution en tant que groupe.  La suppression d’un groupe de ressources supprime tous les composants hello à l’intérieur du groupe de hello.  

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **groupes de ressources** sur le volet gauche de hello.
3. Cliquez sur le nom de groupe de ressources hello que vous avez créé dans votre script PowerShell. Utilisez le filtre de hello si vous avez trop de groupes de ressources répertoriées. Il ouvre le groupe de ressources hello dans un nouveau panneau.
4. Sur hello **ressources** vignette, doit avoir compte de stockage par défaut hello et la fabrique de données hello répertoriés, sauf si vous partagez un groupe de ressources hello avec d’autres projets.
5. Cliquez sur **supprimer** haut hello du Panneau de hello. Cela supprime le compte de stockage hello et données hello stockées dans le compte de stockage hello.
6. Entrez la suppression tooconfirm nom du groupe de ressources hello, puis cliquez sur **supprimer**.

Au cas où vous ne souhaitez pas compte de stockage toodelete hello lorsque vous supprimez le groupe de ressources hello, envisagez de hello suivant architecture en séparant les données d’entreprise hello de compte de stockage par défaut hello. Dans ce cas, vous disposez d’un groupe de ressources pour le compte de stockage hello avec les données métier hello et hello autre groupe de ressources pour le compte de stockage par défaut hello pour HDInsight lié hello et service de fabrique de données. Lorsque vous supprimez le deuxième groupe de ressources hello, il n’affecte pas de compte de stockage de données hello entreprise. toodo pour :

* Ajoutez hello suivant du groupe de ressources de niveau supérieur de toohello, ainsi que de hello Microsoft.DataFactory/datafactories des ressources dans votre modèle de gestionnaire de ressources. Ce code crée un compte de stockage :

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Ajouter un nouveau service lié point toohello compte de stockage :

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Configurer hello HDInsight liée à la demande service avec un dependsOn supplémentaire et une additionalLinkedServiceNames :

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toouse Azure Data Factory toocreate à la demande HDInsight cluster tooprocess ruche de travaux. tooread plus :

* [Didacticiel Hadoop : prise en main de Hadoop sous Linux dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Documentation HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Documentation Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Annexe

### <a name="azure-cli-script"></a>Script d’interface de ligne de commande Azure
Vous pouvez utiliser CLI d’Azure au lieu d’utiliser le didacticiel de hello toodo Azure PowerShell. toouse CLI d’Azure, installez tout d’abord CLI d’Azure conformément à hello suivant les instructions :

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Utiliser le stockage Azure CLI tooprepare hello et copiez les fichiers hello

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

nom du conteneur Hello est *adfgetstarted*. Gardez-le tel quel. Sinon, vous devez modèle de gestionnaire de ressources tooupdate hello. Si vous avez besoin d’aide avec ce script CLI, consultez [Using hello CLI d’Azure avec le stockage Azure](../storage/common/storage-azure-cli.md).
