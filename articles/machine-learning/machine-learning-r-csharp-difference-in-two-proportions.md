---
title: "AAA(deprecated) différence dans les Proportions Test - Azure | Documents Microsoft"
description: "(obsolète) Test de différence des proportions"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a>(obsolète) Test de différence des proportions

> [!NOTE]
> Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée. 
> 
> Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).

Deux proportions sont-elles différentes d'un point de vue statistique ? Supposons qu’un utilisateur souhaite toocompare deux films toodetermine si un nombre beaucoup plus élevé d’un film « aime » lorsque comparées toohello autres. Avec un exemple de grande taille, il peut y avoir une différence statistiquement significative entre des proportions hello 0,50 et 0.51. Avec un petit échantillon, il peut-être pas suffisamment toodetermine de données si ces proportions sont réellement différentes. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Cela [service web](https://datamarket.azure.com/dataset/aml_labs/prop_test) effectue un test d’hypothèse de différence hello dans des deux proportions en fonction de l’entrée d’utilisateur de nombre hello de succès et le nombre total de hello d’essais pour les groupes de comparaison hello 2. Dans un scénario possible, ce service web peut être appelé à partir d’au sein d’une application de comparaison de film, indiquant les utilisateur hello si un des films de hello est vraiment 'aimé' plus souvent que hello autre, en fonction de classification des films.

> Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple. Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R. Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web. service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.
> 
> 

## <a name="consumption-of-web-service"></a>Utilisation du service web
Ce service accepte 4 arguments et effectue un test d'hypothèse des proportions.

les arguments d’entrée Hello sont :

* Successes1 : nombre d’événements de succès dans l’échantillon 1
* Successes2 : nombre d’événements de succès dans l’échantillon 2
* Total1 - taille de l’échantillon 1.
* Total2 : taille de l’échantillon 2

sortie Hello du service de hello résulte de hello d’hypothèse de hello avec hello appel statistique, df, p-valeur de test et proportion dans les limites du 1/2 et l’intervalle de confiance exemple.

> Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET. 
> 
> 

Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Début du code C# pour l'utilisation du service web :
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
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

À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée avec deux modules [Exécuter le script R][execute-r-script]. Dans le module de première hello schéma de données hello est défini, que la deuxième du module hello utilise commande hello prop.test test d’hypothèse R tooperform hello pour 2 proportions. 

### <a name="experiment-flow"></a>Flux de l’expérience :
![Flux de l’expérience][2]

#### <a name="module-1"></a>Module 1 :
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Module 2 :
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a>Limitations
Il s’agit d’un exemple très simple permettant de tester la différence dans 2 proportions. Comme indiqué à partir du code d’exemple hello ci-dessus, aucune erreur interception n’est implémenté et service de hello suppose que toutes les variables de hello sont continues.

## <a name="faq"></a>Forum Aux Questions
Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

