---
title: "Création de pipelines de données prédictifs avec Azure Data Factory | Microsoft Docs"
description: "Décrit comment créer des pipelines prédictifs à l’aide d’Azure Data Factory et d’Azure Machine Learning."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="4f11d-103">Création de pipelines prédictifs à l'aide d'Azure Data Factory et Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f11d-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4f11d-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="4f11d-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4f11d-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="4f11d-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4f11d-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="4f11d-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4f11d-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="4f11d-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4f11d-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="4f11d-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4f11d-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f11d-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4f11d-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f11d-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4f11d-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="4f11d-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4f11d-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4f11d-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4f11d-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="4f11d-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="4f11d-114">Introduction</span><span class="sxs-lookup"><span data-stu-id="4f11d-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="4f11d-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f11d-115">Azure Machine Learning</span></span>
<span data-ttu-id="4f11d-116">[AZURE MACHINE LEARNING](https://azure.microsoft.com/documentation/services/machine-learning/) vous permet de générer, tester et déployer des solutions d’analyse prédictive.</span><span class="sxs-lookup"><span data-stu-id="4f11d-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="4f11d-117">D’un point de vue très général, cela s’effectue en trois étapes :</span><span class="sxs-lookup"><span data-stu-id="4f11d-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="4f11d-118">**Créez une expérience de formation**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-118">**Create a training experiment**.</span></span> <span data-ttu-id="4f11d-119">Vous effectuez cette étape à l’aide d’Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="4f11d-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="4f11d-120">ML Studio est un environnement de développement visuel collaboratif qui vous permet de former et de tester un modèle d’analyse prédictive à l’aide de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="4f11d-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="4f11d-121">**Convertissez-la en une expérience prédictive**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="4f11d-122">Une fois que votre modèle a été formé avec des données existantes et que vous êtes prêt à l’utiliser pour la notation de nouvelles données, vous préparez et simplifiez votre expérience de notation.</span><span class="sxs-lookup"><span data-stu-id="4f11d-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="4f11d-123">**Déployez-la en tant que service web**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="4f11d-124">Vous pouvez publier votre expérience de notation comme un service web Azure.</span><span class="sxs-lookup"><span data-stu-id="4f11d-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="4f11d-125">Vous pouvez envoyer des données à votre modèle via ce point de terminaison de service web et recevoir des prédictions de résultats pour le modèle.</span><span class="sxs-lookup"><span data-stu-id="4f11d-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="4f11d-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4f11d-126">Azure Data Factory</span></span>
<span data-ttu-id="4f11d-127">Data Factory est un service d’intégration de données dans le cloud qui gère et automatise le **déplacement** et la **transformation** des données.</span><span class="sxs-lookup"><span data-stu-id="4f11d-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="4f11d-128">Vous pouvez créer des solutions d’intégration de données à l’aide du service Azure Data Factory, qui peut ingérer des données provenant de différentes banques de données, transformer/traiter les données et publier les données résultantes dans les banques de données.</span><span class="sxs-lookup"><span data-stu-id="4f11d-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="4f11d-129">Le service Data Factory vous permet de créer des pipelines de données qui déplacent et transforment les données, puis d’exécuter ces pipelines selon une planification spécifique (une fois par heure, par jour, par semaine, etc.).</span><span class="sxs-lookup"><span data-stu-id="4f11d-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="4f11d-130">Il fournit également des affichages élaborés pour visualiser le lignage et les dépendances entre vos pipelines de données, ainsi qu’une vue unifiée depuis laquelle vous pouvez surveiller l’ensemble de ces pipelines afin d’identifier les problèmes et de configurer des alertes d’analyse en toute simplicité.</span><span class="sxs-lookup"><span data-stu-id="4f11d-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="4f11d-131">Pour prendre en main le service Azure Data Factory rapidement, voir [Présentation d’Azure Data Factory](data-factory-introduction.md) et [Créer votre premier pipeline](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="4f11d-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="4f11d-132">Data Factory et Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f11d-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="4f11d-133">Azure Data Factory vous permet de créer facilement des pipelines qui utilisent un service web [Azure Machine Learning][azure-machine-learning] publié pour l’analyse prédictive.</span><span class="sxs-lookup"><span data-stu-id="4f11d-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="4f11d-134">À l’aide de l’ **activité d’exécution par lots** dans un pipeline Azure Data Factory, vous pouvez appeler un service web Azure ML pour effectuer des prédictions sur les données par lots.</span><span class="sxs-lookup"><span data-stu-id="4f11d-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="4f11d-135">Consultez la section [Appeler un service web Azure ML à l’aide de l’activité d’exécution par lots](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4f11d-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="4f11d-136">Au fil du temps, les modèles prédictifs dans les expériences de notation Azure ML doivent être reformés à l’aide de nouveaux jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4f11d-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="4f11d-137">Vous pouvez reformer un modèle Azure ML à partir d’un pipeline Data Factory en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f11d-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="4f11d-138">Publiez l’expérience de formation (et non l’expérience prédictive) comme un service web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="4f11d-139">Vous pouvez effectuer cette tâche dans Azure ML Studio comme vous l’avez fait pour exposer l’expérience prédictive en tant que service web dans le scénario précédent.</span><span class="sxs-lookup"><span data-stu-id="4f11d-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="4f11d-140">Utilisez l’activité d’exécution par lots Azure ML pour appeler le service web pour l’expérience de formation.</span><span class="sxs-lookup"><span data-stu-id="4f11d-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="4f11d-141">En fait, vous pouvez utiliser l’activité d’exécution par lots Azure ML pour appeler à la fois le service web de formation et le service web de notation.</span><span class="sxs-lookup"><span data-stu-id="4f11d-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="4f11d-142">Une fois que vous avez fini la reformation, mettez à jour le service web de notation (expérience prédictive exposée comme un service web) avec le modèle qui vient d’être formé à l’aide de l’**Activité des ressources de mise à jour Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="4f11d-143">Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4f11d-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="4f11d-144">Appeler un service web à l’aide de l’activité d’exécution par lots</span><span class="sxs-lookup"><span data-stu-id="4f11d-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="4f11d-145">Vous utilisez Azure Data Factory pour orchestrer le déplacement et le traitement des données, puis pour effectuer une exécution par lot à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4f11d-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="4f11d-146">Voici les étapes principales :</span><span class="sxs-lookup"><span data-stu-id="4f11d-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="4f11d-147">Créer un service lié Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4f11d-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="4f11d-148">Vous avez besoin des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f11d-148">You need the following values:</span></span>

   1. <span data-ttu-id="4f11d-149">**URI DE DEMANDE** pour l’API d’exécution de lot.</span><span class="sxs-lookup"><span data-stu-id="4f11d-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="4f11d-150">Pour trouver l’URI de demande, cliquez sur le lien **EXÉCUTION PAR LOT** dans la page des services web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="4f11d-151">**CLÉ API** pour le service web Azure Machine Learning publié.</span><span class="sxs-lookup"><span data-stu-id="4f11d-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="4f11d-152">Vous trouverez la clé API en cliquant sur le service web que vous avez publié.</span><span class="sxs-lookup"><span data-stu-id="4f11d-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="4f11d-153">L’activité **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="4f11d-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Tableau de bord Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI de lot](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="4f11d-156">Scénario : utilisation d’entrées/sorties de service web qui font référence à des données du stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="4f11d-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="4f11d-157">Dans ce scénario, le service web Azure Machine Learning effectue des prédictions à l’aide des données d’un fichier dans un stockage d’objets blob Azure et stocke les résultats des prédictions dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4f11d-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="4f11d-158">Le code JSON suivant définit un pipeline Data Factory avec une activité AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="4f11d-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="4f11d-159">L’activité a le jeu de données **DecisionTreeInputBlob** en tant qu’entrée, et le jeu de données **DecisionTreeResultBlob** en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="4f11d-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="4f11d-160">Le jeu de données **DecisionTreeInputBlob** est transmis en tant qu’entrée au service web à l’aide de la propriété JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="4f11d-161">Le jeu de données **DecisionTreeResultBlob** est transmis en tant que sortie au service web à l’aide de la propriété JSON **webServiceOuputs**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="4f11d-162">Si le service web prend plusieurs entrées, utilisez la propriété **webServiceInputs** au lieu de la propriété **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="4f11d-163">Consultez la section [Service web nécessitant plusieurs entrées](#web-service-requires-multiple-inputs) pour obtenir un exemple d’utilisation de la propriété webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="4f11d-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="4f11d-164">Les jeux de données référencés par les propriétés **webServiceInput**/**webServiceInputs** et **webServiceOutputs** (dans **typeProperties**) doivent également être inclus dans les **entrées** et **sorties** de l’activité.</span><span class="sxs-lookup"><span data-stu-id="4f11d-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="4f11d-165">Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser.</span><span class="sxs-lookup"><span data-stu-id="4f11d-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="4f11d-166">Les noms que vous utilisez pour les paramètres globalParameters, webServiceOutputs et webServiceInputs doivent correspondre exactement aux noms utilisés dans les expériences.</span><span class="sxs-lookup"><span data-stu-id="4f11d-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="4f11d-167">Vous pouvez afficher la charge utile de l’exemple de requête sur la page d’aide relative à l’exécution par lots pour votre point de terminaison Azure ML afin de vérifier le mappage attendu.</span><span class="sxs-lookup"><span data-stu-id="4f11d-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="4f11d-168">Seules les entrées et sorties de l’activité AzureMLBatchExecution peuvent être transmises en tant que paramètres au service web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="4f11d-169">Par exemple, dans l’extrait de code JSON ci-dessus, DecisionTreeInputBlob est une entrée de l’activité AzureMLBatchExecution, qui est transmise comme entrée au service web via le paramètre webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="4f11d-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="4f11d-170">Exemple</span><span class="sxs-lookup"><span data-stu-id="4f11d-170">Example</span></span>
<span data-ttu-id="4f11d-171">Cet exemple utilise Azure Storage pour stocker les données d'entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="4f11d-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="4f11d-172">Nous vous recommandons de suivre le didacticiel [Créer votre premier pipeline avec Data Factory][adf-build-1st-pipeline] avant de consulter cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4f11d-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="4f11d-173">Utilisez Data Factory Editor pour créer des artefacts Data Factory (services liés, jeux de données, pipeline) dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4f11d-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="4f11d-174">Créez un **service lié** pour votre service **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="4f11d-175">Si les fichiers d’entrée et de sortie se trouvent dans des comptes de stockage distincts, vous avez besoin de deux services liés.</span><span class="sxs-lookup"><span data-stu-id="4f11d-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="4f11d-176">Voici un exemple JSON :</span><span class="sxs-lookup"><span data-stu-id="4f11d-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="4f11d-177">Créez le **jeu de données** Azure Data Factory d’**entrée**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="4f11d-178">Contrairement à d’autres jeux de données Data Factory, ceux-ci doivent contenir les valeurs **folderPath** et **fileName**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="4f11d-179">Vous pouvez utiliser le partitionnement et provoquer l'exécution de chaque lot (chaque tranche de données) pour traiter ou produire des fichiers d'entrée et de sortie uniques.</span><span class="sxs-lookup"><span data-stu-id="4f11d-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="4f11d-180">Vous aurez peut-être besoin d’inclure une activité en amont pour convertir l’entrée au format de fichier CSV, et la placer dans le compte de stockage pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="4f11d-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="4f11d-181">Dans ce cas, n’incluez pas les paramètres **external** et **externalData** indiqués dans l’exemple suivant. Par ailleurs, DecisionTreeInputBlob représente le jeu de données de sortie d’une autre activité.</span><span class="sxs-lookup"><span data-stu-id="4f11d-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    <span data-ttu-id="4f11d-182">Votre fichier csv d’entrée doit disposer d’une ligne d’en-tête de colonnes.</span><span class="sxs-lookup"><span data-stu-id="4f11d-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="4f11d-183">Si vous utilisez **Copier l’activité** pour créer/déplacer le fichier .csv dans le stockage d’objets blob, vous devez définir la propriété du récepteur **blobWriterAddHeader** sur **true**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="4f11d-184">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4f11d-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="4f11d-185">Si le fichier csv ne dispose pas de ligne d'en-tête, l'erreur suivante risque de se produire : **Erreur pendant l'activité : erreur de lecture de la chaîne. Jeton inattendu : StartObject. Chemin d’accès ’’, ligne 1, position 1**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="4f11d-186">Créez le **jeu de données** Azure Data Factory de **sortie**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="4f11d-187">Cet exemple utilise le partitionnement pour créer un chemin de sortie unique à chaque exécution de tranche.</span><span class="sxs-lookup"><span data-stu-id="4f11d-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="4f11d-188">Sans partitionnement, l’activité remplace le fichier.</span><span class="sxs-lookup"><span data-stu-id="4f11d-188">Without the partitioning, the activity would overwrite the file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="4f11d-189">Créez un **service lié** de type **AzureMLLinkedService** en fournissant la clé API et l’URL d’exécution par lots du modèle.</span><span class="sxs-lookup"><span data-stu-id="4f11d-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="4f11d-190">Enfin, créez un pipeline contenant une activité **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="4f11d-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="4f11d-191">Au moment de l’exécution, le pipeline effectue les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f11d-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="4f11d-192">Obtient l’emplacement du fichier d’entrée à partir de vos jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4f11d-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="4f11d-193">Appelle l’API d’exécution par lot Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4f11d-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="4f11d-194">Copie la sortie de l’exécution par lot dans l’objet blob spécifié dans votre jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="4f11d-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4f11d-195">L’activité AzureMLBatchExecution peut avoir zéro ou plusieurs entrées et une ou plusieurs sorties.</span><span class="sxs-lookup"><span data-stu-id="4f11d-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="4f11d-196">Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="4f11d-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="4f11d-197">Par exemple : 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="4f11d-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="4f11d-198">L’heure de **fin** est facultative.</span><span class="sxs-lookup"><span data-stu-id="4f11d-198">The **end** time is optional.</span></span> <span data-ttu-id="4f11d-199">Si vous ne spécifiez aucune valeur pour la propriété **end**, cette dernière est calculée comme suit : « **start + 48 heures** ».</span><span class="sxs-lookup"><span data-stu-id="4f11d-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="4f11d-200">Pour exécuter le pipeline indéfiniment, spécifiez **9999-09-09** comme valeur pour la propriété **end**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="4f11d-201">Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4f11d-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4f11d-202">Définir une entrée pour l’activité AzureMLBatchExecution est facultatif.</span><span class="sxs-lookup"><span data-stu-id="4f11d-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="4f11d-203">Scénario : utilisation de modules lecteur/enregistreur pour faire référence à des données dans différents stockages</span><span class="sxs-lookup"><span data-stu-id="4f11d-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="4f11d-204">Un autre scénario courant pour créer des expériences Azure ML consiste à utiliser des modules lecteur et enregistreur.</span><span class="sxs-lookup"><span data-stu-id="4f11d-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="4f11d-205">Le module lecteur permet de charger des données dans une expérience, tandis que le module enregistreur sert à enregistrer les données issues de cette expérience.</span><span class="sxs-lookup"><span data-stu-id="4f11d-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="4f11d-206">Pour plus d’informations sur les modules lecteur et enregistreur, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN.</span><span class="sxs-lookup"><span data-stu-id="4f11d-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="4f11d-207">Quand vous utilisez les modules lecteur et enregistreur, nous vous recommandons de recourir à un paramètre de service web pour chaque propriété de ces modules.</span><span class="sxs-lookup"><span data-stu-id="4f11d-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="4f11d-208">Ces paramètres web permettent de configurer les valeurs pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4f11d-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="4f11d-209">Par exemple, vous pouvez créer une expérience avec un module lecteur qui utilise une base de données Azure SQL Database : XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="4f11d-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="4f11d-210">Une fois le service web déployé, vous pouvez autoriser les consommateurs du service web à spécifier un autre serveur Azure SQL Server appelé YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="4f11d-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="4f11d-211">Vous pouvez utiliser un paramètre de service web pour permettre à cette valeur d’être configurée.</span><span class="sxs-lookup"><span data-stu-id="4f11d-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="4f11d-212">L’entrée et la sortie du service web diffèrent des paramètres de service web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="4f11d-213">Dans le premier scénario, vous avez vu comment une entrée et une sortie peuvent être spécifiées pour un service web Azure ML.</span><span class="sxs-lookup"><span data-stu-id="4f11d-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="4f11d-214">Dans ce scénario, vous passez pour un service web des paramètres qui correspondent aux propriétés des modules lecteur/enregistreur.</span><span class="sxs-lookup"><span data-stu-id="4f11d-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="4f11d-215">Examinons un scénario d’utilisation de paramètres de service web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="4f11d-216">Vous disposez d’un service web Azure Machine Learning déployé qui utilise un module lecteur pour lire les données de l’une des sources de données prises en charge par Azure Machine Learning (par exemple : Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="4f11d-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="4f11d-217">Après l’exécution par lots, les résultats sont écrits à l’aide d’un module enregistreur (Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="4f11d-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="4f11d-218">Aucune entrée ou sortie de service web n’est définie dans les expériences.</span><span class="sxs-lookup"><span data-stu-id="4f11d-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="4f11d-219">Dans ce cas, nous vous recommandons de configurer les paramètres de service web appropriés pour les modules lecteur et enregistreur.</span><span class="sxs-lookup"><span data-stu-id="4f11d-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="4f11d-220">Cela permet la configuration des modules lecteur/enregistreur quand vous utilisez l’activité AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="4f11d-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="4f11d-221">Spécifiez les paramètres de service web dans la section **globalParameters** du code JSON de l’activité comme suit.</span><span class="sxs-lookup"><span data-stu-id="4f11d-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="4f11d-222">Vous pouvez également utiliser les [fonctions de Data Factory](data-factory-functions-variables.md) pour transmettre les valeurs aux paramètres de service web, comme indiqué dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4f11d-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="4f11d-223">Les paramètres de service web respectent la casse ; veillez donc à ce que les noms que vous indiquez dans le script JSON de l'activité correspondent à ceux exposés par le service web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="4f11d-224">Utilisation d’un module lecteur pour lire les données de plusieurs fichiers dans le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="4f11d-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="4f11d-225">Les pipelines Big Data avec des activités telles que Pig et Hive peuvent produire un ou plusieurs fichiers de sortie sans extensions.</span><span class="sxs-lookup"><span data-stu-id="4f11d-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="4f11d-226">Par exemple, quand vous spécifiez une table Hive externe, les données de cette table peuvent être stockées dans le stockage d’objets blob Azure avec le nom 000000_0 suivant.</span><span class="sxs-lookup"><span data-stu-id="4f11d-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="4f11d-227">Vous pouvez utiliser le module lecteur dans une expérience pour lire plusieurs fichiers et les utiliser pour les prédictions.</span><span class="sxs-lookup"><span data-stu-id="4f11d-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="4f11d-228">Quand vous utilisez le module lecteur dans une expérience Azure Machine Learning, vous pouvez spécifier un objet blob Azure comme entrée.</span><span class="sxs-lookup"><span data-stu-id="4f11d-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="4f11d-229">Les fichiers du stockage d’objets blob Azure peuvent être les fichiers de sortie (par exemple, 000000_0) qui sont générés par un script Pig et Hive exécuté sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f11d-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="4f11d-230">Le module lecteur vous permet de lire des fichiers (sans extension) en configurant le **chemin d’accès au conteneur et le répertoire/l’objet blob**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="4f11d-231">Le **chemin d’accès au conteneur** pointe vers le conteneur et le **répertoire/objet blob** pointe vers le dossier qui contient les fichiers, comme illustré dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="4f11d-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="4f11d-232">L’astérisque \*) **spécifie que tous les fichiers du conteneur/dossier (c’est-à-dire, data/aggregateddata/year=2014/month-6/*\*)** sont lus dans le cadre de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="4f11d-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Propriétés des objets blob Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="4f11d-234">Exemple</span><span class="sxs-lookup"><span data-stu-id="4f11d-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="4f11d-235">Pipeline avec l’activité AzureMLBatchExecution avec les paramètres de service web</span><span class="sxs-lookup"><span data-stu-id="4f11d-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="4f11d-236">Dans l'exemple JSON ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="4f11d-236">In the above JSON example:</span></span>

* <span data-ttu-id="4f11d-237">Le service web Azure Machine Learning déployé utilise un module lecteur et un module enregistreur pour lire/écrire des données depuis/vers une base de données Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4f11d-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="4f11d-238">Ce service web expose les quatre paramètres suivants : Database server name, Database name, Server user account name et Server user account password.</span><span class="sxs-lookup"><span data-stu-id="4f11d-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="4f11d-239">Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="4f11d-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="4f11d-240">Par exemple : 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="4f11d-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="4f11d-241">L’heure de **fin** est facultative.</span><span class="sxs-lookup"><span data-stu-id="4f11d-241">The **end** time is optional.</span></span> <span data-ttu-id="4f11d-242">Si vous ne spécifiez aucune valeur pour la propriété **end**, cette dernière est calculée comme suit : « **start + 48 heures** ».</span><span class="sxs-lookup"><span data-stu-id="4f11d-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="4f11d-243">Pour exécuter le pipeline indéfiniment, spécifiez **9999-09-09** comme valeur pour la propriété **end**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="4f11d-244">Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4f11d-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="4f11d-245">Autres scénarios</span><span class="sxs-lookup"><span data-stu-id="4f11d-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="4f11d-246">Service web nécessitant plusieurs entrées</span><span class="sxs-lookup"><span data-stu-id="4f11d-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="4f11d-247">Si le service web prend plusieurs entrées, utilisez la propriété **webServiceInputs** au lieu de la propriété **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="4f11d-248">Les jeux de données référencés par **webServiceInputs** doivent également être inclus dans les **entrées** de l’activité.</span><span class="sxs-lookup"><span data-stu-id="4f11d-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="4f11d-249">Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser.</span><span class="sxs-lookup"><span data-stu-id="4f11d-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="4f11d-250">Les noms que vous utilisez pour les paramètres globalParameters, webServiceOutputs et webServiceInputs doivent correspondre exactement aux noms utilisés dans les expériences.</span><span class="sxs-lookup"><span data-stu-id="4f11d-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="4f11d-251">Vous pouvez afficher la charge utile de l’exemple de requête sur la page d’aide relative à l’exécution par lots pour votre point de terminaison Azure ML afin de vérifier le mappage attendu.</span><span class="sxs-lookup"><span data-stu-id="4f11d-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="4f11d-252">Le service web ne nécessite pas d’entrée</span><span class="sxs-lookup"><span data-stu-id="4f11d-252">Web Service does not require an input</span></span>
<span data-ttu-id="4f11d-253">Les services web d’exécution par lot Azure ML peuvent servir à exécuter n’importe quel flux de travail (par exemple des scripts R ou Python) qui ne nécessite pas d’entrées.</span><span class="sxs-lookup"><span data-stu-id="4f11d-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="4f11d-254">Ou bien, l’expérience peut être configurée avec un module Lecteur qui n’expose pas de paramètres GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="4f11d-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="4f11d-255">Dans ce cas, l’activité AzureMLBatchExecution doit être configurée comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f11d-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="4f11d-256">Le service web ne nécessite pas d’entrée/sortie</span><span class="sxs-lookup"><span data-stu-id="4f11d-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="4f11d-257">Il se peut qu’aucune sortie de service web ne soit configurée pour le service web d’exécution par lot Azure ML.</span><span class="sxs-lookup"><span data-stu-id="4f11d-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="4f11d-258">Dans cet exemple, aucune entrée ou sortie ni aucun paramètre GlobalParameters n’est configuré.</span><span class="sxs-lookup"><span data-stu-id="4f11d-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="4f11d-259">Il existe toujours une sortie configurée sur l’activité elle-même, mais elle n’est pas donnée comme sortie webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="4f11d-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="4f11d-260">Le service web utilise des lecteurs et enregistreurs et l’activité s’exécute uniquement lorsque d’autres activités ont réussi</span><span class="sxs-lookup"><span data-stu-id="4f11d-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="4f11d-261">Les modules de lecteur et d’enregistreur du service web Azure ML peuvent être configurés pour s’exécuter avec ou sans paramètres GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="4f11d-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="4f11d-262">Toutefois, il peut être utile d’incorporer les appels de service dans un pipeline qui utilise des dépendances de jeux de données, afin d’appeler le service uniquement lorsqu’un traitement en amont est terminé.</span><span class="sxs-lookup"><span data-stu-id="4f11d-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="4f11d-263">Cette approche vous permet également de déclencher d’autres actions une fois l’exécution par lot terminée.</span><span class="sxs-lookup"><span data-stu-id="4f11d-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="4f11d-264">Dans ce cas, vous pouvez exprimer les dépendances à l’aide d’entrées et de sorties d’activité, sans les nommer en tant qu’entrées ou sorties de service web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="4f11d-265">Les **points importants** sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4f11d-265">The **takeaways** are:</span></span>

* <span data-ttu-id="4f11d-266">Si le point de terminaison de votre expérience utilise un élément webServiceInput, il est représenté par un jeu de données d’objets blob et il est inclus dans les entrées de l’activité, ainsi que dans la propriété webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="4f11d-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="4f11d-267">Sinon, la propriété webServiceInput est omise.</span><span class="sxs-lookup"><span data-stu-id="4f11d-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="4f11d-268">Si le point de terminaison de votre expérience utilise des éléments webServiceOutput, ils sont représentés par des jeux de données d’objets blob et sont inclus dans les sorties de l’activité, ainsi que dans la propriété webServiceOutputs.</span><span class="sxs-lookup"><span data-stu-id="4f11d-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="4f11d-269">Les sorties de l’activité et les éléments webServiceOutputs sont mappés par le nom de chaque sortie de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="4f11d-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="4f11d-270">Sinon, la propriété webServiceOutputs est omise.</span><span class="sxs-lookup"><span data-stu-id="4f11d-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="4f11d-271">Si le point de terminaison de votre expérience expose des éléments globalParameters, ceux-ci figurent dans la propriété globalParameters de l’activité sous forme de paires clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="4f11d-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="4f11d-272">Sinon, la propriété globalParameters est omise.</span><span class="sxs-lookup"><span data-stu-id="4f11d-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="4f11d-273">Les clés sont sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="4f11d-273">The keys are case-sensitive.</span></span> <span data-ttu-id="4f11d-274">[fonctions Azure Data Factory](data-factory-functions-variables.md) peuvent être utilisées dans les valeurs.</span><span class="sxs-lookup"><span data-stu-id="4f11d-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="4f11d-275">Des jeux de données supplémentaires peuvent être inclus dans les propriétés d’entrée et de sortie de l’activité, sans être référencés dans l’activité typeProperties.</span><span class="sxs-lookup"><span data-stu-id="4f11d-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="4f11d-276">Ces jeux de données contrôlent l’exécution à l’aide de dépendances entre les tranches. Sinon, ils sont ignorés par l’activité AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="4f11d-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="4f11d-277">Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour</span><span class="sxs-lookup"><span data-stu-id="4f11d-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="4f11d-278">Une fois que vous avez fini la reformation, mettez à jour le service web de notation (expérience prédictive exposée comme un service web) avec le modèle qui vient d’être formé à l’aide de l’**Activité des ressources de mise à jour Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="4f11d-279">Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4f11d-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="4f11d-280">Modules Lecteur et Enregistreur</span><span class="sxs-lookup"><span data-stu-id="4f11d-280">Reader and Writer Modules</span></span>
<span data-ttu-id="4f11d-281">L'utilisation des paramètres de service web passe par un scénario commun : l'utilisation des lecteurs et enregistreurs SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4f11d-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="4f11d-282">Le module lecteur est utilisé pour charger des données dans une expérience à partir des services de gestion des données en dehors d’Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4f11d-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="4f11d-283">Le module enregistreur est utilisé pour enregistrer les données de vos expériences dans les services de gestion des données en dehors d’Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4f11d-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="4f11d-284">Pour plus d’informations sur les modules enregistreur/lecteur Azure Blob/SQL Azure, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN.</span><span class="sxs-lookup"><span data-stu-id="4f11d-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="4f11d-285">L'exemple de la section précédente utilisait le lecteur et l'enregistreur d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4f11d-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="4f11d-286">Cette section décrit leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="4f11d-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="4f11d-287">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="4f11d-287">Frequently asked questions</span></span>
<span data-ttu-id="4f11d-288">**Q :** J’ai plusieurs fichiers qui sont générés par mes pipelines Big Data.</span><span class="sxs-lookup"><span data-stu-id="4f11d-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="4f11d-289">L’activité AzureMLBatchExecution peut-elle fonctionner sur tous les fichiers ?</span><span class="sxs-lookup"><span data-stu-id="4f11d-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="4f11d-290">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="4f11d-290">**A:** Yes.</span></span> <span data-ttu-id="4f11d-291">Pour plus d’informations, consultez la section **Utilisation d’un module lecteur pour lire les données de plusieurs fichiers dans le stockage d’objets blob Azure** .</span><span class="sxs-lookup"><span data-stu-id="4f11d-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="4f11d-292">Activité de notation par lots Azure ML</span><span class="sxs-lookup"><span data-stu-id="4f11d-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="4f11d-293">Si vous utilisez l’activité **AzureMLBatchScoring** en vue d’une intégration avec Azure Machine Learning, nous vous recommandons d’utiliser la dernière activité **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="4f11d-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="4f11d-294">L’activité AzureMLBatchExecution est introduite dans la version d’août 2015 du Kit de développement logiciel (SDK) Azure et d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f11d-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="4f11d-295">Si vous souhaitez continuer à utiliser l’activité AzureMLBatchScoring, poursuivez la lecture de cette section.</span><span class="sxs-lookup"><span data-stu-id="4f11d-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="4f11d-296">Activité de notation par lots Azure ML utilisant Azure Storage pour l’entrée/la sortie</span><span class="sxs-lookup"><span data-stu-id="4f11d-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="4f11d-297">Paramètres de service web</span><span class="sxs-lookup"><span data-stu-id="4f11d-297">Web Service Parameters</span></span>
<span data-ttu-id="4f11d-298">Pour spécifier les valeurs des paramètres de service web, ajoutez une section **typeProperties** à la section **AzureMLBatchScoringActivty** dans le script JSON du pipeline, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4f11d-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="4f11d-299">Vous pouvez également utiliser les [fonctions de Data Factory](data-factory-functions-variables.md) pour transmettre les valeurs aux paramètres de service web, comme indiqué dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4f11d-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="4f11d-300">Les paramètres de service web respectent la casse ; veillez donc à ce que les noms que vous indiquez dans le script JSON de l'activité correspondent à ceux exposés par le service web.</span><span class="sxs-lookup"><span data-stu-id="4f11d-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="4f11d-301">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4f11d-301">See Also</span></span>
* [<span data-ttu-id="4f11d-302">Article de blog Azure : prise en main d’Azure Data Factory et d’Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f11d-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
