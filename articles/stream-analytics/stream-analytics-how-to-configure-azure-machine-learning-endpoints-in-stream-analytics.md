---
title: "points de terminaison aaaUse Azure Machine Learning dans le flux de données Analytique | Documents Microsoft"
description: "Fonctions de langage machine définies par l’utilisateur dans Stream Analytics"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="e7387-103">Intégration de Machine Learning dans Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e7387-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="e7387-104">Analytique de flux de données prend en charge les fonctions définies par l’utilisateur contenant des points de terminaison de Machine Learning tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e7387-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="e7387-105">Prise en charge de l’API REST de cette fonctionnalité est détaillée dans hello [bibliothèque de flux de données Analytique REST API](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7387-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="e7387-106">Cet article fournit les informations supplémentaires nécessaires à la mise en œuvre réussie de cette fonctionnalité dans Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="e7387-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="e7387-107">Un didacticiel a également été validé et est disponible [ici](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e7387-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="e7387-108">Vue d’ensemble de la terminologie Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e7387-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="e7387-109">Microsoft Azure Machine Learning fournit un outil de collaboration, glisser-déplacer vous pouvez utiliser toobuild, tester et déployer des solutions d’analytique prédictive sur vos données.</span><span class="sxs-lookup"><span data-stu-id="e7387-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="e7387-110">Cet outil est appelé hello *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="e7387-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="e7387-111">studio de Hello est toointeract utilisé avec hello ressources d’apprentissage et facilement générer, tester et itérez au sein de votre conception.</span><span class="sxs-lookup"><span data-stu-id="e7387-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="e7387-112">Ces ressources et leurs définitions se trouvent ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e7387-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="e7387-113">**Espace de travail**: hello *espace de travail* est un conteneur qui contient toutes les autres ressources d’apprentissage dans un conteneur pour la gestion et de contrôle.</span><span class="sxs-lookup"><span data-stu-id="e7387-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="e7387-114">**Expérience**: *expériences* sont créés par les données scientifiques tooutilize datasets et de l’apprentissage d’un modèle d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="e7387-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="e7387-115">**Point de terminaison**: *points de terminaison* sont hello Azure Machine Learning de fonctionnalités de tootake objet utilisé comme entrée, appliquer un modèle d’apprentissage de l’ordinateur spécifié et retourne une sortie au score calculé.</span><span class="sxs-lookup"><span data-stu-id="e7387-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="e7387-116">**Service Web d’évaluation**: un *service web d’évaluation* est une collection de points de terminaison, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e7387-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="e7387-117">Chaque point de terminaison dispose d’API servant à l’exécution de lots et l’exécution synchronisée.</span><span class="sxs-lookup"><span data-stu-id="e7387-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="e7387-118">Stream Analytics utilise l’exécution synchronisée.</span><span class="sxs-lookup"><span data-stu-id="e7387-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="e7387-119">service spécifique de Hello se nomme un [Service de demande/réponse](../machine-learning/machine-learning-consume-web-services.md) dans AzureML studio.</span><span class="sxs-lookup"><span data-stu-id="e7387-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="e7387-120">Ressources Machine Learning nécessaires aux tâches d’analyse Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e7387-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="e7387-121">Pour les besoins de hello de flux de données Analytique de la tâche de traitement, un point de terminaison demande/réponse, une [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), et une définition swagger sont nécessaires pour réussir une exécution.</span><span class="sxs-lookup"><span data-stu-id="e7387-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="e7387-122">Flux de données Analytique a un point de terminaison supplémentaire qui construit les url hello pour le point de terminaison swagger, recherche hello interface et renvoie un utilisateur de toohello définition par défaut définie par le.</span><span class="sxs-lookup"><span data-stu-id="e7387-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="e7387-123">Configuration d’une analyse Stream Analytics et d’une fonction définie par l’utilisateur Machine Learning via une API REST</span><span class="sxs-lookup"><span data-stu-id="e7387-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="e7387-124">À l’aide des API REST, vous pouvez configurer vos fonctions de langage de Machine Azure toocall.</span><span class="sxs-lookup"><span data-stu-id="e7387-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="e7387-125">étapes de Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7387-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="e7387-126">Création d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e7387-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="e7387-127">Définition d’une entrée</span><span class="sxs-lookup"><span data-stu-id="e7387-127">Define an input</span></span>
3. <span data-ttu-id="e7387-128">Définition d’une sortie</span><span class="sxs-lookup"><span data-stu-id="e7387-128">Define an output</span></span>
4. <span data-ttu-id="e7387-129">Création d’une fonction définie par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e7387-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="e7387-130">Écrire une transformation de flux de données Analytique que les appels hello UDF</span><span class="sxs-lookup"><span data-stu-id="e7387-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="e7387-131">Démarrer le travail de hello</span><span class="sxs-lookup"><span data-stu-id="e7387-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="e7387-132">Création d’une fonction définie par l’utilisateur avec des propriétés de base</span><span class="sxs-lookup"><span data-stu-id="e7387-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="e7387-133">Par exemple, hello suivant l’exemple de code crée un fichier UDF scalaire nommé *newudf* qui lie le point de terminaison Azure Machine Learning tooan.</span><span class="sxs-lookup"><span data-stu-id="e7387-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="e7387-134">Notez que hello *point de terminaison* (URI du service) se trouvent sur la page d’aide hello API hello choisi service et hello *apiKey* se trouvent sur la page principale des Services de hello.</span><span class="sxs-lookup"><span data-stu-id="e7387-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="e7387-135">Exemple de corps de requête :</span><span class="sxs-lookup"><span data-stu-id="e7387-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="e7387-136">Appeler le point de terminaison RetrieveDefaultDefinition pour la fonction définie par l’utilisateur par défaut</span><span class="sxs-lookup"><span data-stu-id="e7387-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="e7387-137">Une fois hello squelette QU'UDF est créé la définition complète de hello Hello QU'UDF est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e7387-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="e7387-138">point de terminaison Hello RetreiveDefaultDefinition vous permet d’obtenir la définition de valeur par défaut hello pour une fonction scalaire qui est le point de terminaison Azure Machine Learning tooan liée.</span><span class="sxs-lookup"><span data-stu-id="e7387-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="e7387-139">charge utile de Hello ci-dessous nécessite la définition de tooget hello par défaut définie par le pour une fonction scalaire qui est le point de terminaison Azure Machine Learning tooan liée.</span><span class="sxs-lookup"><span data-stu-id="e7387-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="e7387-140">Il ne spécifie pas point de terminaison réel hello comme il a déjà été fourni au cours de la demande PUT.</span><span class="sxs-lookup"><span data-stu-id="e7387-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="e7387-141">Flux de données Analytique appelle point de terminaison hello fournie dans la demande de hello si elle est fournie explicitement.</span><span class="sxs-lookup"><span data-stu-id="e7387-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="e7387-142">Sinon, elle utilise hello un référencé à l’origine.</span><span class="sxs-lookup"><span data-stu-id="e7387-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="e7387-143">Ici, hello prend UDF une chaîne unique paramètre (une phrase) et retourne une seule sortie de type chaîne qui indique l’étiquette « sentiment » hello cette phrase.</span><span class="sxs-lookup"><span data-stu-id="e7387-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="e7387-144">Exemple de corps de requête :</span><span class="sxs-lookup"><span data-stu-id="e7387-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="e7387-145">Un exemple de sortie ressemble à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="e7387-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="e7387-146">UDF correctif avec la réponse de hello</span><span class="sxs-lookup"><span data-stu-id="e7387-146">Patch UDF with hello response</span></span>
<span data-ttu-id="e7387-147">Maintenant hello UDF doit être corrigé avec la réponse précédente de hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e7387-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="e7387-148">Corps de la demande (sortie de RetrieveDefaultDefinition) :</span><span class="sxs-lookup"><span data-stu-id="e7387-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="e7387-149">Implémenter des flux de données Analytique transformation toocall hello UDF</span><span class="sxs-lookup"><span data-stu-id="e7387-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="e7387-150">Maintenant, hello UDF (ici nommé scoreTweet) de la requête pour chaque événement d’entrée et écrire une réponse pour cette sortie tooan des événements.</span><span class="sxs-lookup"><span data-stu-id="e7387-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="e7387-151">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="e7387-151">Get help</span></span>
<span data-ttu-id="e7387-152">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="e7387-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7387-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7387-153">Next steps</span></span>
* [<span data-ttu-id="e7387-154">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="e7387-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e7387-155">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e7387-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e7387-156">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e7387-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e7387-157">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e7387-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e7387-158">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e7387-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
