---
title: "AAA(deprecated) modèle de Cluster - Azure | Documents Microsoft"
description: "(obsolète) Modèle de cluster"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a>(obsolète) Modèle de cluster

> [!NOTE]
> Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée. 
> 
> Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).

Comment nous pouvons pour prédire les groupes de comportements de leur détenteur de crédit dans l’ordre tooreduce hello frais risque d’émetteurs de carte de crédit ? Comment pouvons-nous nous définir des groupes de référence à la personnalité d’employés dans l’ordre tooimprove leurs performances au travail ? Comment les médecins peuvent classifier les patients en groupes basés sur les caractéristiques de leurs diseases hello ? En principe, l’outil d’analyse des clusters permet d’apporter une réponse à toutes ces questions.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

L’analyse des clusters classe un ensemble d’observations en au moins deux groupes inconnus s’excluant mutuellement, en fonction de combinaisons de variables. Hello d’analyse du cluster vise toodiscover un système d’organisation dans des groupes, des observations, généralement des personnes ou leurs caractéristiques, où des membres de groupes de hello partagent des propriétés en commun. Cela [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) utilise hello méthodologie de K-Means, une technique de clustering couramment utilisée, toocluster des données arbitraires dans des groupes. Ce service web prend des données de hello et le nombre de hello de k clusters comme entrée et génère des prédictions qui de hello k groupes toowhich chaque observations appartient. 

> Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple. Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R. Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web. service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.  
> 
> 

## <a name="consumption-of-web-service"></a>Utilisation du service web
Ce service web regroupe les données de hello en un ensemble de k groupes et des sorties hello affectation de groupe pour chaque ligne. service web de Hello attend des données tooinput hello sous forme de chaîne où lignes sont séparées par des virgules (,) et les colonnes sont séparées par des points-virgules ( ;). service web de Hello attend 1 ligne à la fois. Un exemple de jeu de données pourrait ressembler à ceci :

![Exemples de données][1]

Supposons que hello utilisateur souhaité tooseparate ces données en 3 groupes s’excluent mutuellement. Hello des données d’entrée pour hello au-dessus de jeu de données serait suivant de hello : valeur = « 10 ; 5 ; 2,18 ; 1 ; 6,7 ; 5 ; 5,22 ; 3 ; 4,12 ; 2 ; 1,10 ; 3 ; 4 » ; k = « 3 ». sortie de Hello est hello l’appartenance au groupe prévue pour chacune des lignes de hello.

> Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET. 
> 
> 

Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Début du code C# pour l'utilisation du service web :
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a>Création du service web
> Ce service web a été créé à l’aide d’Azure Machine Learning. Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml). Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.
> 
> 

À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux [Execute R Script] [ execute-r-script] extraite de modules sur l’espace de travail hello. schéma de données Hello a été créé avec une simple [Execute R Script][execute-r-script]. Ensuite, schéma de données hello a été lié toohello du cluster modèle, créé à nouveau avec un [Execute R Script][execute-r-script]. Bonjour [Execute R Script] [ execute-r-script] utilisé pour le modèle de cluster hello, hello web service utilise ensuite les fonction hello « k-means », qui est prédéfinie dans hello [Execute R Script] [ execute-r-script] d’Azure Machine Learning.    

![Flux de l’expérience][3]

#### <a name="module-1"></a>Module 1 :
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>Module 2 :
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a>Limitations
Il s'agit d'un exemple très simple de service web de clustering. Comme indiqué à partir du code d’exemple hello ci-dessus, aucune erreur interception n’est implémenté et service de hello suppose que tout est une variable continue (aucune fonctionnalité catégorielles autorisée), comme hello service uniquement les entrées numériques valeurs lors de la création de hello de ce site web hello service. En outre, service de hello gère actuellement taille limitée de données, en raison de la nature de demande/réponse toohello du service web de hello fait appel et hello que hello modèle est en cours correspondre à chaque fois hello web service est appelé. 

## <a name="faq"></a>Forum Aux Questions
Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

