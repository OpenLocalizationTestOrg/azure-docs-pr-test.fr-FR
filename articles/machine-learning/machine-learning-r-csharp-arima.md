---
title: "(déconseillé) Prévisions - Modèle ARIMA (Autoregressive Integrated Moving Average, moyenne mobile intégrée auto-régressive) - Azure | Microsoft Docs"
description: "(déconseillé) Prévisions - Modèle ARIMA (Autoregressive Integrated Moving Average, moyenne mobile intégrée auto-régressive)"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: 1e0d525f-8a9e-4b42-87e0-c9423f059f8c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 4f3af41fd8873fdf75c6426fd395351cb41db190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a>(déconseillé) Prévisions - Modèle ARIMA (Autoregressive Integrated Moving Average, moyenne mobile intégrée auto-régressive)

> [!NOTE]
> Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée. 
> 
> Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).


Cela [service](https://datamarket.azure.com/dataset/aml_labs/arima) implémente des prédictions de tooproduce AUTORÉGRESSIF intégré déplacement moyenne (ARIMA) basées sur des données historiques hello fournies par l’utilisateur de hello. Sera hello à la demande pour une produit spécifique d’augmentation cette année ? Puis-je je prédire Mes ventes de produits pour hello Noël, afin que je peux ainsi planifier efficacement Mon inventaire ? Les modèles de prévision sont tooaddress apt ces questions. Fonction hello au-delà de données, ces modèles examiner les tendances masquées et des tendances futures de saisonnalité toopredict. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple. Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R. Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web. service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.
> 
> 

## <a name="consumption-of-web-service"></a>Utilisation du service web
Ce service accepte des 4 arguments et calcule les prévisions ARIMA hello.
les arguments d’entrée Hello sont :

* Fréquence - indique la fréquence de hello des données brutes de hello (quotidiennes/hebdomadaires/mensuelle/trimestrielle/annuelle).
* Horizon : durée de validité des prévisions
* Date - ajouter dans la nouvelle série de temps hello des données pour le moment.
* La valeur - ajouter des valeurs de données de série hello nouvelle heure.

sortie Hello du service de hello est hello calculé prévision et les valeurs. 

Exemple d'entrée : 

* Frequency : 12
* Horizon : 12
* Date : 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014
* Value : 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509

> Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET. 
> 
> 

Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Début du code C# pour l'utilisation du service web :
    public class Input
    {
        public string frequency;
        public string horizon;
        public string date;
        public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
         byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
         return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }


    void Main()
    {
          var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri =  "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";

          var httpClient = new HttpClient();
           httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere","ChangeToAPIKey");
           httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
          var query = httpClient.PostAsync(acitionUri,new StringContent(json));
          var result = query.Result.Content;
          var scoreResult = result.ReadAsStringAsync().Result;
      }

## <a name="creation-of-web-service"></a>Création du service web
> Ce service web a été créé à l’aide d’Azure Machine Learning. Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml). Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.
> 
> 

Dans Azure Machine Learning, une nouvelle expérience vide a été créée. Des exemples de données d’entrée ont été téléchargés avec un schéma de données prédéfini. Schéma de données toohello lié est un [Execute R Script] [ execute-r-script] module, ce qui génère un modèle de prévision hello ARIMA à l’aide de fonctions 'auto.arima' et 'prévision' à partir de R. 

### <a name="experiment-flow"></a>Flux de l’expérience :
![Create workspace][2]

#### <a name="module-1"></a>Module 1 :
    # Add in hello CSV file with hello data in hello format shown below 
![Create workspace][3]    

#### <a name="module-2"></a>Module 2 :
    # data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- auto.arima(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # produce forecasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a>Limitations
Il s'agit d'un exemple très simple destiné aux prévisions ARIMA. Comme le montre hello exemple de code ci-dessus, aucune interception des erreurs n’est implémenté et service de hello suppose que toutes les variables de hello sont les valeurs continues/positive et la fréquence de hello doit être un entier supérieur à 1. la longueur de vecteurs de valeur de date et hello Hello doit être hello même. variable de date Hello doit respecter toohello format « mm/jj/aaaa ».

## <a name="faq"></a>Forum Aux Questions
Pour les questions fréquemment posées sur la consommation de service web de hello ou toomarketplace de publication, consultez [ici](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

