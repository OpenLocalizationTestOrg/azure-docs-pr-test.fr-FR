---
title: "les pipelines de données prédictives aaaCreate à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Décrit comment toocreate créer des pipelines PRÉDICTIFS à l’aide d’Azure Data Factory et Azure Machine Learning"
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
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="1cb84-103">Création de pipelines prédictifs à l'aide d'Azure Data Factory et Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1cb84-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1cb84-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="1cb84-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1cb84-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="1cb84-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1cb84-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="1cb84-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1cb84-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="1cb84-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1cb84-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="1cb84-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1cb84-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1cb84-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1cb84-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1cb84-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1cb84-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="1cb84-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1cb84-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1cb84-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1cb84-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="1cb84-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="1cb84-114">Introduction</span><span class="sxs-lookup"><span data-stu-id="1cb84-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="1cb84-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1cb84-115">Azure Machine Learning</span></span>
<span data-ttu-id="1cb84-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) Active toobuild, tester et déployer des solutions d’analytique prédictive.</span><span class="sxs-lookup"><span data-stu-id="1cb84-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="1cb84-117">D’un point de vue très général, cela s’effectue en trois étapes :</span><span class="sxs-lookup"><span data-stu-id="1cb84-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="1cb84-118">**Créez une expérience de formation**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-118">**Create a training experiment**.</span></span> <span data-ttu-id="1cb84-119">Vous effectuez cette étape à l’aide de hello Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="1cb84-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="1cb84-120">ML studio de Hello est un environnement collaboratif de développement visuel que vous utilisez tootrain et testez d’un modèle prédictif analytique à l’aide des données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="1cb84-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="1cb84-121">**Convertir les expérience prédictive tooa**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="1cb84-122">Une fois que votre modèle a été formé avec des données existantes et que vous êtes prêt toouse il tooscore de nouvelles données, préparer et de simplifier votre expérience pour calculer les scores.</span><span class="sxs-lookup"><span data-stu-id="1cb84-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="1cb84-123">**Déployez-la en tant que service web**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="1cb84-124">Vous pouvez publier votre expérience de notation comme un service web Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb84-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="1cb84-125">Vous pouvez envoyer le modèle de tooyour des données via ce point de terminaison de service web et recevoir des prédictions de résultat de modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="1cb84-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1cb84-126">Azure Data Factory</span></span>
<span data-ttu-id="1cb84-127">Fabrique de données est un service d’intégration de données basés sur le cloud qui orchestre et automatise hello **mouvement** et **transformation** de données.</span><span class="sxs-lookup"><span data-stu-id="1cb84-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="1cb84-128">Vous pouvez créer des solutions d’intégration données à l’aide d’Azure Data Factory réception des données à partir de différentes banques de données, / processus de transformation des données de hello, et publier des données de résultats hello toohello des magasins de données.</span><span class="sxs-lookup"><span data-stu-id="1cb84-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="1cb84-129">Service de fabrique de données vous permet des pipelines de données toocreate déplacent et transforment des données et puis exécutez les pipelines hello selon un calendrier défini (horaire, quotidienne, hebdomadaire, etc.).</span><span class="sxs-lookup"><span data-stu-id="1cb84-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="1cb84-130">Il fournit également lignage de visualisation enrichie toodisplay hello et les dépendances entre vos pipelines de données et surveiller vos pipelines de données à partir d’une vue unifiée unique tooeasily localiser les problèmes et configurer des alertes d’analyse.</span><span class="sxs-lookup"><span data-stu-id="1cb84-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="1cb84-131">Consultez [Introduction tooAzure Data Factory](data-factory-introduction.md) et [générer votre première pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly prise en main hello service Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1cb84-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="1cb84-132">Data Factory et Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1cb84-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="1cb84-133">Azure permet de Data Factory tooeasily vous créer des pipelines qui utilisent un rapport publié [Azure Machine Learning] [ azure-machine-learning] web service pour l’analytique prédictive.</span><span class="sxs-lookup"><span data-stu-id="1cb84-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="1cb84-134">À l’aide de hello **l’activité d’exécution par lots** dans un pipeline Azure Data Factory, vous pouvez appeler une Azure ML web service toomake de prédictions sur les données de salutation dans le lot.</span><span class="sxs-lookup"><span data-stu-id="1cb84-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="1cb84-135">Consultez [appel d’un Azure ML à l’aide du service web hello l’activité d’exécution par lots](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1cb84-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="1cb84-136">Au fil du temps, utiliser des modèles prédictifs hello dans des expériences de score Azure ML hello doivent toobe reformé à l’aide de nouveaux jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1cb84-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="1cb84-137">Vous pouvez recycler un modèle Azure ML à partir d’un pipeline de fabrique de données en procédant comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1cb84-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="1cb84-138">Publier l’expérience de formation hello (expérience pas prédictive) comme un service web.</span><span class="sxs-lookup"><span data-stu-id="1cb84-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="1cb84-139">Vous effectuez cette étape Bonjour Azure ML Studio comme vous le faisiez expérience prédictive de tooexpose comme un service web dans le scénario précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="1cb84-140">Utilisez hello activité de l’exécution du lot Azure ML tooinvoke hello web service pour une expérience de formation hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="1cb84-141">En fait, vous pouvez utiliser hello exécution du lot Azure ML activité tooinvoke apprentissage service web et le calcul du score du service web.</span><span class="sxs-lookup"><span data-stu-id="1cb84-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="1cb84-142">Une fois que vous avez terminé avec le réapprentissage, mettre à jour hello calculer les scores avec qui vient d’être formé hello le service web (expérience prédictive exposé comme service web) à l’aide de hello **activité de la ressource mise à jour Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="1cb84-143">Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1cb84-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="1cb84-144">Appeler un service web à l’aide de l’activité d’exécution par lots</span><span class="sxs-lookup"><span data-stu-id="1cb84-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="1cb84-145">Vous utilisez le traitement et le déplacement des données de Azure Data Factory tooorchestrate, puis effectuez l’exécution du lot à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1cb84-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="1cb84-146">Voici les étapes de niveau supérieur de hello :</span><span class="sxs-lookup"><span data-stu-id="1cb84-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="1cb84-147">Créer un service lié Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1cb84-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="1cb84-148">Vous devez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="1cb84-148">You need hello following values:</span></span>

   1. <span data-ttu-id="1cb84-149">**URI de demande** pour hello API de l’exécution du lot.</span><span class="sxs-lookup"><span data-stu-id="1cb84-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="1cb84-150">Vous pouvez trouver hello URI de requête en cliquant sur hello **l’exécution par lots** lien dans la page des services web hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="1cb84-151">**Clé API** pour hello publié le service web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1cb84-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="1cb84-152">Vous trouverez la clé d’API hello en cliquant sur le service web hello que vous avez publié.</span><span class="sxs-lookup"><span data-stu-id="1cb84-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="1cb84-153">Hello d’utilisation **AzureMLBatchExecution** activité.</span><span class="sxs-lookup"><span data-stu-id="1cb84-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Tableau de bord Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI de lot](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="1cb84-156">Scénario : Expériences à l’aide de la charge des entrées/sorties de service de Web qui font référence toodata dans le stockage d’objets Blob Azure</span><span class="sxs-lookup"><span data-stu-id="1cb84-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="1cb84-157">Dans ce scénario, hello service Web de Azure Machine Learning effectue des prédictions à l’aide des données à partir d’un fichier dans un stockage d’objets blob Azure et stocke les résultats de prédiction hello dans le stockage blob hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="1cb84-158">Hello JSON suivant définit un pipeline de fabrique de données avec une activité AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="1cb84-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="1cb84-159">activité Hello a hello dataset **DecisionTreeInputBlob** en tant qu’entrée et **DecisionTreeResultBlob** en tant que sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="1cb84-160">Hello **DecisionTreeInputBlob** est passée comme un service web toohello d’entrée à l’aide de hello **webServiceInput** propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="1cb84-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="1cb84-161">Hello **DecisionTreeResultBlob** est passé en tant que sortie toohello Web service par à l’aide de hello **webServiceOutputs** propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="1cb84-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1cb84-162">Si le service web de hello accepte plusieurs entrées, utilisez hello **webServiceInputs** propriété au lieu d’utiliser **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="1cb84-163">Consultez hello [service Web nécessite plusieurs entrées](#web-service-requires-multiple-inputs) pour obtenir un exemple d’utilisation de hello webServiceInputs propriété.</span><span class="sxs-lookup"><span data-stu-id="1cb84-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="1cb84-164">Jeux de données qui est référencées par hello **webServiceInput**/**webServiceInputs** et **webServiceOutputs** propriétés (dans  **typeProperties**) doit également être inclus dans hello activité **entrées** et **génère**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="1cb84-165">Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser.</span><span class="sxs-lookup"><span data-stu-id="1cb84-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="1cb84-166">noms Hello que vous utilisez pour webServiceInputs, webServiceOutputs et globalParameters paramètres doivent correspondre exactement noms hello dans des expériences de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="1cb84-167">Vous pouvez afficher la charge utile de demande hello exemple sur la page d’aide de l’exécution de lot hello pour votre mappage hello attendu d’Azure ML point de terminaison tooverify.</span><span class="sxs-lookup"><span data-stu-id="1cb84-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
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
> <span data-ttu-id="1cb84-168">Uniquement les entrées et sorties de hello AzureMLBatchExecution activité peuvent être passés en tant que paramètres toohello service Web.</span><span class="sxs-lookup"><span data-stu-id="1cb84-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="1cb84-169">Par exemple, Bonjour ci-dessus extrait de code JSON, DecisionTreeInputBlob est une activité AzureMLBatchExecution, qui est passée comme un service Web de toohello d’entrée via un paramètre de webServiceInput de toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1cb84-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="1cb84-170">Exemple</span><span class="sxs-lookup"><span data-stu-id="1cb84-170">Example</span></span>
<span data-ttu-id="1cb84-171">Cette toohold de stockage Azure exemple utilise les deux hello les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="1cb84-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="1cb84-172">Nous recommandons que vous parcourez hello [générer votre première pipeline avec Data Factory] [ adf-build-1st-pipeline] didacticiel avant de passer par cet exemple.</span><span class="sxs-lookup"><span data-stu-id="1cb84-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="1cb84-173">Utiliser des artefacts de Data Factory hello éditeur Data Factory toocreate (services liés, les datasets, pipeline) dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="1cb84-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="1cb84-174">Créez un **service lié** pour votre service **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="1cb84-175">Si hello des fichiers d’entrée et de sortie sont dans différents comptes de stockage, vous avez besoin de deux services liés.</span><span class="sxs-lookup"><span data-stu-id="1cb84-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="1cb84-176">Voici un exemple JSON :</span><span class="sxs-lookup"><span data-stu-id="1cb84-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="1cb84-177">Créer hello **d’entrée** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="1cb84-178">Contrairement à d’autres jeux de données Data Factory, ceux-ci doivent contenir les valeurs **folderPath** et **fileName**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="1cb84-179">Vous pouvez utiliser toocause partitionnement chaque tooprocess (chaque tranche de données) de l’exécution de traitement par lots ou produire une entrée unique et fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="1cb84-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="1cb84-180">Vous devrez peut-être tooinclude certains hello de tootransform activité en amont d’entrée dans le format de fichier CSV hello et placez-le dans le compte de stockage hello pour chaque secteur.</span><span class="sxs-lookup"><span data-stu-id="1cb84-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="1cb84-181">Dans ce cas, vous ne devez pas inclure hello **externe** et **externalData** paramètres affichés dans hello suivant exemple et votre DecisionTreeInputBlob serait hello dataset de sortie d’une autre activité.</span><span class="sxs-lookup"><span data-stu-id="1cb84-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="1cb84-182">Votre fichier csv d’entrée doit avoir la ligne d’en-tête de colonne hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="1cb84-183">Si vous utilisez hello **l’activité de copie** toocreate/déplacement hello volumes partagés de cluster dans le stockage d’objets blob hello, vous devez définir les propriétés du récepteur hello **blobWriterAddHeader** trop**true**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="1cb84-184">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1cb84-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="1cb84-185">Si un fichier csv hello n’a pas de ligne d’en-tête hello, vous pouvez voir hello l’erreur suivante : **erreur dans l’activité : erreur de lecture de chaîne. Jeton inattendu : StartObject. Chemin d’accès ’’, ligne 1, position 1**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="1cb84-186">Créer hello **sortie** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="1cb84-187">Cet exemple utilise un partitionnement toocreate un chemin d’accès unique pour chaque exécution de la tranche.</span><span class="sxs-lookup"><span data-stu-id="1cb84-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="1cb84-188">Sans partitionnement de hello, activité hello entraînerait le remplacement du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

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
4. <span data-ttu-id="1cb84-189">Créer un **service lié** de type : **AzureMLLinkedService**, en fournissant la clé d’API de hello et modèle d’URL d’exécution du lot.</span><span class="sxs-lookup"><span data-stu-id="1cb84-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="1cb84-190">Enfin, créez un pipeline contenant une activité **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="1cb84-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="1cb84-191">Lors de l’exécution, le pipeline exécute hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1cb84-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="1cb84-192">Obtient l’emplacement hello du fichier d’entrée de hello à partir de vos jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1cb84-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="1cb84-193">Appelle l’exécution du lot Azure Machine Learning hello API</span><span class="sxs-lookup"><span data-stu-id="1cb84-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="1cb84-194">Copies hello lot d’exécution sortie toohello objet blob fourni dans votre jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="1cb84-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1cb84-195">L’activité AzureMLBatchExecution peut avoir zéro ou plusieurs entrées et une ou plusieurs sorties.</span><span class="sxs-lookup"><span data-stu-id="1cb84-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="1cb84-196">Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="1cb84-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="1cb84-197">Par exemple : 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="1cb84-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="1cb84-198">Hello **fin** fois est facultative.</span><span class="sxs-lookup"><span data-stu-id="1cb84-198">hello **end** time is optional.</span></span> <span data-ttu-id="1cb84-199">Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures.**»</span><span class="sxs-lookup"><span data-stu-id="1cb84-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="1cb84-200">pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.</span><span class="sxs-lookup"><span data-stu-id="1cb84-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="1cb84-201">Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1cb84-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1cb84-202">Définition d’une entrée pour l’activité de AzureMLBatchExecution hello est facultative.</span><span class="sxs-lookup"><span data-stu-id="1cb84-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="1cb84-203">Scénario : Expériences à l’aide des Modules de lecture/écriture toorefer toodata dans différents stockages</span><span class="sxs-lookup"><span data-stu-id="1cb84-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="1cb84-204">Un autre scénario courant lors de la création d’expériences Azure ML est toouse des modules de lecture et d’écriture.</span><span class="sxs-lookup"><span data-stu-id="1cb84-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="1cb84-205">module de lecture Hello est données tooload utilisé dans une expérience et module de writer hello toosave les données de vos expériences.</span><span class="sxs-lookup"><span data-stu-id="1cb84-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="1cb84-206">Pour plus d’informations sur les modules lecteur et enregistreur, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN.</span><span class="sxs-lookup"><span data-stu-id="1cb84-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="1cb84-207">Lorsque vous utilisez des modules de lecteur et writer hello, il est conseillé toouse un paramètre de service Web pour chaque propriété de ces modules de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="1cb84-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="1cb84-208">Ces paramètres web permettent les valeurs hello tooconfigure pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="1cb84-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="1cb84-209">Par exemple, vous pouvez créer une expérience avec un module lecteur qui utilise une base de données Azure SQL Database : XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1cb84-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="1cb84-210">Après avoir déployé le service web de hello, vous souhaitez tooenable les consommateurs de hello de hello web service toospecify un autre serveur Azure SQL Server appelée YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1cb84-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="1cb84-211">Cette toobe valeur configuré, vous pouvez utiliser un tooallow de paramètre de service Web.</span><span class="sxs-lookup"><span data-stu-id="1cb84-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="1cb84-212">L’entrée et la sortie du service web diffèrent des paramètres de service web.</span><span class="sxs-lookup"><span data-stu-id="1cb84-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="1cb84-213">Dans le premier scénario de hello, vous avez vu comment une entrée et la sortie peuvent être spécifiés pour un service Azure ML Web.</span><span class="sxs-lookup"><span data-stu-id="1cb84-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="1cb84-214">Dans ce scénario, vous passez des paramètres pour un service Web qui correspondent tooproperties des modules de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="1cb84-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="1cb84-215">Examinons un scénario d’utilisation de paramètres de service web.</span><span class="sxs-lookup"><span data-stu-id="1cb84-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="1cb84-216">Vous avez un service web Azure Machine Learning déployé qui utilise un lecteur module tooread de données à partir d’une des sources de données hello pris en charge par Azure Machine Learning (par exemple : base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="1cb84-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="1cb84-217">Après que l’exécution du lot hello est effectuée, les résultats hello sont écrites à l’aide d’un module de Writer (de base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="1cb84-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="1cb84-218">Aucune entrées du service web et les sorties ne sont définies dans des expériences de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="1cb84-219">Dans ce cas, nous vous recommandons de configurer les paramètres de service web appropriés pour les modules de lecteur et writer hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="1cb84-220">Cette configuration permet de toobe modules configuré à l’aide d’activité de AzureMLBatchExecution hello hello lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="1cb84-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="1cb84-221">Vous spécifiez des paramètres de service Web Bonjour **globalParameters** section dans l’activité hello JSON comme suit.</span><span class="sxs-lookup"><span data-stu-id="1cb84-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="1cb84-222">Vous pouvez également utiliser [fonctions de Data Factory](data-factory-functions-variables.md) lors du passage des valeurs hello pour les paramètres de service Web comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1cb84-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="1cb84-223">paramètres de service Web Hello respectent la casse, assurez-vous que les noms de hello que vous spécifiez dans l’activité hello JSON correspondent hello ceux qui sont exposées par le service Web de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="1cb84-224">À l’aide d’un lecteur module tooread de données à partir de plusieurs fichiers d’objets Blob Azure</span><span class="sxs-lookup"><span data-stu-id="1cb84-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="1cb84-225">Les pipelines Big Data avec des activités telles que Pig et Hive peuvent produire un ou plusieurs fichiers de sortie sans extensions.</span><span class="sxs-lookup"><span data-stu-id="1cb84-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="1cb84-226">Par exemple, lorsque vous spécifiez une table Hive externe, les données hello pour une table Hive hello externe peuvent être stockées dans le stockage blob Azure avec hello suivant 000000_0 de nom.</span><span class="sxs-lookup"><span data-stu-id="1cb84-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="1cb84-227">Vous pouvez utiliser le module de lecture hello dans une expérience de tooread plusieurs fichiers et les utiliser pour les prévisions.</span><span class="sxs-lookup"><span data-stu-id="1cb84-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="1cb84-228">Lorsque vous utilisez le module de lecture hello dans une expérience Azure Machine Learning, vous pouvez spécifier les objets Blob Azure en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="1cb84-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="1cb84-229">les fichiers de Hello Bonjour stockage d’objets blob Azure peuvent être des fichiers de sortie hello (exemple : 000000_0) qui sont produites par un script Pig et Hive en cours d’exécution sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1cb84-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="1cb84-230">Hello lecteur module vous permet de fichiers tooread (avec aucune extension) en configurant hello **toocontainer de chemin d’accès, les objets blob ou répertoire**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="1cb84-231">Hello **toocontainer de chemin d’accès** points toohello conteneur et **objets blob ou répertoire** pointe toofolder qui contient les fichiers de hello comme indiqué dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="1cb84-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="1cb84-232">Hello astérisque, \*) **Spécifie que tous les hello des fichiers dans le dossier/conteneur hello (autrement dit, données/aggregateddata/année = mois/2014-6 /\*)** sont lues dans le cadre de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Propriétés des objets blob Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="1cb84-234">Exemple</span><span class="sxs-lookup"><span data-stu-id="1cb84-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="1cb84-235">Pipeline avec l’activité AzureMLBatchExecution avec les paramètres de service web</span><span class="sxs-lookup"><span data-stu-id="1cb84-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="1cb84-236">Bonjour, exemple JSON ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="1cb84-236">In hello above JSON example:</span></span>

* <span data-ttu-id="1cb84-237">Hello déployé Azure Machine Learning service Web utilise un lecteur et une writer module tooread/écrire des données à partir de / tooan base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb84-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="1cb84-238">Ce service Web expose hello quatre paramètres suivants : nom du serveur, nom de la base de données, le nom de compte d’utilisateur serveur et mot de passe utilisateur serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="1cb84-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="1cb84-239">Les dates/heures de **début** et de **fin** doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="1cb84-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="1cb84-240">Par exemple : 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="1cb84-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="1cb84-241">Hello **fin** fois est facultative.</span><span class="sxs-lookup"><span data-stu-id="1cb84-241">hello **end** time is optional.</span></span> <span data-ttu-id="1cb84-242">Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures.**»</span><span class="sxs-lookup"><span data-stu-id="1cb84-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="1cb84-243">pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.</span><span class="sxs-lookup"><span data-stu-id="1cb84-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="1cb84-244">Pour plus d'informations sur les propriétés JSON, consultez [Référence sur la création de scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1cb84-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="1cb84-245">Autres scénarios</span><span class="sxs-lookup"><span data-stu-id="1cb84-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="1cb84-246">Service web nécessitant plusieurs entrées</span><span class="sxs-lookup"><span data-stu-id="1cb84-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="1cb84-247">Si le service web de hello accepte plusieurs entrées, utilisez hello **webServiceInputs** propriété au lieu d’utiliser **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="1cb84-248">Jeux de données qui est référencées par hello **webServiceInputs** doit également être inclus dans hello activité **entrées**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="1cb84-249">Dans votre expérience Azure ML, les ports et paramètres globaux de l’entrée et la sortie du service web ont des noms par défaut (« input1 », « input2 ») que vous pouvez personnaliser.</span><span class="sxs-lookup"><span data-stu-id="1cb84-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="1cb84-250">noms Hello que vous utilisez pour webServiceInputs, webServiceOutputs et globalParameters paramètres doivent correspondre exactement noms hello dans des expériences de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="1cb84-251">Vous pouvez afficher la charge utile de demande hello exemple sur la page d’aide de l’exécution de lot hello pour votre mappage hello attendu d’Azure ML point de terminaison tooverify.</span><span class="sxs-lookup"><span data-stu-id="1cb84-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="1cb84-252">Le service web ne nécessite pas d’entrée</span><span class="sxs-lookup"><span data-stu-id="1cb84-252">Web Service does not require an input</span></span>
<span data-ttu-id="1cb84-253">Services web de Azure ML par lots d’exécution peut être utilisé toorun de flux de travail, par exemple R ou scripts Python, qui peut requièrent pas d’entrées.</span><span class="sxs-lookup"><span data-stu-id="1cb84-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="1cb84-254">Ou bien, expérience de hello peut-être être configurée avec un module de lecture qui n’expose pas de n’importe quel GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="1cb84-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="1cb84-255">Dans ce cas, hello AzureMLBatchExecution activité serait configurée comme suit :</span><span class="sxs-lookup"><span data-stu-id="1cb84-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="1cb84-256">Le service web ne nécessite pas d’entrée/sortie</span><span class="sxs-lookup"><span data-stu-id="1cb84-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="1cb84-257">Hello service web d’exécution par lots d’Azure ML ne dispose ne peut-être pas de sortie de Service Web configuré.</span><span class="sxs-lookup"><span data-stu-id="1cb84-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="1cb84-258">Dans cet exemple, aucune entrée ou sortie ni aucun paramètre GlobalParameters n’est configuré.</span><span class="sxs-lookup"><span data-stu-id="1cb84-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="1cb84-259">Une sortie configurée sur l’activité hello elle-même est toujours, mais il n’est pas spécifié comme un webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="1cb84-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="1cb84-260">Web Service utilise lecteurs et writers et hello activité s’exécute uniquement lorsque les autres activités ont réussi.</span><span class="sxs-lookup"><span data-stu-id="1cb84-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="1cb84-261">Hello modules Azure ML web service lecteur et writer peuvent être configuré toorun avec ou sans les GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="1cb84-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="1cb84-262">Toutefois, vous souhaiterez peut-être tooembed service appelle dans un pipeline qui utilise le service de jeu de données dépendances tooinvoke hello uniquement lorsqu’un traitement en amont est terminée.</span><span class="sxs-lookup"><span data-stu-id="1cb84-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="1cb84-263">Vous pouvez également déclencher d’autres actions après que l’exécution du lot hello est terminée à l’aide de cette approche.</span><span class="sxs-lookup"><span data-stu-id="1cb84-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="1cb84-264">Dans ce cas, vous pouvez exprimer des dépendances hello à l’aide d’activité entrées et sorties, sans les nommer un d'entre eux en tant que Service Web entrée ni sortie.</span><span class="sxs-lookup"><span data-stu-id="1cb84-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="1cb84-265">Hello **éléments importants à retenir** sont :</span><span class="sxs-lookup"><span data-stu-id="1cb84-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="1cb84-266">Si le point de terminaison de votre expérience utilise un webServiceInput : il est représenté par un jeu de données d’objet blob et est inclus dans les entrées de l’activité hello et propriété de webServiceInput hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="1cb84-267">Sinon, la propriété de webServiceInput hello est omise.</span><span class="sxs-lookup"><span data-stu-id="1cb84-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="1cb84-268">Si le point de terminaison de votre expérience utilise webServiceOutput(s) : ils sont représentés par des jeux de données objet blob et sont inclus dans les sorties d’activité hello et dans la propriété de webServiceOutputs hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="1cb84-269">activité Hello génère et webServiceOutputs sont mappés par nom hello de chaque sortie dans l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="1cb84-270">Dans le cas contraire, la propriété de webServiceOutputs hello est omise.</span><span class="sxs-lookup"><span data-stu-id="1cb84-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="1cb84-271">Si le point de terminaison de votre expérience expose globalParameter(s), ils reçoivent dans la propriété globalParameters de l’activité hello comme la paires clé / valeur.</span><span class="sxs-lookup"><span data-stu-id="1cb84-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="1cb84-272">Dans le cas contraire, la propriété de globalParameters hello est omise.</span><span class="sxs-lookup"><span data-stu-id="1cb84-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="1cb84-273">les clés Hello respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="1cb84-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="1cb84-274">[Fonctions d’Azure Data Factory](data-factory-functions-variables.md) peuvent être utilisées dans les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="1cb84-275">Datasets supplémentaires peuvent figurer dans les propriétés entrées et sorties d’activité hello, sans référencé dans typeProperties d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="1cb84-276">Ces jeux de données régissent l’exécution à l’aide de la tranche dépendances mais est sinon ignorées par hello AzureMLBatchExecution activité.</span><span class="sxs-lookup"><span data-stu-id="1cb84-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="1cb84-277">Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour</span><span class="sxs-lookup"><span data-stu-id="1cb84-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="1cb84-278">Une fois que vous avez terminé avec le réapprentissage, mettre à jour hello calculer les scores avec qui vient d’être formé hello le service web (expérience prédictive exposé comme service web) à l’aide de hello **activité de la ressource mise à jour Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="1cb84-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="1cb84-279">Consultez l’article [Mise à jour des modèles à l’aide de l’activité des ressources de mise à jour](data-factory-azure-ml-update-resource-activity.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1cb84-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="1cb84-280">Modules Lecteur et Enregistreur</span><span class="sxs-lookup"><span data-stu-id="1cb84-280">Reader and Writer Modules</span></span>
<span data-ttu-id="1cb84-281">Un scénario courant pour l’utilisation de paramètres de service Web est utiliser hello enregistreurs et lecteurs de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb84-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="1cb84-282">module de lecture Hello est données tooload utilisé dans une expérience à partir des services de gestion des données en dehors d’Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="1cb84-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="1cb84-283">module de writer Hello est toosave les données de vos expériences dans les services de gestion en dehors d’Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="1cb84-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="1cb84-284">Pour plus d’informations sur les modules enregistreur/lecteur Azure Blob/SQL Azure, voir les rubriques [Lecteur](https://msdn.microsoft.com/library/azure/dn905997.aspx) et [Enregistreur](https://msdn.microsoft.com/library/azure/dn905984.aspx) dans la bibliothèque MSDN.</span><span class="sxs-lookup"><span data-stu-id="1cb84-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="1cb84-285">exemple Hello dans la section précédente de hello utilisé la lecture d’objets Blob Azure hello et un writer d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb84-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="1cb84-286">Cette section décrit leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="1cb84-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="1cb84-287">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1cb84-287">Frequently asked questions</span></span>
<span data-ttu-id="1cb84-288">**Q :** J’ai plusieurs fichiers qui sont générés par mes pipelines Big Data.</span><span class="sxs-lookup"><span data-stu-id="1cb84-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="1cb84-289">Puis-je utiliser hello AzureMLBatchExecution activité toowork sur tous les fichiers hello ?</span><span class="sxs-lookup"><span data-stu-id="1cb84-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="1cb84-290">**R :** Oui.</span><span class="sxs-lookup"><span data-stu-id="1cb84-290">**A:** Yes.</span></span> <span data-ttu-id="1cb84-291">Consultez hello **à l’aide d’un lecteur module tooread de données à partir de plusieurs fichiers d’objets Blob Azure** pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1cb84-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="1cb84-292">Activité de notation par lots Azure ML</span><span class="sxs-lookup"><span data-stu-id="1cb84-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="1cb84-293">Si vous utilisez hello **AzureMLBatchScoring** toointegrate d’activité avec Azure Machine Learning, nous vous recommandons d’utiliser hello dernières **AzureMLBatchExecution** activité.</span><span class="sxs-lookup"><span data-stu-id="1cb84-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="1cb84-294">Hello AzureMLBatchExecution activité est introduit dans hello version d’août 2015 de Windows Azure SDK et Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1cb84-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="1cb84-295">Si vous souhaitez toocontinue à l’aide d’activité de AzureMLBatchScoring hello, continuer à lire dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1cb84-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="1cb84-296">Activité de notation par lots Azure ML utilisant Azure Storage pour l’entrée/la sortie</span><span class="sxs-lookup"><span data-stu-id="1cb84-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="1cb84-297">Paramètres de service web</span><span class="sxs-lookup"><span data-stu-id="1cb84-297">Web Service Parameters</span></span>
<span data-ttu-id="1cb84-298">toospecify des valeurs pour les paramètres de service Web, ajoutez un **typeProperties** section toohello **AzureMLBatchScoringActivty** section dans le pipeline hello JSON comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1cb84-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="1cb84-299">Vous pouvez également utiliser [fonctions de Data Factory](data-factory-functions-variables.md) lors du passage des valeurs hello pour les paramètres de service Web comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1cb84-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="1cb84-300">paramètres de service Web Hello respectent la casse, assurez-vous que les noms de hello que vous spécifiez dans l’activité hello JSON correspondent hello ceux qui sont exposées par le service Web de hello.</span><span class="sxs-lookup"><span data-stu-id="1cb84-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="1cb84-301">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1cb84-301">See Also</span></span>
* [<span data-ttu-id="1cb84-302">Article de blog Azure : prise en main d’Azure Data Factory et d’Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1cb84-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
