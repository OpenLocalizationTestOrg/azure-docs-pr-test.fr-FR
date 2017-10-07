---
title: "capacités de U-SQL cognitifs aaaUsing dans Analytique de LAC de données Azure | Documents Microsoft"
description: "Découvrez comment toouse hello intelligence de fonctionnalités cognitifs U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: 2c9ac71f490e929070fa0e72b93c3ffdb1ab243b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-hello-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="b566e-103">Didacticiel : Prise en main hello cognitifs aux capacités de U-SQL</span><span class="sxs-lookup"><span data-stu-id="b566e-103">Tutorial: Get started with hello Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="b566e-104">Fonctionnalités cognitifs pour U-SQL activer toouse développeurs placer intelligence dans leur programme de données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="b566e-104">Cognitive capabilities for U-SQL enable developers toouse put intelligence in their big data programs.</span></span> <span data-ttu-id="b566e-105">Hello processus global dans simple :</span><span class="sxs-lookup"><span data-stu-id="b566e-105">hello overall process in simple:</span></span>

* <span data-ttu-id="b566e-106">Utiliser les fonctionnalités cognitifs hello de tooenable instruction hello ASSEMBLY de référence pour hello Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="b566e-106">Use hello REFERENCE ASSEMBLY statement tooenable hello cognitive features for hello U-SQL Script</span></span>
* <span data-ttu-id="b566e-107">Appeler une opération de processus hello capacités de troubles cognitifs toouse hello</span><span class="sxs-lookup"><span data-stu-id="b566e-107">Call hello PROCESS operation toouse hello Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="b566e-108">Scénarios d’acquisition d’images</span><span class="sxs-lookup"><span data-stu-id="b566e-108">Imaging scenarios</span></span>

### <a name="example-image-tagging"></a><span data-ttu-id="b566e-109">Exemple : balisage d’images</span><span class="sxs-lookup"><span data-stu-id="b566e-109">Example: Image tagging</span></span>

<span data-ttu-id="b566e-110">Bonjour à l’exemple suivant montre une utilisation de bout en bout de hello imaging objets toodetect de fonctionnalités dans des images.</span><span class="sxs-lookup"><span data-stu-id="b566e-110">hello following example shows an end-to-end use of hello imaging capabilities toodetect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract hello number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="b566e-111">Reconnaissance d’émotions sur des visages humains</span><span class="sxs-lookup"><span data-stu-id="b566e-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="b566e-112">Estimation de l’âge et du sexe de visages humains</span><span class="sxs-lookup"><span data-stu-id="b566e-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="b566e-113">Détection de texte dans des images (OCR)</span><span class="sxs-lookup"><span data-stu-id="b566e-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="b566e-114">Scénarios de texte</span><span class="sxs-lookup"><span data-stu-id="b566e-114">Text scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="b566e-115">Données d’entrée</span><span class="sxs-lookup"><span data-stu-id="b566e-115">Input data</span></span>

<span data-ttu-id="b566e-116">Supposons que nous disposons d’une entrée composée de « Guerre et paix » de Leon Tolstoy.</span><span class="sxs-lookup"><span data-stu-id="b566e-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

    REFERENCE ASSEMBLY [TextCommon];
    REFERENCE ASSEMBLY [TextSentiment];
    REFERENCE ASSEMBLY [TextKeyPhrase];

    @WarAndPeace =
        EXTRACT No int,
                Year string,
                Book string,
                Chapter string,
                Text string
        FROM @"/usqlext/samples/cognition/war_and_peace.csv"
        USING Extractors.Csv();

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="b566e-117">Extraire des expressions clés dans chaque paragraphe</span><span class="sxs-lookup"><span data-stu-id="b566e-117">Extract key phrases for each paragraph</span></span>

    @keyphrase =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                KeyPhrase string
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.KeyPhraseExtractor();

    // Tokenize hello key phrases.
    @kpsplits =
        SELECT No,
            Year,
            Book,
            Chapter,
            Text,
            T.KeyPhrase
        FROM @keyphrase
            CROSS APPLY
                new Cognition.Text.Splitter("KeyPhrase") AS T(KeyPhrase);
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="b566e-118">Effectuer une analyse des sentiments dans chaque paragraphe</span><span class="sxs-lookup"><span data-stu-id="b566e-118">Perform sentiment analysis on each paragraph</span></span>

    @sentiment =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                Sentiment string,
                Conf double
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.SentimentAnalyzer(true);

