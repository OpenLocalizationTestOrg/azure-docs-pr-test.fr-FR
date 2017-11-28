---
title: "(obsolète) Analyse des sentiments basée sur un lexique - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7bc80a1e1067296528eca1a843ea30b0c27af616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="78b6e-103">(obsolète) Analyse des sentiments basée sur un lexique</span><span class="sxs-lookup"><span data-stu-id="78b6e-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="78b6e-104">Microsoft DataMarket va être supprimé et cette API est désormais obsolète.</span><span class="sxs-lookup"><span data-stu-id="78b6e-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="78b6e-105">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="78b6e-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="78b6e-106">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="78b6e-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="78b6e-107">Comment pouvez-vous évaluer les avis et les attitudes des utilisateurs envers des marques ou des rubriques sur les réseaux sociaux en ligne, tels que des publications Facebook, des Tweets, des critiques, etc. ?</span><span class="sxs-lookup"><span data-stu-id="78b6e-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="78b6e-108">L’analyse de sentiments fournit une méthode d’analyse de ces questions.</span><span class="sxs-lookup"><span data-stu-id="78b6e-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="78b6e-109">Il existe en général deux méthodes pour l’analyse de sentiments.</span><span class="sxs-lookup"><span data-stu-id="78b6e-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="78b6e-110">L’une utilise un algorithme d’apprentissage supervisé et l’autre peut être traitée comme un apprentissage non supervisé.</span><span class="sxs-lookup"><span data-stu-id="78b6e-110">One is using a supervised learning algorithm, and the other can be treated as unsupervised learning.</span></span> <span data-ttu-id="78b6e-111">Un algorithme d’apprentissage supervisé crée généralement un modèle de classification pour les corpus volumineux annotés.</span><span class="sxs-lookup"><span data-stu-id="78b6e-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="78b6e-112">Sa précision est principalement basée sur la qualité de l’annotation et la phase d’apprentissage prend généralement beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="78b6e-112">Its accuracy is mainly based on the quality of the annotation, and usually the training process will take a long time.</span></span> <span data-ttu-id="78b6e-113">En outre, lorsque nous appliquons l'algorithme à un autre domaine, le résultat n'est généralement pas bon.</span><span class="sxs-lookup"><span data-stu-id="78b6e-113">Besides that, when we apply the algorithm to another domain, the result is usually not good.</span></span> <span data-ttu-id="78b6e-114">Par rapport à l’apprentissage supervisé, l’apprentissage non supervisé basé sur un lexique utilise un dictionnaire de sentiments, qui ne nécessite pas le stockage d’un corpus de données volumineux et de formation, ce qui permet d’accélérer considérablement l’ensemble du processus.</span><span class="sxs-lookup"><span data-stu-id="78b6e-114">Compared to supervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes the whole process much faster.</span></span> 

<span data-ttu-id="78b6e-115">Notre [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) repose sur le lexique MPQA (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), qui est l’un des lexiques de subjectivité les plus fréquemment utilisés.</span><span class="sxs-lookup"><span data-stu-id="78b6e-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on the MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of the most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="78b6e-116">Il existe 5 097 mots négatifs et 2 533 mots positifs dans le MPQA.</span><span class="sxs-lookup"><span data-stu-id="78b6e-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="78b6e-117">Par ailleurs, tous ces mots sont annotés avec une polarité forte ou faible.</span><span class="sxs-lookup"><span data-stu-id="78b6e-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="78b6e-118">Le corpus entier fait l'objet d'une licence GPL GNU.</span><span class="sxs-lookup"><span data-stu-id="78b6e-118">The whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="78b6e-119">Le service web peut être utilisé pour toutes les phrases courtes telles que les Tweets et les publications Facebook.</span><span class="sxs-lookup"><span data-stu-id="78b6e-119">The web service can be applied to any short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="78b6e-120">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="78b6e-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="78b6e-121">Mais l’objectif du service web est également de servir d’exemple d’utilisation d’Azure Machine Learning pour créer des services web avec le code R.</span><span class="sxs-lookup"><span data-stu-id="78b6e-121">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="78b6e-122">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="78b6e-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="78b6e-123">Le service web peut ensuite être publié sur Azure Marketplace afin que les utilisateurs et les appareils du monde entier l’utilisent sans que l’auteur du service web n’ait à configurer l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="78b6e-123">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="78b6e-124">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="78b6e-124">Consumption of web service</span></span>
<span data-ttu-id="78b6e-125">Les données en entrée peuvent correspondre à n'importe quel texte, mais le service web fonctionne mieux avec des phrases courtes.</span><span class="sxs-lookup"><span data-stu-id="78b6e-125">The input data can be any text, but the web service works better with short sentences.</span></span> <span data-ttu-id="78b6e-126">Le résultat est une valeur numérique comprise entre -1 et 1.</span><span class="sxs-lookup"><span data-stu-id="78b6e-126">The output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="78b6e-127">Toute valeur inférieure à 0 indique que le sentiment à l’égard du texte est négatif, il est positif si la valeur est supérieure à 0.</span><span class="sxs-lookup"><span data-stu-id="78b6e-127">Any value below 0 denotes that the sentiment of the text is negative; positive if above 0.</span></span> <span data-ttu-id="78b6e-128">La valeur absolue du résultat indique la puissance du sentiment associé.</span><span class="sxs-lookup"><span data-stu-id="78b6e-128">The absolute value of the result denotes the strength of the associated sentiment.</span></span> 

