---
title: "API Machine Learning : analyses de texte | Microsoft Docs"
description: "Machine Learning texte Analytique API Microsoft peut être utilisé tooanalyze texte non structuré pour l’analyse des sentiments, extraction d’expressions clés, détection de la langue et détection de la rubrique."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>API Machine Learning : analyse de texte pour déterminer les sentiments, l’extraction d’expressions clés, la détection de la langue et la détection de la rubrique
> [!NOTE]
> Ce guide est pour la version 1 de hello API. Pour la version 2, [ **toothis document de référence**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Version 2 correspond désormais hello par défaut de cette API.
> 
> 

## <a name="overview"></a>Vue d'ensemble
Hello texte Analytique API est une suite d’analytique de texte [services web](https://datamarket.azure.com/dataset/amla/text-analytics) intègrent Azure Machine Learning. Hello API peut être utilisé tooanalyze texte non structuré pour des tâches telles que l’analyse des sentiments, extraction d’expressions clés, détection de la langue et détection de la rubrique. Aucune données de formation ne nécessaire toouse cette API : simplement mettre vos données de texte. Cette API utilise un langage naturel avancé traitement toodeliver de techniques dans les prédictions de classe.

Vous pouvez voir analytique de texte dans une action sur notre [site de démonstration](https://text-analytics-demo.azurewebsites.net/), où vous trouverez également [exemples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sur l’analytique de texte tooimplement en c# et Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>analyse de sentiments
Hello API retourne un score entre 0 et 1. Too1 fermer des scores indiquent sentiment positif, alors que too0 fermer des scores négatifs sentiments. La valeur de notation du sentiment est générée via des techniques de classification. Hello des fonctionnalités d’entrée toohello classifieur incluent n-grammes, fonctionnalités générées à partir de morphosyntaxique balises et incorporations de word. Actuellement, l’anglais est hello uniquement prise en charge de langue.

## <a name="key-phrase-extraction"></a>Extraction d’expressions clés
Hello API retourne une liste de chaînes qui désigne les points de discussion clé hello dans le texte d’entrée hello. Nous utilisons des techniques fournies par la boîte à outils de traitement du langage naturel sophistiquée de Microsoft Office. Actuellement, l’anglais est hello uniquement prise en charge de langue.

## <a name="language-detection"></a>Détection de la langue
Hello API renvoie hello a détecté la langue et un score entre 0 et 1. Too1 fermer des scores indiquent la certitude de 100 % language de hello identifié a la valeur true. Au total, 120 langues sont prises en charge.

## <a name="topic-detection"></a>Détection de la rubrique
Il s’agit d’une API qui vient d’être publiée qui retourne les rubriques de détectés supérieur hello pour une liste des enregistrements texte envoyé. Une rubrique est identifiée par une expression clé, représentée par un ou plusieurs mots associés. Cette API requiert un minimum de 100 texte enregistre toobe soumis, mais est conçue toodetect rubriques sur des centaines toothousands d’enregistrements. Notez que cette API facture 1 transaction par enregistrement texte soumis. Hello API est toowork conçue pour humaines court, écrit du texte tels que les révisions et les commentaires des utilisateurs.

- - -
## <a name="api-definition"></a>Définition de l’API
### <a name="headers"></a>headers
Veillez à inclure les en-têtes correct hello dans votre demande, qui doit se présenter comme suit :

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Vous pouvez trouver votre clé de compte dans votre compte Bonjour [Azure Data Market](https://datamarket.azure.com/account/keys). Actuellement, seul JSON est accepté pour les formats d’entrée et de sortie. XML n’est pas pris en charge.

- - -
## <a name="single-response-apis"></a>API à réponse unique
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Exemple de demande**

Dans l’appel hello ci-dessous, nous invitons analyse des sentiments pour la phrase de hello « Hello World » :

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Cette requête renverra une réponse du type :

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Exemple de demande**

Dans l’appel hello ci-dessous, nous invitons les expressions clés hello trouvée dans le texte hello « Il était un toostay hôtel merveilleux au, avec décor unique et convivial » :

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Cette requête renverra une réponse du type :

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Exemple de demande**

Dans l’appel GET hello ci-dessous, nous invitons pour sentiment hello pour les expressions clés de hello dans le texte hello *Hello World*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Cette requête renverra une réponse du type :

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Paramètres facultatifs**

`NumberOfLanguagesToDetect` est un paramètre facultatif. valeur par défaut Hello est 1.

- - -
## <a name="batch-apis"></a>API Batch
Hello service de texte Analytique permet de vous sentiment de toodo et les extractions de phrase clé en mode batch. Notez que chacun des enregistrements de hello transformée nombres comme une transaction. Par exemple, si vous demandez le sentiment pour 1 000 enregistrements en un seul appel, 1 000 transactions sont déduites.

Notez que les identificateurs hello entrés dans le système de hello sont ID hello retournés par le système de hello. service web de Hello ne vérifie pas que ces ID est uniques. Il incombe hello d’unicité de tooverify hello appelant. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Exemple de demande**

Bonjour POST appeler ci-dessous, nous invitons pour les éléments hello d’expressions hello « Hello World », « Hello World de Foo » et « Mes Bonjour » dans le corps hello de demande de hello :

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Corps de la requête :

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

Dans la réponse de hello ci-dessous, vous obtenez la liste hello des scores associé à votre ID de texte :

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Exemple de demande**

Dans cet exemple, nous invitons pour la liste d’éléments pour des expressions clés hello Bonjour suivant textes hello : 

* « Il était un toostay hôtel merveilleux au, avec décor unique et convivial »
* « La conférence était exceptionnelle, avec des discussions très intéressantes »
* « le trafic de hello a été horribles, j’ai passé à trois heures va toohello aéroport »

Cette demande est effectuée en tant qu’un point de terminaison du toohello appel POST :

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Corps de la requête :

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

Dans la réponse de hello ci-dessous, vous obtenez la liste hello des expressions clés associées à votre ID de texte :

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

Dans l’appel POST hello ci-dessous, nous invitons détection de la langue pour les deux entrées de texte :

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Corps de la requête :

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Cet exemple renvoie hello suivant réponse, où anglais est détectée dans la première entrée de hello et Français dans la deuxième entrée du hello :

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>API de détection de la rubrique
Il s’agit d’une API qui vient d’être publiée qui retourne les rubriques de détectés supérieur hello pour une liste des enregistrements texte envoyé. Une rubrique est identifiée par une expression clé, représentée par un ou plusieurs mots associés. Notez que cette API facture 1 transaction par enregistrement texte soumis.

Cette API requiert un minimum de 100 texte enregistre toobe soumis, mais est conçue toodetect rubriques sur des centaines toothousands d’enregistrements.

### <a name="topics--submit-job"></a>Rubriques – Envoyer le travail
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Exemple de demande**

Dans l’appel POST hello ci-dessous, nous invitons les rubriques pour un ensemble de 100 articles, où hello et prénom d’entrée articles sont affichés, et deux StopPhrases sont inclus.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Corps de la requête :

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

Dans la réponse de hello ci-dessous, vous obtenez hello JobId pour les travaux soumis hello :

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Une liste de mots uniques ou de phrases qui ne doivent pas être renvoyés comme des rubriques. Peut être utilisé toofilter rubriques très générique. Par exemple, dans un jeu de données sur les évaluations d’un hôtel, « hotel » et « hostel » peuvent être des StopPhrases.  

### <a name="topics--poll-for-job-results"></a>Rubriques – Recherche des résultats d’un travail
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Exemple de demande**

Passez hello que JobID retourné à partir des résultats de hello 'job Submit' étape toofetch hello. Nous vous recommandons d’appeler ce point de terminaison toutes les minutes jusqu'à ce que l’état = 'Terminé' dans la réponse de hello. Elle prendra environ 10 minutes pour un travail toocomplete, ou plus pour les travaux avec des milliers d’enregistrements.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Pendant son traitement, réponse de hello seront comme suit :

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Hello API retourne la sortie au format JSON Bonjour suivant le format :

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


propriétés Hello pour chaque partie de la réponse de hello sont les suivantes :

**Propriétés de TopicInfo**

| Clé | Description |
|:--- |:--- |
| TopicId |Identificateur unique de chaque rubrique. |
| Score |Nombre d’enregistrements assigné tootopic. |
| KeyPhrase |Un mot ou une expression pour une rubrique de hello résumer. Peut contenir un ou plusieurs mots. |

**Propriétés de TopicAssignment**

| Clé | Description |
|:--- |:--- |
| Id |Identificateur de l’enregistrement de hello. Attribue un ID toohello inclus dans l’entrée de hello. |
| TopicId |ID de rubrique Hello enregistrement hello a été affectée. |
| Distance |Confiance hello enregistrement appartient toohello rubrique. Toozero de plus près de distance indique toute confiance. |

