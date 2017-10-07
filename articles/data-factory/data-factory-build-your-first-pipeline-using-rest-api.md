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
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="125a9-103">Didacticiel : Créer votre première fabrique de données Azure en utilisant l’API REST Data Factory</span><span class="sxs-lookup"><span data-stu-id="125a9-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="125a9-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="125a9-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="125a9-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="125a9-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="125a9-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="125a9-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="125a9-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="125a9-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="125a9-108">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="125a9-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="125a9-109">API REST</span><span class="sxs-lookup"><span data-stu-id="125a9-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="125a9-110">Dans cet article, vous utilisez API REST de fabrique données toocreate votre première Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="125a9-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="125a9-111">didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="125a9-112">pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="125a9-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="125a9-113">Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce.</span><span class="sxs-lookup"><span data-stu-id="125a9-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="125a9-114">pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="125a9-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="125a9-115">Cet article ne couvre pas hello toutes les API REST.</span><span class="sxs-lookup"><span data-stu-id="125a9-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="125a9-116">pour obtenir une documentation complète sur les API REST, consultez [Informations de référence sur l’API REST Data Factory](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="125a9-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="125a9-117">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="125a9-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="125a9-118">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="125a9-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="125a9-119">Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="125a9-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="125a9-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="125a9-120">Prerequisites</span></span>
* <span data-ttu-id="125a9-121">Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.</span><span class="sxs-lookup"><span data-stu-id="125a9-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="125a9-122">Installez [Curl](https://curl.haxx.se/dlwiz/) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="125a9-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="125a9-123">Vous utilisez l’outil CURL de hello avec d’autres commandes toocreate une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="125a9-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="125a9-124">Suivez les instructions de [cet article](../azure-resource-manager/resource-group-create-service-principal-portal.md) pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="125a9-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="125a9-125">Créez une application Web nommée **ADFGetStartedApp** dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="125a9-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="125a9-126">Obtenez un **ID client** et une **clé secrète**.</span><span class="sxs-lookup"><span data-stu-id="125a9-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="125a9-127">Obtenez l’ **ID de locataire**.</span><span class="sxs-lookup"><span data-stu-id="125a9-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="125a9-128">Affecter hello **ADFGetStartedApp** application toohello **collaborateur de fabrique de données** rôle.</span><span class="sxs-lookup"><span data-stu-id="125a9-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="125a9-129">Installez [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="125a9-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="125a9-130">Lancez **PowerShell** et hello exécution de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="125a9-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="125a9-131">Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="125a9-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="125a9-132">Si vous fermez et rouvrez, vous devez à nouveau les commandes de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="125a9-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="125a9-133">Exécutez **AzureRmAccount de connexion** et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="125a9-134">Exécutez **Get-AzureRmSubscription** tooview tous hello abonnements pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="125a9-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="125a9-135">Exécutez **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello abonnement toowork avec.</span><span class="sxs-lookup"><span data-stu-id="125a9-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="125a9-136">Remplacez **NameOfAzureSubscription** avec le nom de hello de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="125a9-137">Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello commande Bonjour PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="125a9-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="125a9-138">Certaines des étapes hello dans ce didacticiel supposent que vous utilisez le groupe de ressources hello nommé ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="125a9-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="125a9-139">Si vous utilisez un autre groupe de ressources, vous devez le nom de hello toouse de votre groupe de ressources à la place de ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="125a9-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="125a9-140">Créer des définitions JSON</span><span class="sxs-lookup"><span data-stu-id="125a9-140">Create JSON definitions</span></span>
<span data-ttu-id="125a9-141">Créer des fichiers JSON dans le dossier hello où se trouve curl.exe suivants.</span><span class="sxs-lookup"><span data-stu-id="125a9-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="125a9-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="125a9-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="125a9-143">Nom doit être globalement unique, vous pouvez donc tooprefix/suffixe ADFCopyTutorialDF toomake il un nom unique.</span><span class="sxs-lookup"><span data-stu-id="125a9-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="125a9-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="125a9-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="125a9-145">Remplacez **accountname** et **accountkey** par le nom et la clé de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="125a9-146">toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="125a9-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="125a9-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="125a9-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="125a9-148">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="125a9-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="125a9-149">Propriété</span><span class="sxs-lookup"><span data-stu-id="125a9-149">Property</span></span> | <span data-ttu-id="125a9-150">Description</span><span class="sxs-lookup"><span data-stu-id="125a9-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="125a9-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="125a9-151">ClusterSize</span></span> |<span data-ttu-id="125a9-152">Taille du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="125a9-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="125a9-153">TimeToLive</span></span> |<span data-ttu-id="125a9-154">Spécifie la durée d’inactivité de ce hello pour le cluster HDInsight de hello, avant d’être supprimé.</span><span class="sxs-lookup"><span data-stu-id="125a9-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="125a9-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="125a9-155">linkedServiceName</span></span> |<span data-ttu-id="125a9-156">Spécifie le compte de stockage hello toostore utilisé hello journaux générés par HDInsight</span><span class="sxs-lookup"><span data-stu-id="125a9-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="125a9-157">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="125a9-157">Note hello following points:</span></span>

* <span data-ttu-id="125a9-158">Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello au-dessus de JSON.</span><span class="sxs-lookup"><span data-stu-id="125a9-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="125a9-159">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="125a9-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="125a9-160">Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="125a9-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="125a9-161">Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="125a9-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="125a9-162">Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="125a9-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="125a9-163">HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="125a9-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="125a9-164">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="125a9-164">This behavior is by design.</span></span> <span data-ttu-id="125a9-165">Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois une tranche est traitée, sauf s’il existe un cluster dynamique existant (**timeToLive**) et est supprimé quand le traitement de hello est effectué.</span><span class="sxs-lookup"><span data-stu-id="125a9-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="125a9-166">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="125a9-167">Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="125a9-168">les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ».</span><span class="sxs-lookup"><span data-stu-id="125a9-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="125a9-169">Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="125a9-170">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="125a9-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="125a9-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="125a9-171">inputdataset.json</span></span>

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

<span data-ttu-id="125a9-172">Hello JSON définit un dataset nommé **AzureBlobInput**, qui représente les données d’entrée pour une activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="125a9-173">En outre, il spécifie que les données d’entrée hello se trouve dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="125a9-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="125a9-174">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="125a9-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="125a9-175">Propriété</span><span class="sxs-lookup"><span data-stu-id="125a9-175">Property</span></span> | <span data-ttu-id="125a9-176">Description</span><span class="sxs-lookup"><span data-stu-id="125a9-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="125a9-177">type</span><span class="sxs-lookup"><span data-stu-id="125a9-177">type</span></span> |<span data-ttu-id="125a9-178">propriété de type Hello a la valeur tooAzureBlob, car les données résident dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="125a9-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="125a9-179">linkedServiceName</span></span> |<span data-ttu-id="125a9-180">fait référence toohello StorageLinkedService que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="125a9-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="125a9-181">fileName</span><span class="sxs-lookup"><span data-stu-id="125a9-181">fileName</span></span> |<span data-ttu-id="125a9-182">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="125a9-182">This property is optional.</span></span> <span data-ttu-id="125a9-183">Si vous omettez cette propriété, tous les fichiers hello hello folderPath sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="125a9-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="125a9-184">Dans ce cas, uniquement les input.log hello est traitée.</span><span class="sxs-lookup"><span data-stu-id="125a9-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="125a9-185">type</span><span class="sxs-lookup"><span data-stu-id="125a9-185">type</span></span> |<span data-ttu-id="125a9-186">les fichiers journaux Hello étant au format texte, nous utilisons TextFormat.</span><span class="sxs-lookup"><span data-stu-id="125a9-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="125a9-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="125a9-187">columnDelimiter</span></span> |<span data-ttu-id="125a9-188">colonnes dans les fichiers journaux de hello sont délimitées par une virgule ()</span><span class="sxs-lookup"><span data-stu-id="125a9-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="125a9-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="125a9-189">frequency/interval</span></span> |<span data-ttu-id="125a9-190">fréquence égale tooMonth et l’intervalle est 1, ce qui signifie que les tranches d’entrée hello sont disponibles chaque mois.</span><span class="sxs-lookup"><span data-stu-id="125a9-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="125a9-191">external</span><span class="sxs-lookup"><span data-stu-id="125a9-191">external</span></span> |<span data-ttu-id="125a9-192">Cette propriété a la valeur tootrue si les données d’entrée hello ne sont pas générées par le service de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="125a9-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="125a9-193">outputdataset.json</span></span>

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

<span data-ttu-id="125a9-194">Hello JSON définit un dataset nommé **AzureBlobOutput**, qui représente les données de sortie d’une activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="125a9-195">En outre, il spécifie que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="125a9-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="125a9-196">Hello **disponibilité** section spécifie ce jeu de données de sortie hello est généré sur une base mensuelle.</span><span class="sxs-lookup"><span data-stu-id="125a9-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="125a9-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="125a9-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="125a9-198">Remplacez **storageaccountname** par le nom de votre compte Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
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

<span data-ttu-id="125a9-199">Dans l’extrait de code hello JSON, vous créez un pipeline qui se compose d’une activité unique qui utilise des données de tooprocess Hive sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="125a9-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="125a9-200">fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **StorageLinkedService**) et dans **script**  dossier dans le conteneur de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="125a9-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="125a9-201">Hello **définit** section spécifie les paramètres d’exécution qui sont passés de script hive de toohello en tant que valeurs de configuration Hive (exemple : ${hiveconf : inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="125a9-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="125a9-202">Hello **Démarrer** et **fin** propriétés de pipeline de hello spécifie la période active de hello du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="125a9-203">Dans l’activité hello JSON, vous spécifiez ce script Hive hello s’exécute sur le calcul hello spécifié par hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="125a9-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="125a9-204">Consultez la section « JSON de Pipeline » dans [Pipelines et les activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON utilisées Bonjour précédent exemple.</span><span class="sxs-lookup"><span data-stu-id="125a9-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="125a9-205">Définir des variables globales</span><span class="sxs-lookup"><span data-stu-id="125a9-205">Set global variables</span></span>
<span data-ttu-id="125a9-206">Dans Azure PowerShell, exécutez hello suivant les commandes après le remplacement des valeurs de hello par les vôtres :</span><span class="sxs-lookup"><span data-stu-id="125a9-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="125a9-207">Consultez la section [Configuration requise](#prerequisites) pour savoir comment obtenir un ID client, une clé secrète client, un ID de locataire et un ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="125a9-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
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


## <a name="authenticate-with-aad"></a><span data-ttu-id="125a9-208">Authentifier avec AAD</span><span class="sxs-lookup"><span data-stu-id="125a9-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="125a9-209">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="125a9-209">Create data factory</span></span>
<span data-ttu-id="125a9-210">Dans cette étape, vous créez une fabrique de données Azure Data Factory nommée **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="125a9-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="125a9-211">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="125a9-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="125a9-212">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="125a9-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="125a9-213">Par exemple, une activité de copie toocopy données à partir d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive une données tootransform du script Hive.</span><span class="sxs-lookup"><span data-stu-id="125a9-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="125a9-214">Exécutez hello suivant la fabrique de données de commandes toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="125a9-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="125a9-215">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="125a9-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="125a9-216">Confirmer ce nom hello hello fabrique de données vous spécifiez ici les correspondances (ADFCopyTutorialDF) hello nom spécifié dans hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="125a9-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="125a9-217">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="125a9-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="125a9-218">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-218">View hello results.</span></span> <span data-ttu-id="125a9-219">Si la fabrique de données hello a été créé avec succès, vous voyez hello JSON de fabrique de données hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="125a9-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="125a9-220">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="125a9-220">Note hello following points:</span></span>

* <span data-ttu-id="125a9-221">nom de Hello Hello Azure Data Factory doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="125a9-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="125a9-222">Si vous voyez l’erreur hello dans les résultats : **nom de fabrique de données « FirstDataFactoryREST » n’est pas disponible**, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="125a9-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="125a9-223">Modifier le nom hello (par exemple, yournameFirstDataFactoryREST) Bonjour **datafactory.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="125a9-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="125a9-224">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="125a9-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="125a9-225">Dans la première commande de hello où hello **$cmd** une valeur est assignée à la variable, remplacez FirstDataFactoryREST avec le nouveau nom de hello et exécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="125a9-226">Résultats de la série hello deux commandes tooinvoke hello API REST toocreate hello données fabrique et impression hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="125a9-227">instances de fabrique de données toocreate, vous devez toobe un collaborateur/administrateur Hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="125a9-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="125a9-228">nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="125a9-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="125a9-229">Si vous recevez une erreur de hello : «**cet abonnement n’est pas un espace de noms inscrit toouse Microsoft.DataFactory**», effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :</span><span class="sxs-lookup"><span data-stu-id="125a9-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="125a9-230">Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="125a9-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="125a9-231">Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello :</span><span class="sxs-lookup"><span data-stu-id="125a9-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="125a9-232">Connexion à l’aide de hello abonnement Azure dans hello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="125a9-233">Cette action enregistre automatiquement le fournisseur hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="125a9-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="125a9-234">Avant de créer un pipeline, vous devez toocreate quelques entités de fabrique de données tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="125a9-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="125a9-235">Vous créez tout d’abord les données de toolink services liés magasins/calcule tooyour données stocker, définissent l’entrée et sortie des données toorepresent de jeux de données dans des magasins de données liée.</span><span class="sxs-lookup"><span data-stu-id="125a9-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="125a9-236">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="125a9-236">Create linked services</span></span>
<span data-ttu-id="125a9-237">Dans cette étape, vous liez votre compte de stockage Azure et une fabrique de données à la demande Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="125a9-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="125a9-238">blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="125a9-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="125a9-239">Hello service lié HDInsight est toorun utilisé un script Hive spécifié dans l’activité hello du pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="125a9-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="125a9-240">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="125a9-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="125a9-241">Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="125a9-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="125a9-242">Ce didacticiel, vous utilisez hello même compte de stockage Azure hello HQL et les données d’entrée/sortie toostore de fichier de script.</span><span class="sxs-lookup"><span data-stu-id="125a9-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="125a9-243">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="125a9-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="125a9-244">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="125a9-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="125a9-245">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-245">View hello results.</span></span> <span data-ttu-id="125a9-246">Si hello lié service a été créé avec succès, vous voyez hello JSON pour le service lié de hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="125a9-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="125a9-247">Créer le service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="125a9-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="125a9-248">Dans cette étape, vous liez une fabrique de données à la demande HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="125a9-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="125a9-249">Hello cluster HDInsight est automatiquement créé lors de l’exécution et supprimée une fois ceci effectué inactifs et le traitement de la durée spécifiée hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="125a9-250">Vous pouvez utiliser votre propre cluster HDInsight au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="125a9-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="125a9-251">Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="125a9-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="125a9-252">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="125a9-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="125a9-253">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="125a9-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="125a9-254">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-254">View hello results.</span></span> <span data-ttu-id="125a9-255">Si hello lié service a été créé avec succès, vous voyez hello JSON pour le service lié de hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="125a9-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="125a9-256">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="125a9-256">Create datasets</span></span>
<span data-ttu-id="125a9-257">Dans cette étape, vous créez des groupes de données toorepresent hello d’entrée et sortie des données pour le traitement de la ruche.</span><span class="sxs-lookup"><span data-stu-id="125a9-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="125a9-258">Ces jeux de données font référence toohello **StorageLinkedService** que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="125a9-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="125a9-259">Hello tooan de points de service lié compte de stockage Azure et de jeux de données spécifiez conteneur, dossier, le nom de fichier dans le stockage hello qui contient l’entrée et les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="125a9-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="125a9-260">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="125a9-260">Create input dataset</span></span>
<span data-ttu-id="125a9-261">Dans cette étape, vous créez hello dataset d’entrée toorepresent d’entrée les données stockées dans le stockage Blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="125a9-262">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="125a9-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="125a9-263">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="125a9-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="125a9-264">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-264">View hello results.</span></span> <span data-ttu-id="125a9-265">Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="125a9-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="125a9-266">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="125a9-266">Create output dataset</span></span>
<span data-ttu-id="125a9-267">Dans cette étape, vous créez hello sortie dataset toorepresent sortie les données stockées dans hello le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="125a9-268">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="125a9-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="125a9-269">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="125a9-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="125a9-270">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-270">View hello results.</span></span> <span data-ttu-id="125a9-271">Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="125a9-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="125a9-272">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="125a9-272">Create pipeline</span></span>
<span data-ttu-id="125a9-273">Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="125a9-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="125a9-274">Secteur d’entrée est disponible mensuellement (fréquence : mois, intervalle : 1), la tranche de sortie est générée chaque mois et hello du planificateur pour l’activité de hello est également définie toomonthly.</span><span class="sxs-lookup"><span data-stu-id="125a9-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="125a9-275">paramètres Hello pour le jeu de données de sortie hello et planificateur d’activité hello doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="125a9-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="125a9-276">Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="125a9-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="125a9-277">Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="125a9-278">Vérifiez que vous voyez hello **input.log** fichier Bonjour **adfgetstarted/inputdata** dossier hello stockage d’objets blob Azure et exécution hello suivant de pipeline de commande toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="125a9-279">Depuis hello **Démarrer** et **fin** heures sont définies dans hello passée et **isPaused** est toofalse ensemble, pipeline de hello (activité dans le pipeline de hello) immédiatement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="125a9-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="125a9-280">Affecter hello toovariable de commande nommé **cmd**.</span><span class="sxs-lookup"><span data-stu-id="125a9-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="125a9-281">Exécutez la commande hello à l’aide de **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="125a9-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="125a9-282">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-282">View hello results.</span></span> <span data-ttu-id="125a9-283">Si hello dataset a été créé avec succès, vous voyez hello JSON pour le dataset hello Bonjour **résultats**; sinon, vous voyez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="125a9-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="125a9-284">Félicitations, vous avez réussi à créer votre premier pipeline avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="125a9-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="125a9-285">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="125a9-285">Monitor pipeline</span></span>
<span data-ttu-id="125a9-286">Dans cette étape, vous utilisez tranches de toomonitor API REST de fabrique données produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

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
> <span data-ttu-id="125a9-287">La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="125a9-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="125a9-288">Par conséquent, s’attendent hello pipeline tootake **environ 30 minutes** tooprocess hello tranche.</span><span class="sxs-lookup"><span data-stu-id="125a9-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="125a9-289">Exécutez hello Invoke-Command et hello suivant jusqu'à ce que vous voyiez secteur hello dans **prêt** état ou **n’a pas pu** état.</span><span class="sxs-lookup"><span data-stu-id="125a9-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="125a9-290">Lors de la tranche de hello est prêt, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="125a9-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="125a9-291">la création d’un cluster de HDInsight à la demande Hello prend généralement un certain temps.</span><span class="sxs-lookup"><span data-stu-id="125a9-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![données de sortie](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="125a9-293">fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès.</span><span class="sxs-lookup"><span data-stu-id="125a9-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="125a9-294">Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="125a9-295">Vous pouvez également utiliser des sections de toomonitor portail Azure et résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="125a9-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="125a9-296">Consultez la page [Surveillance et gestion des pipelines d’Azure Data Factory](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="125a9-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="125a9-297">Résumé</span><span class="sxs-lookup"><span data-stu-id="125a9-297">Summary</span></span>
<span data-ttu-id="125a9-298">Dans ce didacticiel, vous avez créé un Azure data factory tooprocess de données en exécutant le script Hive sur un cluster de hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="125a9-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="125a9-299">Vous avez utilisé hello éditeur Data Factory dans Bonjour Azure toodo portail Bonjour comme suit :</span><span class="sxs-lookup"><span data-stu-id="125a9-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="125a9-300">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="125a9-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="125a9-301">Création de deux **services liés**:</span><span class="sxs-lookup"><span data-stu-id="125a9-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="125a9-302">**Le stockage Azure** lié service toolink votre stockage d’objets blob Azure qui contient la fabrique de données toohello les fichiers d’entrée/sortie.</span><span class="sxs-lookup"><span data-stu-id="125a9-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="125a9-303">**Azure HDInsight** à la demande liée service toolink une fabrique de données à la demande HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="125a9-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="125a9-304">Azure Data Factory crée un HDInsight Hadoop données d’entrée de cluster juste-à-temps tooprocess et générer les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="125a9-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="125a9-305">Créé deux **jeux de données**, qui décrivent les données d’entrée et de sortie pour l’activité HDInsight Hive dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="125a9-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="125a9-306">Création d’un **pipeline** avec une activité **Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="125a9-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="125a9-307">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="125a9-307">Next steps</span></span>
<span data-ttu-id="125a9-308">Dans cet article, vous avez créé un pipeline avec une activité de transformation (Activité HDInsight) qui exécute un script Hive sur un cluster Azure HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="125a9-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="125a9-309">toosee toouse un activité de copie toocopy des données d’une tooAzure d’objets Blob Azure SQL, voir [didacticiel : copier des données à partir d’un tooAzure d’objets Blob Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="125a9-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="125a9-310">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="125a9-310">See Also</span></span>
| <span data-ttu-id="125a9-311">Rubrique</span><span class="sxs-lookup"><span data-stu-id="125a9-311">Topic</span></span> | <span data-ttu-id="125a9-312">Description</span><span class="sxs-lookup"><span data-stu-id="125a9-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="125a9-313">Informations de référence sur l’API REST Data Factory</span><span class="sxs-lookup"><span data-stu-id="125a9-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="125a9-314">Consultez la documentation complète sur les applets de commande de Data Factory</span><span class="sxs-lookup"><span data-stu-id="125a9-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="125a9-315">Pipelines</span><span class="sxs-lookup"><span data-stu-id="125a9-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="125a9-316">Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario.</span><span class="sxs-lookup"><span data-stu-id="125a9-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="125a9-317">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="125a9-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="125a9-318">Cet article vous aide à comprendre les jeux de données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="125a9-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="125a9-319">Planification et exécution</span><span class="sxs-lookup"><span data-stu-id="125a9-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="125a9-320">Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="125a9-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="125a9-321">Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="125a9-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="125a9-322">Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion.</span><span class="sxs-lookup"><span data-stu-id="125a9-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
