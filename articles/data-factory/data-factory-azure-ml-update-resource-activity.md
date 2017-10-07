---
title: "les modèles de Machine Learning aaaUpdate à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Décrit comment toocreate créer des pipelines PRÉDICTIFS à l’aide d’Azure Data Factory et Azure Machine Learning"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="abf19-103">Mettre à jour les modèles Azure Machine Learning à l’aide de l’activité des ressources de mise à jour</span><span class="sxs-lookup"><span data-stu-id="abf19-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="abf19-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="abf19-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="abf19-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="abf19-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="abf19-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="abf19-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="abf19-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="abf19-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="abf19-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="abf19-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="abf19-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="abf19-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="abf19-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="abf19-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="abf19-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="abf19-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="abf19-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="abf19-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="abf19-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="abf19-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="abf19-114">Cet article complète hello principal Azure Data Factory - article de l’intégration d’Azure Machine Learning : [créer des pipelines PRÉDICTIFS à l’aide d’Azure Machine Learning et Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="abf19-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="abf19-115">Si vous n’avez pas déjà fait, passez en revue l’article principal de hello avant la lecture de cet article.</span><span class="sxs-lookup"><span data-stu-id="abf19-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="abf19-116">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="abf19-116">Overview</span></span>
<span data-ttu-id="abf19-117">Au fil du temps, utiliser des modèles prédictifs hello dans des expériences de score Azure ML hello doivent toobe reformé à l’aide de nouveaux jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="abf19-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="abf19-118">Une fois que vous avez terminé avec le réapprentissage, vous souhaitez hello tooupdate calcul du score du service web avec hello reformés modèle ML.</span><span class="sxs-lookup"><span data-stu-id="abf19-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="abf19-119">Hello étapes classiques tooenable réapprentissage et mise à jour des modèles Azure ML via les services web sont :</span><span class="sxs-lookup"><span data-stu-id="abf19-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="abf19-120">Créez une expérience dans [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="abf19-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="abf19-121">Lorsque vous êtes satisfait de modèle de hello, utiliser des services web à la fois hello Azure ML Studio toopublish **expérience de formation** et le score /**expérience prédictive**.</span><span class="sxs-lookup"><span data-stu-id="abf19-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="abf19-122">Hello tableau suivant décrit les services web hello utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="abf19-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="abf19-123">Pour plus d’informations, consultez [Reformation des modèles Machine Learning par programme](../machine-learning/machine-learning-retrain-models-programmatically.md) .</span><span class="sxs-lookup"><span data-stu-id="abf19-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="abf19-124">**Service Web de formation** - Reçoit les données d’apprentissage et produit les modèles formés.</span><span class="sxs-lookup"><span data-stu-id="abf19-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="abf19-125">sortie de Hello de recyclage de hello est un fichier .ilearner dans un stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="abf19-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="abf19-126">Hello **par défaut du point de terminaison** est automatiquement créé pour vous lors de la publication de la formation de hello expérimenter comme un service web.</span><span class="sxs-lookup"><span data-stu-id="abf19-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="abf19-127">Vous pouvez créer plusieurs points de terminaison, mais hello exemple utilise uniquement les point de terminaison de valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="abf19-128">**Service Web de notation** - Reçoit des exemples de données sans étiquette et effectue des prédictions.</span><span class="sxs-lookup"><span data-stu-id="abf19-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="abf19-129">sortie Hello de prédiction peut avoir différentes formes, par exemple un fichier .csv ou des lignes dans une base de données SQL Azure, selon la configuration de hello d’expérimentation de hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="abf19-130">point de terminaison par défaut Hello est automatiquement créé lorsque vous publiez l’expérience de prédictive hello comme un service web.</span><span class="sxs-lookup"><span data-stu-id="abf19-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="abf19-131">Hello image suivante illustre les relations de hello entre les jeux d’apprentissage et le score des points de terminaison dans Azure ML.</span><span class="sxs-lookup"><span data-stu-id="abf19-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVICES WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="abf19-133">Vous pouvez appeler hello **formation service web** à l’aide de hello **activité de l’exécution du lot Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="abf19-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="abf19-134">L’appel d’un service web de formation est similaire à l’appel d’un service web Azure ML (service web de notation) pour les données de notation.</span><span class="sxs-lookup"><span data-stu-id="abf19-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="abf19-135">Bonjour précédent garde sections Comment tooinvoke un service web de Azure ML à partir d’une fabrique de données Azure de pipeline en détail.</span><span class="sxs-lookup"><span data-stu-id="abf19-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="abf19-136">Vous pouvez appeler hello **calcul du score du service web** à l’aide de hello **activité de ressource mise à jour Azure ML** service web qui vient d’être formé hello tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="abf19-137">Hello exemple suivant fournit les définitions de service lié :</span><span class="sxs-lookup"><span data-stu-id="abf19-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="abf19-138">Service web de notation est un service web classique</span><span class="sxs-lookup"><span data-stu-id="abf19-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="abf19-139">Si hello calcul du score du service web est un **service web classique**, créer hello deuxième **point de terminaison par défaut et mettre à jour** à l’aide de hello [portail Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="abf19-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="abf19-140">Pour connaître les étapes, consultez l’article [Créer des points de terminaison](../machine-learning/machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="abf19-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="abf19-141">Après avoir créé le point de terminaison actualisable hello non définis par défaut, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="abf19-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="abf19-142">Cliquez sur **l’exécution par lots** tooget hello URI valeur hello **mlEndpoint** propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="abf19-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="abf19-143">Cliquez sur **mise à jour de ressource** lier la valeur de l’URI tooget hello pour hello **updateResourceEndpoint** propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="abf19-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="abf19-144">clé d’API Hello est sur la page de point de terminaison hello lui-même (dans le coin inférieur droit de hello).</span><span class="sxs-lookup"><span data-stu-id="abf19-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![point de terminaison pouvant être mis à jour](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="abf19-146">Hello, l’exemple suivant fournit un exemple de définition JSON pour hello service AzureML lié.</span><span class="sxs-lookup"><span data-stu-id="abf19-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="abf19-147">Hello service lié utilise hello apiKey pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="abf19-147">hello linked service uses hello apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="abf19-148">Le service web de notification est un service web Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abf19-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="abf19-149">Si le service web de hello est hello nouveau type de service web qui expose un point de terminaison Azure Resource Manager, il est inutile tooadd hello deuxième **non définis par défaut** point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="abf19-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="abf19-150">Hello **updateResourceEndpoint** Bonjour service lié est hello format :</span><span class="sxs-lookup"><span data-stu-id="abf19-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="abf19-151">Vous pouvez obtenir des valeurs pour les espaces réservés dans les URL hello lors de l’interrogation du service web hello hello [portail de Services Web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="abf19-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="abf19-152">Hello nouveau type de point de terminaison de mise à jour de ressource requiert un jeton AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="abf19-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="abf19-153">Spécifiez **servicePrincipalId** et **servicePrincipalKey**dans le service lié AzureML.</span><span class="sxs-lookup"><span data-stu-id="abf19-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="abf19-154">Consultez [comment toocreate principal de service et assigner des autorisations toomanage ressource Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="abf19-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="abf19-155">Voici un exemple de définition de service lié AzureML :</span><span class="sxs-lookup"><span data-stu-id="abf19-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="abf19-156">Hello scénario suivant fournit plus de détails.</span><span class="sxs-lookup"><span data-stu-id="abf19-156">hello following scenario provides more details.</span></span> <span data-ttu-id="abf19-157">Il présente un exemple de reformation et de mise à jour de modèles Azure ML à partir d’un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abf19-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="abf19-158">Scénario : reformation et mise à jour d’un modèle Azure ML</span><span class="sxs-lookup"><span data-stu-id="abf19-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="abf19-159">Cette section fournit un exemple de pipeline qui utilise hello **l’activité d’exécution de lot Azure ML** tooretrain un modèle.</span><span class="sxs-lookup"><span data-stu-id="abf19-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="abf19-160">pipeline de Hello utilise également hello **de ressources de mise à jour Azure ML activité** modèle hello tooupdate hello calcul du score du service web.</span><span class="sxs-lookup"><span data-stu-id="abf19-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="abf19-161">Hello présente également des extraits de code JSON de tous les hello services liés, des datasets et pipeline dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="abf19-162">Voici une vue de diagramme hello du pipeline d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="abf19-163">Comme vous pouvez le voir, hello activité de l’exécution du lot Azure ML accepte l’entrée d’apprentissage hello et génère une sortie de formation (fichier iLearner).</span><span class="sxs-lookup"><span data-stu-id="abf19-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="abf19-164">Hello activité de ressources Azure ML mise à jour prend cette sortie de formation et mises à jour hello modèle Bonjour calcul du score du point de terminaison de service web.</span><span class="sxs-lookup"><span data-stu-id="abf19-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="abf19-165">Hello activité des ressources de mise à jour ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="abf19-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="abf19-166">Hello placeholderBlob est simplement un dataset de sortie factice est requis par le pipeline hello toorun hello Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="abf19-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![schéma du pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="abf19-168">Service lié Azure Blob Storage :</span><span class="sxs-lookup"><span data-stu-id="abf19-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="abf19-169">Bonjour Azure Storage conserve hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="abf19-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="abf19-170">Données de formation.</span><span class="sxs-lookup"><span data-stu-id="abf19-170">training data.</span></span> <span data-ttu-id="abf19-171">données d’entrée de salutation pour le service web de hello Azure ML d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="abf19-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="abf19-172">Fichier iLearner.</span><span class="sxs-lookup"><span data-stu-id="abf19-172">iLearner file.</span></span> <span data-ttu-id="abf19-173">Hello la sortie à partir du service web de hello Azure ML d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="abf19-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="abf19-174">Ce fichier est également hello, toohello d’entrée de ressources de mise à jour l’activité.</span><span class="sxs-lookup"><span data-stu-id="abf19-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="abf19-175">Voici hello exemple JSON de définition de service de hello lié :</span><span class="sxs-lookup"><span data-stu-id="abf19-175">Here is hello sample JSON definition of hello linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="abf19-176">Jeu de données d’entrée de formation</span><span class="sxs-lookup"><span data-stu-id="abf19-176">Training input dataset:</span></span>
<span data-ttu-id="abf19-177">Hello dataset suivant représente hello les données de formation d’entrée pour le service web de hello Azure ML d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="abf19-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="abf19-178">Hello activité d’exécution du lot Azure ML prend ce jeu de données comme entrée.</span><span class="sxs-lookup"><span data-stu-id="abf19-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "policy": {          
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

### <a name="training-output-dataset"></a><span data-ttu-id="abf19-179">Jeu de données de sortie de formation :</span><span class="sxs-lookup"><span data-stu-id="abf19-179">Training output dataset:</span></span>
<span data-ttu-id="abf19-180">Hello dataset suivant représente hello iLearner fichier de sortie à partir du service web de hello Azure ML d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="abf19-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="abf19-181">Hello d’activité de l’exécution du lot Azure ML génère ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="abf19-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="abf19-182">Ce jeu de données est également hello, toohello d’entrée de ressources de mise à jour Azure ML l’activité.</span><span class="sxs-lookup"><span data-stu-id="abf19-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="abf19-183">Service lié pour le point de terminaison de formation Azure ML</span><span class="sxs-lookup"><span data-stu-id="abf19-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="abf19-184">Hello suivant extrait de code JSON définit un service lié Azure Machine Learning qui pointe toohello point de terminaison par défaut du service web de formation hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="abf19-185">Dans **Azure ML Studio**, hello tooget valeurs suivantes pour **mlEndpoint** et **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="abf19-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="abf19-186">Cliquez sur **SERVICES WEB** sur le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="abf19-187">Cliquez sur hello **formation service web** dans la liste hello de services web.</span><span class="sxs-lookup"><span data-stu-id="abf19-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="abf19-188">Cliquez sur Copier ensuite trop**clé API** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="abf19-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="abf19-189">Collez la clé de hello dans le Presse-papiers de hello dans l’éditeur JSON de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="abf19-190">Bonjour **Azure ML studio**, cliquez sur **l’exécution par lots** lien.</span><span class="sxs-lookup"><span data-stu-id="abf19-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="abf19-191">Hello de copie **URI de requête** de hello **demande** section et collez-le dans l’éditeur JSON de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="abf19-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="abf19-192">Service lié pour le point de terminaison de notation pouvant être mis à jour Azure ML :</span><span class="sxs-lookup"><span data-stu-id="abf19-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="abf19-193">Hello suivant extrait de code JSON définit un service lié Azure Machine Learning qui pointe de point de terminaison toohello non définis par défaut être mise à jour de hello calcul du score du service web.</span><span class="sxs-lookup"><span data-stu-id="abf19-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="abf19-194">Jeu de données de sortie de l’espace réservé</span><span class="sxs-lookup"><span data-stu-id="abf19-194">Placeholder output dataset:</span></span>
<span data-ttu-id="abf19-195">Hello activité des ressources de mise à jour Azure ML ne génère pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="abf19-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="abf19-196">Toutefois, Azure Data Factory nécessite une planification de hello sortie dataset toodrive d’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="abf19-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="abf19-197">Par conséquent, nous utilisons dans cet exemple un jeu de données factice/paramètre fictif.</span><span class="sxs-lookup"><span data-stu-id="abf19-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="abf19-198">Pipeline</span><span class="sxs-lookup"><span data-stu-id="abf19-198">Pipeline</span></span>
<span data-ttu-id="abf19-199">pipeline de Hello a deux activités : **AzureMLBatchExecution** et **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="abf19-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="abf19-200">Hello activité d’exécution du lot Azure ML prend les données d’apprentissage hello comme entrée et produit un fichier iLearner comme sortie.</span><span class="sxs-lookup"><span data-stu-id="abf19-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="abf19-201">activité Hello appelle le service web de formation hello (expérience d’apprentissage exposé comme service web) avec une entrée hello données d’apprentissage et reçoit de fichier ilearner de hello de hello webservice.</span><span class="sxs-lookup"><span data-stu-id="abf19-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="abf19-202">Hello placeholderBlob est simplement un dataset de sortie factice est requis par le pipeline hello toorun hello Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="abf19-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![schéma du pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
