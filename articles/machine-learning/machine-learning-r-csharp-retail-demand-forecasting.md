---
title: AAA(deprecated) Forecasting - ETS + STL - Azure | Documents Microsoft
description: "(obsolète) Prévisions - ETS + STL"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
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
ms.openlocfilehash: 550d423898d46564936fdcfbf05b7c88d2e292c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---ets--stl"></a><span data-ttu-id="29641-103">(obsolète) Prévisions - ETS + STL</span><span class="sxs-lookup"><span data-stu-id="29641-103">(deprecated) Forecasting - ETS + STL</span></span>

> [!NOTE]
> <span data-ttu-id="29641-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="29641-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="29641-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="29641-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="29641-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="29641-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="29641-107">Cela [service web](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implémente des prédictions tooproduce modèles saisonnières tendance décomposition (STL) et lissage exponentiel (ETS) basé sur des données historiques hello fournies par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="29641-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implements Seasonal Trend Decomposition (STL) and Exponential Smoothing (ETS) models tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="29641-108">Sera hello à la demande pour une produit spécifique d’augmentation cette année ?</span><span class="sxs-lookup"><span data-stu-id="29641-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="29641-109">Puis-je je prédire Mes ventes de produits pour hello Noël, afin que je peux ainsi planifier efficacement Mon inventaire ?</span><span class="sxs-lookup"><span data-stu-id="29641-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="29641-110">Les modèles de prévision sont tooaddress apt ces questions.</span><span class="sxs-lookup"><span data-stu-id="29641-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="29641-111">Fonction hello au-delà de données, ces modèles examiner les tendances masquées et des tendances futures de saisonnalité toopredict.</span><span class="sxs-lookup"><span data-stu-id="29641-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="29641-112">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="29641-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="29641-113">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="29641-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="29641-114">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="29641-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="29641-115">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="29641-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="29641-116">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="29641-116">Consumption of web service</span></span>
<span data-ttu-id="29641-117">Ce service accepte des 4 arguments et calcule les prévisions hello.</span><span class="sxs-lookup"><span data-stu-id="29641-117">This service accepts 4 arguments and calculates hello forecasts.</span></span>
<span data-ttu-id="29641-118">les arguments d’entrée Hello sont :</span><span class="sxs-lookup"><span data-stu-id="29641-118">hello input arguments are:</span></span>

* <span data-ttu-id="29641-119">Fréquence - indique la fréquence de hello des données brutes de hello (quotidiennes/hebdomadaires/mensuelle/trimestrielle/annuelle).</span><span class="sxs-lookup"><span data-stu-id="29641-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="29641-120">Horizon : durée de validité des prévisions</span><span class="sxs-lookup"><span data-stu-id="29641-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="29641-121">Date - ajouter dans la nouvelle série de temps hello des données pour le moment.</span><span class="sxs-lookup"><span data-stu-id="29641-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="29641-122">La valeur - ajouter des valeurs de données de série hello nouvelle heure.</span><span class="sxs-lookup"><span data-stu-id="29641-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="29641-123">sortie Hello du service de hello est hello calculé prévision et les valeurs.</span><span class="sxs-lookup"><span data-stu-id="29641-123">hello output of hello service is hello calculated forecast values.</span></span>

<span data-ttu-id="29641-124">Exemple d'entrée :</span><span class="sxs-lookup"><span data-stu-id="29641-124">Sample input could be:</span></span> 

* <span data-ttu-id="29641-125">Frequency : 12</span><span class="sxs-lookup"><span data-stu-id="29641-125">Frequency - 12</span></span>
* <span data-ttu-id="29641-126">Horizon : 12</span><span class="sxs-lookup"><span data-stu-id="29641-126">Horizon - 12</span></span>
* <span data-ttu-id="29641-127">Date : 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="29641-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="29641-128">Value : 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="29641-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="29641-129">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="29641-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="29641-130">Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="29641-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="29641-131">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="29641-131">Starting C# code for web service consumption:</span></span>
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
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="29641-132">Création du service web</span><span class="sxs-lookup"><span data-stu-id="29641-132">Creation of web service</span></span>
> <span data-ttu-id="29641-133">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="29641-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="29641-134">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="29641-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="29641-135">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="29641-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="29641-136">Dans Azure Machine Learning, une nouvelle expérience vide a été créée.</span><span class="sxs-lookup"><span data-stu-id="29641-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="29641-137">Des exemples de données d’entrée ont été téléchargés avec un schéma de données prédéfini.</span><span class="sxs-lookup"><span data-stu-id="29641-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="29641-138">Schéma de données toohello lié est un [Execute R Script] [ execute-r-script] module, STL et ETS les modèles de prévision à l’aide de 'stl', 'ets', ce qui génère et les fonctions « prévision » à partir de R.</span><span class="sxs-lookup"><span data-stu-id="29641-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module, which generates STL and ETS forecasting models by using ‘stl’, ‘ets’, and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="29641-139">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="29641-139">Experiment flow:</span></span>
![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="29641-141">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="29641-141">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Exemples de données][3]    

#### <a name="module-2"></a><span data-ttu-id="29641-143">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="29641-143">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a><span data-ttu-id="29641-144">Limitations</span><span class="sxs-lookup"><span data-stu-id="29641-144">Limitations</span></span>
<span data-ttu-id="29641-145">Il s’agit d’un exemple très simple pour les prévisions ETS + STL.</span><span class="sxs-lookup"><span data-stu-id="29641-145">This is a very simple example for ETS + STL forecasting.</span></span> <span data-ttu-id="29641-146">Comme le montre hello exemple de code ci-dessus, aucune interception des erreurs n’est implémenté et service de hello suppose que toutes les variables de hello sont les valeurs continues/positive et la fréquence de hello doit être un entier supérieur à 1.</span><span class="sxs-lookup"><span data-stu-id="29641-146">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="29641-147">Hello longueur de vecteurs de valeur de date et hello doit être identique hello et longueur hello de MTS hello doit être supérieure à 2 * fréquence.</span><span class="sxs-lookup"><span data-stu-id="29641-147">hello length of hello date and value vectors should be hello same, and hello length of hello time series should be greater than 2*frequency.</span></span> <span data-ttu-id="29641-148">variable de date Hello doit respecter toohello format « mm/jj/aaaa ».</span><span class="sxs-lookup"><span data-stu-id="29641-148">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="29641-149">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="29641-149">FAQ</span></span>
<span data-ttu-id="29641-150">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="29641-150">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

