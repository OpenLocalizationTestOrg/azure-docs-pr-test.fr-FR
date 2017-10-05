---
title: "API Machine Learning : analyses de texte | Microsoft Docs"
description: "Les API Machine Learning Text Analytics de Microsoft peuvent être utilisées pour analyser le texte non structuré dans le cadre de l’analyse de sentiments, l’extraction d’expressions clés, la détection de la langue et la détection de la rubrique."
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
redirect_document_id: TRUE
ms.openlocfilehash: 10eae2ff5624dcb57de1cf72b326147f35bc2a0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="22432-103">API Machine Learning : analyse de texte pour déterminer les sentiments, l’extraction d’expressions clés, la détection de la langue et la détection de la rubrique</span><span class="sxs-lookup"><span data-stu-id="22432-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="22432-104">Ce guide concerne la version 1 de l’API.</span><span class="sxs-lookup"><span data-stu-id="22432-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="22432-105">Pour la version 2, [**consultez ce document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="22432-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="22432-106">La version 2 est désormais la version par défaut de cette API.</span><span class="sxs-lookup"><span data-stu-id="22432-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="22432-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="22432-107">Overview</span></span>
<span data-ttu-id="22432-108">L’API Text Analytics est une suite de [services web](https://datamarket.azure.com/dataset/amla/text-analytics) d’analyse de texte intégrée dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="22432-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="22432-109">Cette API peut être utilisée pour analyser le texte non structuré dans le cadre de différentes tâches, comme l’analyse de sentiments, l’extraction d’expressions clés, la détection de la langue et la détection de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="22432-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="22432-110">L’utilisation de cette API ne requiert aucune formation. Il vous suffit d’importer vos données de texte.</span><span class="sxs-lookup"><span data-stu-id="22432-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="22432-111">Cette API utilise des techniques avancées de traitement du langage naturel pour effectuer des prédictions de pointe.</span><span class="sxs-lookup"><span data-stu-id="22432-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="22432-112">Vous pouvez voir une démonstration de l’analyse de texte sur notre [site de démo](https://text-analytics-demo.azurewebsites.net/), où vous trouverez également des [exemples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) d’implémentation de l’analyse de texte dans C# et Python.</span><span class="sxs-lookup"><span data-stu-id="22432-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="22432-113">analyse de sentiments</span><span class="sxs-lookup"><span data-stu-id="22432-113">Sentiment analysis</span></span>
<span data-ttu-id="22432-114">Cette API renvoie une valeur numérique de notation située entre 0 et 1.</span><span class="sxs-lookup"><span data-stu-id="22432-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="22432-115">Les valeurs de notation proches de 1 indiquent un sentiment positif, tandis que les valeurs proches de 0 signalent un sentiment négatif.</span><span class="sxs-lookup"><span data-stu-id="22432-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="22432-116">La valeur de notation du sentiment est générée via des techniques de classification.</span><span class="sxs-lookup"><span data-stu-id="22432-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="22432-117">Les fonctionnalités d’entrée du classifieur incluent des services n-grams, des fonctionnalités générées à partir de balises morphosyntaxiques et des incorporations de mot.</span><span class="sxs-lookup"><span data-stu-id="22432-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="22432-118">Actuellement, l’anglais est la seule langue prise en charge.</span><span class="sxs-lookup"><span data-stu-id="22432-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="22432-119">Extraction d’expressions clés</span><span class="sxs-lookup"><span data-stu-id="22432-119">Key phrase extraction</span></span>
<span data-ttu-id="22432-120">L’API renvoie une liste de chaînes indiquant les principaux propos suggérés dans le texte en entrée.</span><span class="sxs-lookup"><span data-stu-id="22432-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="22432-121">Nous utilisons des techniques fournies par la boîte à outils de traitement du langage naturel sophistiquée de Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="22432-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="22432-122">Actuellement, l’anglais est la seule langue prise en charge.</span><span class="sxs-lookup"><span data-stu-id="22432-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="22432-123">Détection de la langue</span><span class="sxs-lookup"><span data-stu-id="22432-123">Language detection</span></span>
<span data-ttu-id="22432-124">L’API indique la langue détectée et un score entre 0 et 1.</span><span class="sxs-lookup"><span data-stu-id="22432-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="22432-125">Un score proche de 1 indique une certitude à 100 % que la langue identifiée est la bonne.</span><span class="sxs-lookup"><span data-stu-id="22432-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="22432-126">Au total, 120 langues sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="22432-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="22432-127">Détection de la rubrique</span><span class="sxs-lookup"><span data-stu-id="22432-127">Topic detection</span></span>
<span data-ttu-id="22432-128">Il s’agit d’une API lancée récemment, qui renvoie les premières rubriques détectées pour une liste d’enregistrements texte soumis.</span><span class="sxs-lookup"><span data-stu-id="22432-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="22432-129">Une rubrique est identifiée par une expression clé, représentée par un ou plusieurs mots associés.</span><span class="sxs-lookup"><span data-stu-id="22432-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="22432-130">Cette API nécessite l’envoi d’au moins 100 enregistrements texte, mais elle est conçu pour détecter des rubriques parmi des centaines de milliers d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="22432-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="22432-131">Notez que cette API facture 1 transaction par enregistrement texte soumis.</span><span class="sxs-lookup"><span data-stu-id="22432-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="22432-132">L'API est conçue pour fonctionner correctement avec un texte court écrit par un humain, par exemple des évaluations et des commentaires d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="22432-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="22432-133">Définition de l’API</span><span class="sxs-lookup"><span data-stu-id="22432-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="22432-134">En-têtes</span><span class="sxs-lookup"><span data-stu-id="22432-134">Headers</span></span>
<span data-ttu-id="22432-135">Veillez à inclure les bons en-têtes dans votre requête, qui doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="22432-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="22432-136">Vous trouverez votre clé de compte dans votre compte sur [Azure Data Market](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="22432-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="22432-137">Actuellement, seul JSON est accepté pour les formats d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="22432-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="22432-138">XML n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="22432-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="22432-139">API à réponse unique</span><span class="sxs-lookup"><span data-stu-id="22432-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="22432-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="22432-140">GetSentiment</span></span>
<span data-ttu-id="22432-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="22432-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="22432-142">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="22432-142">**Example request**</span></span>

<span data-ttu-id="22432-143">Dans l’appel ci-dessous, nous demandons l’analyse du sentiment de l’expression « Hello World » :</span><span class="sxs-lookup"><span data-stu-id="22432-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="22432-144">Cette requête renverra une réponse du type :</span><span class="sxs-lookup"><span data-stu-id="22432-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="22432-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="22432-145">GetKeyPhrases</span></span>
<span data-ttu-id="22432-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="22432-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="22432-147">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="22432-147">**Example request**</span></span>

<span data-ttu-id="22432-148">Dans l’appel ci-dessous, nous demandons les expressions clés dans le texte « Nous avons passé un formidable séjour dans cet hôtel, la décoration est exceptionnelle et le personnel très accueillant » :</span><span class="sxs-lookup"><span data-stu-id="22432-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="22432-149">Cette requête renverra une réponse du type :</span><span class="sxs-lookup"><span data-stu-id="22432-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="22432-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="22432-150">GetLanguage</span></span>
<span data-ttu-id="22432-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="22432-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="22432-152">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="22432-152">**Example request**</span></span>

<span data-ttu-id="22432-153">Dans l’appel GET ci-dessous, nous demandons le sentiment des expressions clés dans le texte *Hello World*</span><span class="sxs-lookup"><span data-stu-id="22432-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="22432-154">Cette requête renverra une réponse du type :</span><span class="sxs-lookup"><span data-stu-id="22432-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="22432-155">**Paramètres facultatifs**</span><span class="sxs-lookup"><span data-stu-id="22432-155">**Optional parameters**</span></span>

<span data-ttu-id="22432-156">`NumberOfLanguagesToDetect` est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="22432-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="22432-157">La valeur par défaut est 1.</span><span class="sxs-lookup"><span data-stu-id="22432-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="22432-158">API Batch</span><span class="sxs-lookup"><span data-stu-id="22432-158">Batch APIs</span></span>
<span data-ttu-id="22432-159">Le service d’analyse de texte vous permet d’effectuer des extractions de sentiments et d’expressions clés en mode Batch.</span><span class="sxs-lookup"><span data-stu-id="22432-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="22432-160">Notez que chacun des enregistrements notés compte comme une transaction unique.</span><span class="sxs-lookup"><span data-stu-id="22432-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="22432-161">Par exemple, si vous demandez le sentiment pour 1 000 enregistrements en un seul appel, 1 000 transactions sont déduites.</span><span class="sxs-lookup"><span data-stu-id="22432-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="22432-162">Remarque : les ID saisis dans le système sont les ID retournés par le système.</span><span class="sxs-lookup"><span data-stu-id="22432-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="22432-163">Le service web ne vérifie pas que ces ID sont uniques.</span><span class="sxs-lookup"><span data-stu-id="22432-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="22432-164">Il incombe à l’appelant d’en vérifier l’unicité.</span><span class="sxs-lookup"><span data-stu-id="22432-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="22432-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="22432-165">GetSentimentBatch</span></span>
<span data-ttu-id="22432-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="22432-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="22432-167">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="22432-167">**Example request**</span></span>

<span data-ttu-id="22432-168">Dans l’appel POST ci-dessous, nous demandons les sentiments des expressions « Hello World », « Hello Foo World » et « Hello My World » dans le corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="22432-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="22432-169">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="22432-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="22432-170">Dans la réponse ci-dessous, vous obtenez la liste de résultats associée à vos ID de texte :</span><span class="sxs-lookup"><span data-stu-id="22432-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="22432-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="22432-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="22432-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="22432-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="22432-173">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="22432-173">**Example request**</span></span>

<span data-ttu-id="22432-174">Dans cet exemple, nous demandons la liste de sentiments des expressions clés dans les textes suivants :</span><span class="sxs-lookup"><span data-stu-id="22432-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="22432-175">« Nous avons passé un formidable séjour dans cet hôtel, la décoration est exceptionnelle et le personnel très accueillant »</span><span class="sxs-lookup"><span data-stu-id="22432-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="22432-176">« La conférence était exceptionnelle, avec des discussions très intéressantes »</span><span class="sxs-lookup"><span data-stu-id="22432-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="22432-177">« La circulation était horrible, le trajet vers l’aéroport a duré trois heures »</span><span class="sxs-lookup"><span data-stu-id="22432-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="22432-178">Cette requête est effectuée comme un appel POST au point de terminaison :</span><span class="sxs-lookup"><span data-stu-id="22432-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="22432-179">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="22432-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="22432-180">Dans la réponse ci-dessous, vous obtenez la liste des expressions clés associées à vos ID de texte :</span><span class="sxs-lookup"><span data-stu-id="22432-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="22432-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="22432-181">GetLanguageBatch</span></span>

<span data-ttu-id="22432-182">Dans l’appel POST ci-dessous, nous demandons à détecter la langue pour deux entrées de texte :</span><span class="sxs-lookup"><span data-stu-id="22432-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="22432-183">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="22432-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="22432-184">Cet exemple renvoie la réponse suivante, où l’anglais est détecté dans la première entrée et le français dans la seconde entrée :</span><span class="sxs-lookup"><span data-stu-id="22432-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="22432-185">API de détection de la rubrique</span><span class="sxs-lookup"><span data-stu-id="22432-185">Topic Detection APIs</span></span>
<span data-ttu-id="22432-186">Il s’agit d’une API lancée récemment, qui renvoie les premières rubriques détectées pour une liste d’enregistrements texte soumis.</span><span class="sxs-lookup"><span data-stu-id="22432-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="22432-187">Une rubrique est identifiée par une expression clé, représentée par un ou plusieurs mots associés.</span><span class="sxs-lookup"><span data-stu-id="22432-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="22432-188">Notez que cette API facture 1 transaction par enregistrement texte soumis.</span><span class="sxs-lookup"><span data-stu-id="22432-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="22432-189">Cette API nécessite l’envoi d’au moins 100 enregistrements texte, mais elle est conçu pour détecter des rubriques parmi des centaines de milliers d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="22432-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="22432-190">Rubriques – Envoyer le travail</span><span class="sxs-lookup"><span data-stu-id="22432-190">Topics – Submit job</span></span>
<span data-ttu-id="22432-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="22432-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="22432-192">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="22432-192">**Example request**</span></span>

<span data-ttu-id="22432-193">Dans l’appel POST ci-dessous, nous demandons des rubriques pour un ensemble de 100 articles, où les premier et dernier articles d’entrée sont affichés, et deux StopPhrases sont inclus.</span><span class="sxs-lookup"><span data-stu-id="22432-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="22432-194">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="22432-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="22432-195">Dans la réponse ci-dessous, vous obtenez le JobId du travail soumis :</span><span class="sxs-lookup"><span data-stu-id="22432-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="22432-196">Une liste de mots uniques ou de phrases qui ne doivent pas être renvoyés comme des rubriques.</span><span class="sxs-lookup"><span data-stu-id="22432-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="22432-197">Permet de filtrer des rubriques très génériques.</span><span class="sxs-lookup"><span data-stu-id="22432-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="22432-198">Par exemple, dans un jeu de données sur les évaluations d’un hôtel, « hotel » et « hostel » peuvent être des StopPhrases.</span><span class="sxs-lookup"><span data-stu-id="22432-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="22432-199">Rubriques – Recherche des résultats d’un travail</span><span class="sxs-lookup"><span data-stu-id="22432-199">Topics – Poll for job results</span></span>
<span data-ttu-id="22432-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="22432-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="22432-201">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="22432-201">**Example request**</span></span>

<span data-ttu-id="22432-202">Passez le JobId renvoyé à partir de l'étape « Envoyer le travail » pour extraire les résultats.</span><span class="sxs-lookup"><span data-stu-id="22432-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="22432-203">Nous vous recommandons d'appeler ce point de terminaison toutes les minutes jusqu'à ce que la réponse affiche Status=’Complete’.</span><span class="sxs-lookup"><span data-stu-id="22432-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="22432-204">Le travail prendra environ 10 minutes, ou plus pour les travaux impliquant des milliers d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="22432-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="22432-205">Pendant le traitement, la réponse se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="22432-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="22432-206">L'API renvoie un résultat au format JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="22432-206">The API returns output in JSON format in the following format:</span></span>

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


<span data-ttu-id="22432-207">Les propriétés de chaque partie de la réponse sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="22432-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="22432-208">**Propriétés de TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="22432-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="22432-209">Clé</span><span class="sxs-lookup"><span data-stu-id="22432-209">Key</span></span> | <span data-ttu-id="22432-210">Description</span><span class="sxs-lookup"><span data-stu-id="22432-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22432-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="22432-211">TopicId</span></span> |<span data-ttu-id="22432-212">Identificateur unique de chaque rubrique.</span><span class="sxs-lookup"><span data-stu-id="22432-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="22432-213">Score</span><span class="sxs-lookup"><span data-stu-id="22432-213">Score</span></span> |<span data-ttu-id="22432-214">Nombre d’enregistrements affectés à une rubrique.</span><span class="sxs-lookup"><span data-stu-id="22432-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="22432-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="22432-215">KeyPhrase</span></span> |<span data-ttu-id="22432-216">Mot ou phrase résumant la rubrique.</span><span class="sxs-lookup"><span data-stu-id="22432-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="22432-217">Peut contenir un ou plusieurs mots.</span><span class="sxs-lookup"><span data-stu-id="22432-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="22432-218">**Propriétés de TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="22432-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="22432-219">Clé</span><span class="sxs-lookup"><span data-stu-id="22432-219">Key</span></span> | <span data-ttu-id="22432-220">Description</span><span class="sxs-lookup"><span data-stu-id="22432-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22432-221">ID</span><span class="sxs-lookup"><span data-stu-id="22432-221">Id</span></span> |<span data-ttu-id="22432-222">Identificateur de l'enregistrement.</span><span class="sxs-lookup"><span data-stu-id="22432-222">Identifier for the record.</span></span> <span data-ttu-id="22432-223">Équivaut à l'ID inclus dans l'entrée.</span><span class="sxs-lookup"><span data-stu-id="22432-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="22432-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="22432-224">TopicId</span></span> |<span data-ttu-id="22432-225">ID de rubrique auquel l’enregistrement a été affecté.</span><span class="sxs-lookup"><span data-stu-id="22432-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="22432-226">Distance</span><span class="sxs-lookup"><span data-stu-id="22432-226">Distance</span></span> |<span data-ttu-id="22432-227">Niveau de confiance que l’enregistrement appartient à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="22432-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="22432-228">Plus la distance est proche de zéro, plus le niveau de confiance est élevé.</span><span class="sxs-lookup"><span data-stu-id="22432-228">Distance closer to zero indicates higher confidence.</span></span> |

