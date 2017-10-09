---
title: "AAA(deprecated) analyse des sentiments basée lexique - Azure | Documents Microsoft"
description: "(obsolète) Analyse des sentiments basée sur un lexique"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="7f2ee-103">(obsolète) Analyse des sentiments basée sur un lexique</span><span class="sxs-lookup"><span data-stu-id="7f2ee-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="7f2ee-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="7f2ee-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="7f2ee-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="7f2ee-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="7f2ee-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="7f2ee-107">Comment pouvez-vous évaluer les avis et les attitudes des utilisateurs envers des marques ou des rubriques sur les réseaux sociaux en ligne, tels que des publications Facebook, des Tweets, des critiques, etc. ?</span><span class="sxs-lookup"><span data-stu-id="7f2ee-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="7f2ee-108">L’analyse de sentiments fournit une méthode d’analyse de ces questions.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="7f2ee-109">Il existe en général deux méthodes pour l’analyse de sentiments.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="7f2ee-110">Une utilise un algorithme d’apprentissage supervisé et hello autres peut être traitée comme apprentissage non supervisé.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="7f2ee-111">Un algorithme d’apprentissage supervisé crée généralement un modèle de classification pour les corpus volumineux annotés.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="7f2ee-112">Sa précision est principalement basée sur la qualité de l’annotation hello hello, et généralement le processus d’apprentissage hello prendra un certain temps.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="7f2ee-113">En outre, lorsque nous appliquons domaine tooanother algorithme hello hello résultat n’est généralement pas correct.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="7f2ee-114">Comparées toosupervised l’apprentissage, lexique-apprentissage non supervisé utilise un sentiments du dictionnaire, qui ne nécessite pas le stockage d’un corpus de données de grande taille et de formation - ce qui rend hello ensemble du processus beaucoup plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="7f2ee-115">Notre [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) repose sur hello MPQA subjectivité lexique (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), qui est un des lexiques de subjectivité hello couramment utilisé.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="7f2ee-116">Il existe 5 097 mots négatifs et 2 533 mots positifs dans le MPQA.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="7f2ee-117">Par ailleurs, tous ces mots sont annotés avec une polarité forte ou faible.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="7f2ee-118">corpus de toute Hello est sous licence publique générale GNU.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="7f2ee-119">service web de Hello peut être appliqué tooany phrases, tels que des tweets et les billets de Facebook.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="7f2ee-120">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="7f2ee-121">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="7f2ee-122">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="7f2ee-123">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="7f2ee-124">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="7f2ee-124">Consumption of web service</span></span>
<span data-ttu-id="7f2ee-125">les données d’entrée Hello peuvent être n’importe quel texte, mais hello service web fonctionne mieux avec des phrases.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="7f2ee-126">sortie de Hello est une valeur numérique comprise entre -1 et 1.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="7f2ee-127">Toute valeur inférieure à 0 indique que sentiment hello du texte hello est négative ; Si elle est positive supérieure 0.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="7f2ee-128">valeur absolue de Hello du résultat de hello indique la force de hello de sentiment de hello associé.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="7f2ee-129">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="7f2ee-130">Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="7f2ee-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="7f2ee-131">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="7f2ee-131">Starting C# code for web service consumption:</span></span>
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



<span data-ttu-id="7f2ee-132">entrée de Hello est « Aujourd'hui est une bonne journée ».</span><span class="sxs-lookup"><span data-stu-id="7f2ee-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="7f2ee-133">sortie de Hello est « 1 », ce qui indique un sentiments positif associé phrase d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="7f2ee-134">Création du service web</span><span class="sxs-lookup"><span data-stu-id="7f2ee-134">Creation of web service</span></span>
> <span data-ttu-id="7f2ee-135">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="7f2ee-136">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="7f2ee-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="7f2ee-137">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="7f2ee-138">Dans Azure Machine Learning, une nouvelle expérience vide a été créée.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="7f2ee-139">Hello figure ci-dessous flux d’expérience hello d’analyse de sentiments basée sur le lexique.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="7f2ee-140">fichier de « sent_dict.csv » Hello est lexique de hello MPQA subjectivité et est défini comme une des entrées hello de [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="7f2ee-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="7f2ee-141">Une autre entrée est une revue échantillonnée hello Amazon révision DataSet pour le test, où nous effectué la sélection, la modification du nom de colonne et opérations de fractionnement.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="7f2ee-142">Nous utilisent un lexique subjectivité de hachage package toostore hello dans la mémoire de hello et accélérer le processus de calcul de score hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="7f2ee-143">intégralité du texte Hello est créée par le package de « tm » et comparé au mot hello dans le dictionnaire de sentiment hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="7f2ee-144">Enfin, un score est calculé en ajoutant des poids hello de chaque mot subjective dans le texte hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="7f2ee-145">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="7f2ee-145">Experiment flow:</span></span>
![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="7f2ee-147">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="7f2ee-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="7f2ee-148">Installation du package de hachage</span><span class="sxs-lookup"><span data-stu-id="7f2ee-148">Install hash package</span></span>
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="7f2ee-149">Limites</span><span class="sxs-lookup"><span data-stu-id="7f2ee-149">Limitations</span></span>
<span data-ttu-id="7f2ee-150">Du point de vue de l’algorithme, analyse de sentiments basée sur un lexique est un outil d’analyse de sentiments générales, qui peuvent ne pas offrir de meilleures performances que la méthode de classification hello pour les champs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="7f2ee-151">problème de négation Hello n’est pas correctement traité.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="7f2ee-152">Nous codons en dur plusieurs négations dans notre programme, mais une meilleure méthode consiste à utiliser un dictionnaire de négations et à créer certaines règles.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="7f2ee-153">service web de Hello fonctionne mieux sur les phrases à courts et simples, telles que tweets et les billets de Facebook, que sur des phrases longs et complexes telles que les avis Amazon.</span><span class="sxs-lookup"><span data-stu-id="7f2ee-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="7f2ee-154">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="7f2ee-154">FAQ</span></span>
<span data-ttu-id="7f2ee-155">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="7f2ee-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


