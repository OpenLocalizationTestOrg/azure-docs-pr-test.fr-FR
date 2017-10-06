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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="f9b04-103">API Machine Learning : analyse de texte pour déterminer les sentiments, l’extraction d’expressions clés, la détection de la langue et la détection de la rubrique</span><span class="sxs-lookup"><span data-stu-id="f9b04-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="f9b04-104">Ce guide est pour la version 1 de hello API.</span><span class="sxs-lookup"><span data-stu-id="f9b04-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="f9b04-105">Pour la version 2, [ **toothis document de référence**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="f9b04-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="f9b04-106">Version 2 correspond désormais hello par défaut de cette API.</span><span class="sxs-lookup"><span data-stu-id="f9b04-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="f9b04-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f9b04-107">Overview</span></span>
<span data-ttu-id="f9b04-108">Hello texte Analytique API est une suite d’analytique de texte [services web](https://datamarket.azure.com/dataset/amla/text-analytics) intègrent Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f9b04-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="f9b04-109">Hello API peut être utilisé tooanalyze texte non structuré pour des tâches telles que l’analyse des sentiments, extraction d’expressions clés, détection de la langue et détection de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="f9b04-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="f9b04-110">Aucune données de formation ne nécessaire toouse cette API : simplement mettre vos données de texte.</span><span class="sxs-lookup"><span data-stu-id="f9b04-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="f9b04-111">Cette API utilise un langage naturel avancé traitement toodeliver de techniques dans les prédictions de classe.</span><span class="sxs-lookup"><span data-stu-id="f9b04-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="f9b04-112">Vous pouvez voir analytique de texte dans une action sur notre [site de démonstration](https://text-analytics-demo.azurewebsites.net/), où vous trouverez également [exemples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sur l’analytique de texte tooimplement en c# et Python.</span><span class="sxs-lookup"><span data-stu-id="f9b04-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="f9b04-113">analyse de sentiments</span><span class="sxs-lookup"><span data-stu-id="f9b04-113">Sentiment analysis</span></span>
<span data-ttu-id="f9b04-114">Hello API retourne un score entre 0 et 1.</span><span class="sxs-lookup"><span data-stu-id="f9b04-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="f9b04-115">Too1 fermer des scores indiquent sentiment positif, alors que too0 fermer des scores négatifs sentiments.</span><span class="sxs-lookup"><span data-stu-id="f9b04-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="f9b04-116">La valeur de notation du sentiment est générée via des techniques de classification.</span><span class="sxs-lookup"><span data-stu-id="f9b04-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="f9b04-117">Hello des fonctionnalités d’entrée toohello classifieur incluent n-grammes, fonctionnalités générées à partir de morphosyntaxique balises et incorporations de word.</span><span class="sxs-lookup"><span data-stu-id="f9b04-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="f9b04-118">Actuellement, l’anglais est hello uniquement prise en charge de langue.</span><span class="sxs-lookup"><span data-stu-id="f9b04-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="f9b04-119">Extraction d’expressions clés</span><span class="sxs-lookup"><span data-stu-id="f9b04-119">Key phrase extraction</span></span>
<span data-ttu-id="f9b04-120">Hello API retourne une liste de chaînes qui désigne les points de discussion clé hello dans le texte d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="f9b04-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="f9b04-121">Nous utilisons des techniques fournies par la boîte à outils de traitement du langage naturel sophistiquée de Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="f9b04-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="f9b04-122">Actuellement, l’anglais est hello uniquement prise en charge de langue.</span><span class="sxs-lookup"><span data-stu-id="f9b04-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="f9b04-123">Détection de la langue</span><span class="sxs-lookup"><span data-stu-id="f9b04-123">Language detection</span></span>
<span data-ttu-id="f9b04-124">Hello API renvoie hello a détecté la langue et un score entre 0 et 1.</span><span class="sxs-lookup"><span data-stu-id="f9b04-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="f9b04-125">Too1 fermer des scores indiquent la certitude de 100 % language de hello identifié a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="f9b04-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="f9b04-126">Au total, 120 langues sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="f9b04-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="f9b04-127">Détection de la rubrique</span><span class="sxs-lookup"><span data-stu-id="f9b04-127">Topic detection</span></span>
<span data-ttu-id="f9b04-128">Il s’agit d’une API qui vient d’être publiée qui retourne les rubriques de détectés supérieur hello pour une liste des enregistrements texte envoyé.</span><span class="sxs-lookup"><span data-stu-id="f9b04-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="f9b04-129">Une rubrique est identifiée par une expression clé, représentée par un ou plusieurs mots associés.</span><span class="sxs-lookup"><span data-stu-id="f9b04-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="f9b04-130">Cette API requiert un minimum de 100 texte enregistre toobe soumis, mais est conçue toodetect rubriques sur des centaines toothousands d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="f9b04-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="f9b04-131">Notez que cette API facture 1 transaction par enregistrement texte soumis.</span><span class="sxs-lookup"><span data-stu-id="f9b04-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="f9b04-132">Hello API est toowork conçue pour humaines court, écrit du texte tels que les révisions et les commentaires des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f9b04-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="f9b04-133">Définition de l’API</span><span class="sxs-lookup"><span data-stu-id="f9b04-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="f9b04-134">headers</span><span class="sxs-lookup"><span data-stu-id="f9b04-134">Headers</span></span>
<span data-ttu-id="f9b04-135">Veillez à inclure les en-têtes correct hello dans votre demande, qui doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9b04-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="f9b04-136">Vous pouvez trouver votre clé de compte dans votre compte Bonjour [Azure Data Market](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="f9b04-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="f9b04-137">Actuellement, seul JSON est accepté pour les formats d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="f9b04-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="f9b04-138">XML n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f9b04-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="f9b04-139">API à réponse unique</span><span class="sxs-lookup"><span data-stu-id="f9b04-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="f9b04-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="f9b04-140">GetSentiment</span></span>
<span data-ttu-id="f9b04-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="f9b04-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="f9b04-142">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="f9b04-142">**Example request**</span></span>

<span data-ttu-id="f9b04-143">Dans l’appel hello ci-dessous, nous invitons analyse des sentiments pour la phrase de hello « Hello World » :</span><span class="sxs-lookup"><span data-stu-id="f9b04-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="f9b04-144">Cette requête renverra une réponse du type :</span><span class="sxs-lookup"><span data-stu-id="f9b04-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="f9b04-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="f9b04-145">GetKeyPhrases</span></span>
<span data-ttu-id="f9b04-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="f9b04-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="f9b04-147">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="f9b04-147">**Example request**</span></span>

<span data-ttu-id="f9b04-148">Dans l’appel hello ci-dessous, nous invitons les expressions clés hello trouvée dans le texte hello « Il était un toostay hôtel merveilleux au, avec décor unique et convivial » :</span><span class="sxs-lookup"><span data-stu-id="f9b04-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="f9b04-149">Cette requête renverra une réponse du type :</span><span class="sxs-lookup"><span data-stu-id="f9b04-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="f9b04-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="f9b04-150">GetLanguage</span></span>
<span data-ttu-id="f9b04-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="f9b04-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="f9b04-152">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="f9b04-152">**Example request**</span></span>

<span data-ttu-id="f9b04-153">Dans l’appel GET hello ci-dessous, nous invitons pour sentiment hello pour les expressions clés de hello dans le texte hello *Hello World*</span><span class="sxs-lookup"><span data-stu-id="f9b04-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="f9b04-154">Cette requête renverra une réponse du type :</span><span class="sxs-lookup"><span data-stu-id="f9b04-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="f9b04-155">**Paramètres facultatifs**</span><span class="sxs-lookup"><span data-stu-id="f9b04-155">**Optional parameters**</span></span>

<span data-ttu-id="f9b04-156">`NumberOfLanguagesToDetect` est un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="f9b04-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="f9b04-157">valeur par défaut Hello est 1.</span><span class="sxs-lookup"><span data-stu-id="f9b04-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="f9b04-158">API Batch</span><span class="sxs-lookup"><span data-stu-id="f9b04-158">Batch APIs</span></span>
<span data-ttu-id="f9b04-159">Hello service de texte Analytique permet de vous sentiment de toodo et les extractions de phrase clé en mode batch.</span><span class="sxs-lookup"><span data-stu-id="f9b04-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="f9b04-160">Notez que chacun des enregistrements de hello transformée nombres comme une transaction.</span><span class="sxs-lookup"><span data-stu-id="f9b04-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="f9b04-161">Par exemple, si vous demandez le sentiment pour 1 000 enregistrements en un seul appel, 1 000 transactions sont déduites.</span><span class="sxs-lookup"><span data-stu-id="f9b04-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="f9b04-162">Notez que les identificateurs hello entrés dans le système de hello sont ID hello retournés par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b04-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="f9b04-163">service web de Hello ne vérifie pas que ces ID est uniques.</span><span class="sxs-lookup"><span data-stu-id="f9b04-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="f9b04-164">Il incombe hello d’unicité de tooverify hello appelant.</span><span class="sxs-lookup"><span data-stu-id="f9b04-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="f9b04-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="f9b04-165">GetSentimentBatch</span></span>
<span data-ttu-id="f9b04-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="f9b04-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="f9b04-167">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="f9b04-167">**Example request**</span></span>

<span data-ttu-id="f9b04-168">Bonjour POST appeler ci-dessous, nous invitons pour les éléments hello d’expressions hello « Hello World », « Hello World de Foo » et « Mes Bonjour » dans le corps hello de demande de hello :</span><span class="sxs-lookup"><span data-stu-id="f9b04-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="f9b04-169">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="f9b04-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="f9b04-170">Dans la réponse de hello ci-dessous, vous obtenez la liste hello des scores associé à votre ID de texte :</span><span class="sxs-lookup"><span data-stu-id="f9b04-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="f9b04-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="f9b04-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="f9b04-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="f9b04-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="f9b04-173">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="f9b04-173">**Example request**</span></span>

<span data-ttu-id="f9b04-174">Dans cet exemple, nous invitons pour la liste d’éléments pour des expressions clés hello Bonjour suivant textes hello :</span><span class="sxs-lookup"><span data-stu-id="f9b04-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="f9b04-175">« Il était un toostay hôtel merveilleux au, avec décor unique et convivial »</span><span class="sxs-lookup"><span data-stu-id="f9b04-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="f9b04-176">« La conférence était exceptionnelle, avec des discussions très intéressantes »</span><span class="sxs-lookup"><span data-stu-id="f9b04-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="f9b04-177">« le trafic de hello a été horribles, j’ai passé à trois heures va toohello aéroport »</span><span class="sxs-lookup"><span data-stu-id="f9b04-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="f9b04-178">Cette demande est effectuée en tant qu’un point de terminaison du toohello appel POST :</span><span class="sxs-lookup"><span data-stu-id="f9b04-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="f9b04-179">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="f9b04-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="f9b04-180">Dans la réponse de hello ci-dessous, vous obtenez la liste hello des expressions clés associées à votre ID de texte :</span><span class="sxs-lookup"><span data-stu-id="f9b04-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="f9b04-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="f9b04-181">GetLanguageBatch</span></span>

<span data-ttu-id="f9b04-182">Dans l’appel POST hello ci-dessous, nous invitons détection de la langue pour les deux entrées de texte :</span><span class="sxs-lookup"><span data-stu-id="f9b04-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="f9b04-183">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="f9b04-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="f9b04-184">Cet exemple renvoie hello suivant réponse, où anglais est détectée dans la première entrée de hello et Français dans la deuxième entrée du hello :</span><span class="sxs-lookup"><span data-stu-id="f9b04-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="f9b04-185">API de détection de la rubrique</span><span class="sxs-lookup"><span data-stu-id="f9b04-185">Topic Detection APIs</span></span>
<span data-ttu-id="f9b04-186">Il s’agit d’une API qui vient d’être publiée qui retourne les rubriques de détectés supérieur hello pour une liste des enregistrements texte envoyé.</span><span class="sxs-lookup"><span data-stu-id="f9b04-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="f9b04-187">Une rubrique est identifiée par une expression clé, représentée par un ou plusieurs mots associés.</span><span class="sxs-lookup"><span data-stu-id="f9b04-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="f9b04-188">Notez que cette API facture 1 transaction par enregistrement texte soumis.</span><span class="sxs-lookup"><span data-stu-id="f9b04-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="f9b04-189">Cette API requiert un minimum de 100 texte enregistre toobe soumis, mais est conçue toodetect rubriques sur des centaines toothousands d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="f9b04-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="f9b04-190">Rubriques – Envoyer le travail</span><span class="sxs-lookup"><span data-stu-id="f9b04-190">Topics – Submit job</span></span>
<span data-ttu-id="f9b04-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="f9b04-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="f9b04-192">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="f9b04-192">**Example request**</span></span>

<span data-ttu-id="f9b04-193">Dans l’appel POST hello ci-dessous, nous invitons les rubriques pour un ensemble de 100 articles, où hello et prénom d’entrée articles sont affichés, et deux StopPhrases sont inclus.</span><span class="sxs-lookup"><span data-stu-id="f9b04-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="f9b04-194">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="f9b04-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="f9b04-195">Dans la réponse de hello ci-dessous, vous obtenez hello JobId pour les travaux soumis hello :</span><span class="sxs-lookup"><span data-stu-id="f9b04-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="f9b04-196">Une liste de mots uniques ou de phrases qui ne doivent pas être renvoyés comme des rubriques.</span><span class="sxs-lookup"><span data-stu-id="f9b04-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="f9b04-197">Peut être utilisé toofilter rubriques très générique.</span><span class="sxs-lookup"><span data-stu-id="f9b04-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="f9b04-198">Par exemple, dans un jeu de données sur les évaluations d’un hôtel, « hotel » et « hostel » peuvent être des StopPhrases.</span><span class="sxs-lookup"><span data-stu-id="f9b04-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="f9b04-199">Rubriques – Recherche des résultats d’un travail</span><span class="sxs-lookup"><span data-stu-id="f9b04-199">Topics – Poll for job results</span></span>
<span data-ttu-id="f9b04-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="f9b04-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="f9b04-201">**Exemple de demande**</span><span class="sxs-lookup"><span data-stu-id="f9b04-201">**Example request**</span></span>

<span data-ttu-id="f9b04-202">Passez hello que JobID retourné à partir des résultats de hello 'job Submit' étape toofetch hello.</span><span class="sxs-lookup"><span data-stu-id="f9b04-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="f9b04-203">Nous vous recommandons d’appeler ce point de terminaison toutes les minutes jusqu'à ce que l’état = 'Terminé' dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b04-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="f9b04-204">Elle prendra environ 10 minutes pour un travail toocomplete, ou plus pour les travaux avec des milliers d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="f9b04-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="f9b04-205">Pendant son traitement, réponse de hello seront comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9b04-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="f9b04-206">Hello API retourne la sortie au format JSON Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="f9b04-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="f9b04-207">propriétés Hello pour chaque partie de la réponse de hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9b04-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="f9b04-208">**Propriétés de TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="f9b04-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="f9b04-209">Clé</span><span class="sxs-lookup"><span data-stu-id="f9b04-209">Key</span></span> | <span data-ttu-id="f9b04-210">Description</span><span class="sxs-lookup"><span data-stu-id="f9b04-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f9b04-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="f9b04-211">TopicId</span></span> |<span data-ttu-id="f9b04-212">Identificateur unique de chaque rubrique.</span><span class="sxs-lookup"><span data-stu-id="f9b04-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="f9b04-213">Score</span><span class="sxs-lookup"><span data-stu-id="f9b04-213">Score</span></span> |<span data-ttu-id="f9b04-214">Nombre d’enregistrements assigné tootopic.</span><span class="sxs-lookup"><span data-stu-id="f9b04-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="f9b04-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="f9b04-215">KeyPhrase</span></span> |<span data-ttu-id="f9b04-216">Un mot ou une expression pour une rubrique de hello résumer.</span><span class="sxs-lookup"><span data-stu-id="f9b04-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="f9b04-217">Peut contenir un ou plusieurs mots.</span><span class="sxs-lookup"><span data-stu-id="f9b04-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="f9b04-218">**Propriétés de TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="f9b04-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="f9b04-219">Clé</span><span class="sxs-lookup"><span data-stu-id="f9b04-219">Key</span></span> | <span data-ttu-id="f9b04-220">Description</span><span class="sxs-lookup"><span data-stu-id="f9b04-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f9b04-221">Id</span><span class="sxs-lookup"><span data-stu-id="f9b04-221">Id</span></span> |<span data-ttu-id="f9b04-222">Identificateur de l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b04-222">Identifier for hello record.</span></span> <span data-ttu-id="f9b04-223">Attribue un ID toohello inclus dans l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b04-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="f9b04-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="f9b04-224">TopicId</span></span> |<span data-ttu-id="f9b04-225">ID de rubrique Hello enregistrement hello a été affectée.</span><span class="sxs-lookup"><span data-stu-id="f9b04-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="f9b04-226">Distance</span><span class="sxs-lookup"><span data-stu-id="f9b04-226">Distance</span></span> |<span data-ttu-id="f9b04-227">Confiance hello enregistrement appartient toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="f9b04-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="f9b04-228">Toozero de plus près de distance indique toute confiance.</span><span class="sxs-lookup"><span data-stu-id="f9b04-228">Distance closer toozero indicates higher confidence.</span></span> |

