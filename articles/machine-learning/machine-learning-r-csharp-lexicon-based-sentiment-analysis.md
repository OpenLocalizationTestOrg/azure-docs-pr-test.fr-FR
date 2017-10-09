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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(obsolète) Analyse des sentiments basée sur un lexique

> [!NOTE]
> Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée. 
> 
> Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).

Comment pouvez-vous évaluer les avis et les attitudes des utilisateurs envers des marques ou des rubriques sur les réseaux sociaux en ligne, tels que des publications Facebook, des Tweets, des critiques, etc. ? L’analyse de sentiments fournit une méthode d’analyse de ces questions.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Il existe en général deux méthodes pour l’analyse de sentiments. Une utilise un algorithme d’apprentissage supervisé et hello autres peut être traitée comme apprentissage non supervisé. Un algorithme d’apprentissage supervisé crée généralement un modèle de classification pour les corpus volumineux annotés. Sa précision est principalement basée sur la qualité de l’annotation hello hello, et généralement le processus d’apprentissage hello prendra un certain temps. En outre, lorsque nous appliquons domaine tooanother algorithme hello hello résultat n’est généralement pas correct. Comparées toosupervised l’apprentissage, lexique-apprentissage non supervisé utilise un sentiments du dictionnaire, qui ne nécessite pas le stockage d’un corpus de données de grande taille et de formation - ce qui rend hello ensemble du processus beaucoup plus rapidement. 

Notre [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) repose sur hello MPQA subjectivité lexique (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), qui est un des lexiques de subjectivité hello couramment utilisé. Il existe 5 097 mots négatifs et 2 533 mots positifs dans le MPQA. Par ailleurs, tous ces mots sont annotés avec une polarité forte ou faible. corpus de toute Hello est sous licence publique générale GNU. service web de Hello peut être appliqué tooany phrases, tels que des tweets et les billets de Facebook. 

> Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple. Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R. Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web. service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.
> 
> 

## <a name="consumption-of-web-service"></a>Utilisation du service web
les données d’entrée Hello peuvent être n’importe quel texte, mais hello service web fonctionne mieux avec des phrases. sortie de Hello est une valeur numérique comprise entre -1 et 1. Toute valeur inférieure à 0 indique que sentiment hello du texte hello est négative ; Si elle est positive supérieure 0. valeur absolue de Hello du résultat de hello indique la force de hello de sentiment de hello associé. 

> Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET. 
> 
> 

Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>Début du code C# pour l'utilisation du service web :
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



entrée de Hello est « Aujourd'hui est une bonne journée ». sortie de Hello est « 1 », ce qui indique un sentiments positif associé phrase d’entrée de hello. 

## <a name="creation-of-web-service"></a>Création du service web
> Ce service web a été créé à l’aide d’Azure Machine Learning. Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml). Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.
> 
> 

Dans Azure Machine Learning, une nouvelle expérience vide a été créée. Hello figure ci-dessous flux d’expérience hello d’analyse de sentiments basée sur le lexique. fichier de « sent_dict.csv » Hello est lexique de hello MPQA subjectivité et est défini comme une des entrées hello de [Execute R Script][execute-r-script]. Une autre entrée est une revue échantillonnée hello Amazon révision DataSet pour le test, où nous effectué la sélection, la modification du nom de colonne et opérations de fractionnement. Nous utilisent un lexique subjectivité de hachage package toostore hello dans la mémoire de hello et accélérer le processus de calcul de score hello. intégralité du texte Hello est créée par le package de « tm » et comparé au mot hello dans le dictionnaire de sentiment hello. Enfin, un score est calculé en ajoutant des poids hello de chaque mot subjective dans le texte hello. 

### <a name="experiment-flow"></a>Flux de l’expérience :
![Flux de l’expérience][2]

#### <a name="module-1"></a>Module 1 :
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Installation du package de hachage
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



## <a name="limitations"></a>Limites
Du point de vue de l’algorithme, analyse de sentiments basée sur un lexique est un outil d’analyse de sentiments générales, qui peuvent ne pas offrir de meilleures performances que la méthode de classification hello pour les champs spécifiques. problème de négation Hello n’est pas correctement traité. Nous codons en dur plusieurs négations dans notre programme, mais une meilleure méthode consiste à utiliser un dictionnaire de négations et à créer certaines règles. service web de Hello fonctionne mieux sur les phrases à courts et simples, telles que tweets et les billets de Facebook, que sur des phrases longs et complexes telles que les avis Amazon. 

## <a name="faq"></a>Forum Aux Questions
Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


