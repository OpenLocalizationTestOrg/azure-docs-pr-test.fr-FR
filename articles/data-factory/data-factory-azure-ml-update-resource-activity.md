---
title: "Mise à jour des modèles Machine Learning à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Décrit comment créer des pipelines prédictifs à l’aide d’Azure Data Factory et d’Azure Machine Learning."
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
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="79494-103">Mettre à jour les modèles Azure Machine Learning à l’aide de l’activité des ressources de mise à jour</span><span class="sxs-lookup"><span data-stu-id="79494-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="79494-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="79494-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="79494-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="79494-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="79494-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="79494-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="79494-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="79494-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="79494-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="79494-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="79494-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="79494-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="79494-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="79494-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="79494-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="79494-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="79494-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="79494-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="79494-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="79494-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="79494-114">Cet article vient s’ajouter à l’article principal sur l’intégration Azure Data Factory - Azure Machine Learning : [Création de pipelines prédictifs à l'aide d'Azure Data Factory et Azure Machine Learning](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="79494-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="79494-115">Si vous ne l’avez pas encore fait, consultez l’article principal avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="79494-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="79494-116">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="79494-116">Overview</span></span>
<span data-ttu-id="79494-117">Au fil du temps, les modèles prédictifs dans les expériences de notation Azure ML doivent être reformés à l’aide de nouveaux jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="79494-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="79494-118">Une fois que vous avez fini la reformation, vous souhaitez mettre à jour le service web de notation avec le modèle ML reformé.</span><span class="sxs-lookup"><span data-stu-id="79494-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="79494-119">Les étapes classiques pour activer la reformation et la mise à jour des modèles Azure ML via les services web sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="79494-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="79494-120">Créez une expérience dans [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="79494-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="79494-121">Lorsque vous êtes satisfait du modèle, utilisez Azure ML Studio pour publier des services web à la fois pour l’**expérience de formation** et l’expérience de notation/**prédictive**.</span><span class="sxs-lookup"><span data-stu-id="79494-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="79494-122">Le tableau suivant décrit les services web utilisés dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="79494-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="79494-123">Pour plus d’informations, consultez [Reformation des modèles Machine Learning par programme](../machine-learning/machine-learning-retrain-models-programmatically.md) .</span><span class="sxs-lookup"><span data-stu-id="79494-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="79494-124">**Service Web de formation** - Reçoit les données d’apprentissage et produit les modèles formés.</span><span class="sxs-lookup"><span data-stu-id="79494-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="79494-125">La sortie de la reformation est un fichier .ilearner dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="79494-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="79494-126">Le **point de terminaison par défaut** est automatiquement créé pour vous lorsque vous publiez l’expérience de formation en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="79494-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="79494-127">Vous pouvez créer d’autres points de terminaison, mais l’exemple utilise uniquement le point de terminaison par défaut.</span><span class="sxs-lookup"><span data-stu-id="79494-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="79494-128">**Service Web de notation** - Reçoit des exemples de données sans étiquette et effectue des prédictions.</span><span class="sxs-lookup"><span data-stu-id="79494-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="79494-129">La sortie de la prédiction peut prendre plusieurs formes, comme un fichier .csv ou des lignes dans une base de données SQL Azure, selon la configuration de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="79494-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="79494-130">Le point de terminaison par défaut est automatiquement créé pour vous lorsque vous publiez l’expérience prédictive comme un service web.</span><span class="sxs-lookup"><span data-stu-id="79494-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="79494-131">Le schéma suivant illustre la relation entre points de terminaison de formation et de notation dans Azure ML.</span><span class="sxs-lookup"><span data-stu-id="79494-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVICES WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="79494-133">Vous pouvez appeler le **training web service** à l’aide du **activité d’exécution par lot Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="79494-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="79494-134">L’appel d’un service web de formation est similaire à l’appel d’un service web Azure ML (service web de notation) pour les données de notation.</span><span class="sxs-lookup"><span data-stu-id="79494-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="79494-135">Les sections précédentes expliquent de manière détaillée comment appeler un service web Azure ML à partir d’un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79494-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="79494-136">Vous pouvez appeler le **scoring web service** à l’aide du **activité des ressources de mise à jour Azure ML** pour mettre à jour le service web avec le modèle qui vient d’être formé.</span><span class="sxs-lookup"><span data-stu-id="79494-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="79494-137">Les exemples suivants fournissent les définitions de service associé :</span><span class="sxs-lookup"><span data-stu-id="79494-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="79494-138">Service web de notation est un service web classique</span><span class="sxs-lookup"><span data-stu-id="79494-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="79494-139">Si le service web de notation est un **service classique web**, créez le deuxième **point de terminaison (qui n’est pas le point de terminaison par défaut) pouvant être mis à jour** à l’aide du [portail Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="79494-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="79494-140">Pour connaître les étapes, consultez l’article [Créer des points de terminaison](../machine-learning/machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="79494-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="79494-141">Après avoir créé le point de terminaison non par défaut pouvant être mis à jour, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79494-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="79494-142">Cliquez sur **EXÉCUTION PAR LOT** pour obtenir la valeur d’URI pour la propriété JSON **mlEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="79494-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="79494-143">Cliquez sur le lien **RESSOURCE DE MISE À JOUR** pour obtenir la valeur d’URI pour la propriété JSON **updateResourceEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="79494-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="79494-144">La clé API est sur la page du point de terminaison même (dans le coin inférieur droit).</span><span class="sxs-lookup"><span data-stu-id="79494-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![point de terminaison pouvant être mis à jour](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="79494-146">L’exemple suivant présente un exemple de définition JSON pour le service lié AzureML.</span><span class="sxs-lookup"><span data-stu-id="79494-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="79494-147">Le service lié utilise apiKey pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="79494-147">The linked service uses the apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="79494-148">Le service web de notification est un service web Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="79494-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="79494-149">Si le service web est un nouveau type de service web qui expose un point de terminaison Azure Resource Manager, vous n’avez pas besoin ajouter le second point de terminaison, **qui n’est pas celui par défaut** .</span><span class="sxs-lookup"><span data-stu-id="79494-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="79494-150">Le **updateResourceEndpoint** du service lié est au format :</span><span class="sxs-lookup"><span data-stu-id="79494-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="79494-151">Vous pouvez obtenir des valeurs pour les espaces réservés dans l’URL lors de l’interrogation du service web sur le [portail des services web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="79494-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="79494-152">Le nouveau type de point de terminaison de ressource de mise à jour requiert un jeton AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="79494-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="79494-153">Spécifiez **servicePrincipalId** et **servicePrincipalKey**dans le service lié AzureML.</span><span class="sxs-lookup"><span data-stu-id="79494-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="79494-154">Consultez [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md) (comment créer le principal de service et affecter des autorisations de gestion de ressources Azure).</span><span class="sxs-lookup"><span data-stu-id="79494-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="79494-155">Voici un exemple de définition de service lié AzureML :</span><span class="sxs-lookup"><span data-stu-id="79494-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
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

<span data-ttu-id="79494-156">Le scénario suivant fournit plus de détails.</span><span class="sxs-lookup"><span data-stu-id="79494-156">The following scenario provides more details.</span></span> <span data-ttu-id="79494-157">Il présente un exemple de reformation et de mise à jour de modèles Azure ML à partir d’un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79494-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="79494-158">Scénario : reformation et mise à jour d’un modèle Azure ML</span><span class="sxs-lookup"><span data-stu-id="79494-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="79494-159">Cette section fournit un exemple de pipeline qui utilise **l’activité d’exécution par lot Azure ML** pour reformer un modèle.</span><span class="sxs-lookup"><span data-stu-id="79494-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="79494-160">Le pipeline utilise également **l’activité des ressources de mise à jour Azure ML** pour mettre à jour le modèle dans le service web de notation.</span><span class="sxs-lookup"><span data-stu-id="79494-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="79494-161">La section fournit également des extraits de code JSON pour tous les services liés, jeux de données et éléments de pipeline dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="79494-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="79494-162">Voici la vue schématique de l’exemple de pipeline.</span><span class="sxs-lookup"><span data-stu-id="79494-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="79494-163">Comme vous pouvez le voir, l’activité d’exécution par lot Azure ML prend l’entrée de formation et génère une sortie de formation (fichier iLearner).</span><span class="sxs-lookup"><span data-stu-id="79494-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="79494-164">L’activité des ressources de mise à jour Azure ML prend cette sortie de formation et met à jour le modèle dans le point de terminaison de service web de notation.</span><span class="sxs-lookup"><span data-stu-id="79494-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="79494-165">L’activité des ressources de mise à jour ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="79494-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="79494-166">placeholderBlob est simplement un jeu de données de sortie factice requis par le service Azure Data Factory pour exécuter le pipeline.</span><span class="sxs-lookup"><span data-stu-id="79494-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![schéma du pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="79494-168">Service lié Azure Blob Storage :</span><span class="sxs-lookup"><span data-stu-id="79494-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="79494-169">Azure Storage contient les données suivantes :</span><span class="sxs-lookup"><span data-stu-id="79494-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="79494-170">Données de formation.</span><span class="sxs-lookup"><span data-stu-id="79494-170">training data.</span></span> <span data-ttu-id="79494-171">Les données d’entrée pour le service web de formation Azure ML.</span><span class="sxs-lookup"><span data-stu-id="79494-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="79494-172">Fichier iLearner.</span><span class="sxs-lookup"><span data-stu-id="79494-172">iLearner file.</span></span> <span data-ttu-id="79494-173">La sortie du service web de formation Azure ML.</span><span class="sxs-lookup"><span data-stu-id="79494-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="79494-174">Ce fichier est également l’entrée de l’activité des ressources de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="79494-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="79494-175">Voici la définition d’exemple JSON du service lié :</span><span class="sxs-lookup"><span data-stu-id="79494-175">Here is the sample JSON definition of the linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="79494-176">Jeu de données d’entrée de formation</span><span class="sxs-lookup"><span data-stu-id="79494-176">Training input dataset:</span></span>
<span data-ttu-id="79494-177">Le jeu de données suivant représente les données de formation d’entrée pour le service web de formation Azure ML.</span><span class="sxs-lookup"><span data-stu-id="79494-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="79494-178">L’activité d’exécution par lots Azure ML prend ce jeu de données comme entrée.</span><span class="sxs-lookup"><span data-stu-id="79494-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="79494-179">Jeu de données de sortie de formation :</span><span class="sxs-lookup"><span data-stu-id="79494-179">Training output dataset:</span></span>
<span data-ttu-id="79494-180">Le jeu de données suivant représente le fichier iLearner de sortie issu du service web de formation Azure ML.</span><span class="sxs-lookup"><span data-stu-id="79494-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="79494-181">L’activité d’exécution par lots Azure ML génère ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="79494-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="79494-182">Ce jeu de données est également l’entrée de l’activité des ressources de mise à jour Azure ML.</span><span class="sxs-lookup"><span data-stu-id="79494-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="79494-183">Service lié pour le point de terminaison de formation Azure ML</span><span class="sxs-lookup"><span data-stu-id="79494-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="79494-184">L’extrait de code JSON suivant définit un service lié Azure Machine Learning qui pointe vers le point de terminaison par défaut du service web de formation.</span><span class="sxs-lookup"><span data-stu-id="79494-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

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

<span data-ttu-id="79494-185">Dans **Azure ML Studio**, procédez comme suit pour obtenir les valeurs pour **mlEndpoint** et **apiKey** :</span><span class="sxs-lookup"><span data-stu-id="79494-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="79494-186">Cliquez sur **SERVICES WEB** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="79494-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="79494-187">Cliquez sur le **service web de formation** dans la liste des services web.</span><span class="sxs-lookup"><span data-stu-id="79494-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="79494-188">Cliquez sur Copier regard de la zone de texte **Clé API** .</span><span class="sxs-lookup"><span data-stu-id="79494-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="79494-189">Collez la clé copiée dans l’éditeur JSON Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79494-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="79494-190">Dans le **studio Azure ML**, cliquez sur le lien **EXÉCUTION PAR LOT**.</span><span class="sxs-lookup"><span data-stu-id="79494-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="79494-191">Copiez l’**URI de demande** à partir de la section **Demande**, et collez-le dans l’éditeur JSON Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79494-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="79494-192">Service lié pour le point de terminaison de notation pouvant être mis à jour Azure ML :</span><span class="sxs-lookup"><span data-stu-id="79494-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="79494-193">L’extrait de code JSON suivant définit un service lié Azure Machine Learning qui pointe vers le point de terminaison autre que par défaut pouvant être mis à jour du service web de notation.</span><span class="sxs-lookup"><span data-stu-id="79494-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="79494-194">Jeu de données de sortie de l’espace réservé</span><span class="sxs-lookup"><span data-stu-id="79494-194">Placeholder output dataset:</span></span>
<span data-ttu-id="79494-195">L’activité des ressources de mise à jour Azure ML ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="79494-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="79494-196">Toutefois, Azure Data Factory requiert un jeu de données de sortie pour que la planification d’un pipeline fonctionne.</span><span class="sxs-lookup"><span data-stu-id="79494-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="79494-197">Par conséquent, nous utilisons dans cet exemple un jeu de données factice/paramètre fictif.</span><span class="sxs-lookup"><span data-stu-id="79494-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="79494-198">Pipeline</span><span class="sxs-lookup"><span data-stu-id="79494-198">Pipeline</span></span>
<span data-ttu-id="79494-199">Le pipeline a deux activités : **AzureMLBatchExecution** et **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="79494-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="79494-200">L’activité d’exécution par lot Azure ML prend les données d’apprentissage comme entrée et génère un fichier .iLearner comme sortie.</span><span class="sxs-lookup"><span data-stu-id="79494-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="79494-201">L’activité appelle le service web de formation (expérience de formation exposée comme un service web) avec les données de formation d’entrée et reçoit le fichier iLearner du service web.</span><span class="sxs-lookup"><span data-stu-id="79494-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="79494-202">placeholderBlob est simplement un jeu de données de sortie factice requis par le service Azure Data Factory pour exécuter le pipeline.</span><span class="sxs-lookup"><span data-stu-id="79494-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

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
