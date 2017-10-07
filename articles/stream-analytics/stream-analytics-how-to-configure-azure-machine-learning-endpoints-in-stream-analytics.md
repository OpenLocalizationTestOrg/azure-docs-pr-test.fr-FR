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
# <a name="machine-learning-integration-in-stream-analytics"></a>Intégration de Machine Learning dans Stream Analytics
Analytique de flux de données prend en charge les fonctions définies par l’utilisateur contenant des points de terminaison de Machine Learning tooAzure. Prise en charge de l’API REST de cette fonctionnalité est détaillée dans hello [bibliothèque de flux de données Analytique REST API](https://msdn.microsoft.com/library/azure/dn835031.aspx). Cet article fournit les informations supplémentaires nécessaires à la mise en œuvre réussie de cette fonctionnalité dans Stream Analytics. Un didacticiel a également été validé et est disponible [ici](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Vue d’ensemble de la terminologie Azure Machine Learning
Microsoft Azure Machine Learning fournit un outil de collaboration, glisser-déplacer vous pouvez utiliser toobuild, tester et déployer des solutions d’analytique prédictive sur vos données. Cet outil est appelé hello *Azure Machine Learning Studio*. studio de Hello est toointeract utilisé avec hello ressources d’apprentissage et facilement générer, tester et itérez au sein de votre conception. Ces ressources et leurs définitions se trouvent ci-dessous.

* **Espace de travail**: hello *espace de travail* est un conteneur qui contient toutes les autres ressources d’apprentissage dans un conteneur pour la gestion et de contrôle.
* **Expérience**: *expériences* sont créés par les données scientifiques tooutilize datasets et de l’apprentissage d’un modèle d’apprentissage.
* **Point de terminaison**: *points de terminaison* sont hello Azure Machine Learning de fonctionnalités de tootake objet utilisé comme entrée, appliquer un modèle d’apprentissage de l’ordinateur spécifié et retourne une sortie au score calculé.
* **Service Web d’évaluation**: un *service web d’évaluation* est une collection de points de terminaison, comme indiqué ci-dessus.

Chaque point de terminaison dispose d’API servant à l’exécution de lots et l’exécution synchronisée. Stream Analytics utilise l’exécution synchronisée. service spécifique de Hello se nomme un [Service de demande/réponse](../machine-learning/machine-learning-consume-web-services.md) dans AzureML studio.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Ressources Machine Learning nécessaires aux tâches d’analyse Stream Analytics
Pour les besoins de hello de flux de données Analytique de la tâche de traitement, un point de terminaison demande/réponse, une [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), et une définition swagger sont nécessaires pour réussir une exécution. Flux de données Analytique a un point de terminaison supplémentaire qui construit les url hello pour le point de terminaison swagger, recherche hello interface et renvoie un utilisateur de toohello définition par défaut définie par le.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Configuration d’une analyse Stream Analytics et d’une fonction définie par l’utilisateur Machine Learning via une API REST
À l’aide des API REST, vous pouvez configurer vos fonctions de langage de Machine Azure toocall. étapes de Hello sont les suivantes :

1. Création d’un travail Stream Analytics
2. Définition d’une entrée
3. Définition d’une sortie
4. Création d’une fonction définie par l’utilisateur
5. Écrire une transformation de flux de données Analytique que les appels hello UDF
6. Démarrer le travail de hello

## <a name="creating-a-udf-with-basic-properties"></a>Création d’une fonction définie par l’utilisateur avec des propriétés de base
Par exemple, hello suivant l’exemple de code crée un fichier UDF scalaire nommé *newudf* qui lie le point de terminaison Azure Machine Learning tooan. Notez que hello *point de terminaison* (URI du service) se trouvent sur la page d’aide hello API hello choisi service et hello *apiKey* se trouvent sur la page principale des Services de hello.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Exemple de corps de requête :  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>Appeler le point de terminaison RetrieveDefaultDefinition pour la fonction définie par l’utilisateur par défaut
Une fois hello squelette QU'UDF est créé la définition complète de hello Hello QU'UDF est nécessaire. point de terminaison Hello RetreiveDefaultDefinition vous permet d’obtenir la définition de valeur par défaut hello pour une fonction scalaire qui est le point de terminaison Azure Machine Learning tooan liée. charge utile de Hello ci-dessous nécessite la définition de tooget hello par défaut définie par le pour une fonction scalaire qui est le point de terminaison Azure Machine Learning tooan liée. Il ne spécifie pas point de terminaison réel hello comme il a déjà été fourni au cours de la demande PUT. Flux de données Analytique appelle point de terminaison hello fournie dans la demande de hello si elle est fournie explicitement. Sinon, elle utilise hello un référencé à l’origine. Ici, hello prend UDF une chaîne unique paramètre (une phrase) et retourne une seule sortie de type chaîne qui indique l’étiquette « sentiment » hello cette phrase.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Exemple de corps de requête :  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Un exemple de sortie ressemble à ce qui suit.  

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

## <a name="patch-udf-with-hello-response"></a>UDF correctif avec la réponse de hello
Maintenant hello UDF doit être corrigé avec la réponse précédente de hello, comme indiqué ci-dessous.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

Corps de la demande (sortie de RetrieveDefaultDefinition) :

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Implémenter des flux de données Analytique transformation toocall hello UDF
Maintenant, hello UDF (ici nommé scoreTweet) de la requête pour chaque événement d’entrée et écrire une réponse pour cette sortie tooan des événements.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