> <span data-ttu-id="78b6e-129">Étant hébergé sur Azure Marketplace, ce service est un service OData. Il peut être appelé à l’aide des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="78b6e-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="78b6e-130">Il existe plusieurs façons d’utiliser le service de manière automatique (un exemple d’application est disponible [ici](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="78b6e-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="78b6e-131">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="78b6e-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="78b6e-132">L’entrée est la suivante : « Aujourd’hui est une belle journée. ».</span><span class="sxs-lookup"><span data-stu-id="78b6e-132">The input is “Today is a good day.”</span></span> <span data-ttu-id="78b6e-133">Le résultat est « 1 », ce qui indique un sentiment positif associé à la phrase en entrée.</span><span class="sxs-lookup"><span data-stu-id="78b6e-133">The output is “1”, which indicates a positive sentiment associated with the input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="78b6e-134">Création du service web</span><span class="sxs-lookup"><span data-stu-id="78b6e-134">Creation of web service</span></span>
> <span data-ttu-id="78b6e-135">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="78b6e-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="78b6e-136">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="78b6e-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="78b6e-137">Voici une capture d'écran de l'expérience qui a créé le service web et l'exemple de code pour chacun des modules dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="78b6e-137">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="78b6e-138">Dans Azure Machine Learning, une nouvelle expérience vide a été créée.</span><span class="sxs-lookup"><span data-stu-id="78b6e-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="78b6e-139">La figure ci-dessous illustre le flux d’expérience pour l’analyse de sentiments basée sur un lexique.</span><span class="sxs-lookup"><span data-stu-id="78b6e-139">The figure below shows the experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="78b6e-140">Le fichier « sent_dict.csv » correspond au lexique de subjectivité MPQA ; il est défini en tant que l’une des entrées du module [Exécuter le script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="78b6e-140">The “sent_dict.csv” file is the MPQA subjectivity lexicon, and is set as one of the inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="78b6e-141">Une autre entrée correspond à une critique partielle provenant du jeu de données des critiques Amazon à des fins de test, dans laquelle nous avons effectué des opérations de sélection, de modification des noms de colonne et de fractionnement.</span><span class="sxs-lookup"><span data-stu-id="78b6e-141">Another input is a sampled review from the Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="78b6e-142">Nous utilisons un package de hachage pour stocker le lexique de subjectivité en mémoire et accélérer le processus de calcul du score.</span><span class="sxs-lookup"><span data-stu-id="78b6e-142">We use a hash package to store the subjectivity lexicon in the memory and accelerate the score computation process.</span></span> <span data-ttu-id="78b6e-143">L'ensemble du texte sera converti en jetons par le package « tm » et comparé au mot dans le dictionnaire de sentiments.</span><span class="sxs-lookup"><span data-stu-id="78b6e-143">The whole text will be tokenized by “tm” package and compared with the word in the sentiment dictionary.</span></span> <span data-ttu-id="78b6e-144">Enfin, un score sera calculé en ajoutant le poids de chaque mot subjectif dans le texte.</span><span class="sxs-lookup"><span data-stu-id="78b6e-144">Finally, a score will be calculated by adding the weight of each subjective word in the text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="78b6e-145">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="78b6e-145">Experiment flow:</span></span>
![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="78b6e-147">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="78b6e-147">Module 1:</span></span>
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="78b6e-148">Installation du package de hachage</span><span class="sxs-lookup"><span data-stu-id="78b6e-148">Install hash package</span></span>
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="78b6e-149">Limitations</span><span class="sxs-lookup"><span data-stu-id="78b6e-149">Limitations</span></span>
<span data-ttu-id="78b6e-150">Du point de vue d’un algorithme, l’analyse de sentiments basée sur un lexique est un outil général d’analyse de sentiments qui peut ne pas être plus performant que la méthode de classification pour des champs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="78b6e-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than the classification method for specific fields.</span></span> <span data-ttu-id="78b6e-151">Le problème de la négation n'est pas correctement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="78b6e-151">The negation problem is not well dealt with.</span></span> <span data-ttu-id="78b6e-152">Nous codons en dur plusieurs négations dans notre programme, mais une meilleure méthode consiste à utiliser un dictionnaire de négations et à créer certaines règles.</span><span class="sxs-lookup"><span data-stu-id="78b6e-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="78b6e-153">Le service web fonctionne mieux avec des phrases courtes et simples, telles que les Tweets et les publications Facebook, qu’avec les phrases longues et complexes, telles que les critiques Amazon.</span><span class="sxs-lookup"><span data-stu-id="78b6e-153">The web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="78b6e-154">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="78b6e-154">FAQ</span></span>
<span data-ttu-id="78b6e-155">Pour les questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Azure Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="78b6e-155">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


